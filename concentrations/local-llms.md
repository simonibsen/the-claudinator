# Local LLMs — and how Claude makes them yours

A post-curriculum concentration. Scoped as a small project — the centerpiece is a real distillation pipeline: take a task you've been paying Claude to do, use Claude to teach a small local model how to do it, and stop paying for that task.

This is not "set up Ollama and play around." Anyone can do that. This is *use Claude as a force multiplier to develop your own local model* — a skill most engineers ten years older haven't done.

## Why care

- **Cost.** Iterating on prompts and evals against the Claude API can run $10-50/week during the curriculum. Local models give you a free sandbox for dev work.
- **Privacy.** Personal data, school records, medical, anything sensitive — never has to leave your machine.
- **Latency.** A local 7-8B model on decent hardware responds faster than any API for short tasks. No network round-trip.
- **Career signal.** Distillation, LoRA fine-tuning, model routing — these are *AI infrastructure / AI engineer* skills. Mentioning a working distillation pipeline in an interview separates you from 95% of CS-junior peers.
- **Architecture literacy.** "Local vs. API" should be a deliberate choice. Knowing how to make that choice is the skill.

## Prerequisites

- **Module 10 (Evals) is non-negotiable.** Without a working eval harness, distillation is theater. You'll have no idea whether your local model is actually working.
- **Claude Code installed and fluent.** This concentration *operates* through Claude Code — generating datasets, writing training scripts, running comparisons, debugging quantization. If you're not fluent in Claude Code, do the curriculum first.
- **Hardware:**
  - **Comfortable:** Apple Silicon M-series (M1+) with 16GB+ RAM, OR Linux/Windows with NVIDIA GPU (8GB+ VRAM)
  - **Workable:** Any modern machine with 16GB RAM for inference of small (1-3B) models
  - **For training:** M-series with 32GB+ RAM, OR rent a GPU on Modal / Replicate / Colab Pro / Lambda for ~$1-5/run

## Roadmap

1. **Setup** — Ollama installed and running (Claude Code does most of it)
2. **Integration** — swap local for API with one line of code
3. **Compare** — port one Claude workload to local, run your module-10 evals on both
4. **Distillation pipeline** ⭐ — the centerpiece
5. **The orchestrator pattern** — Claude conducts, local LLMs work the volume
6. **Stretch** — embedding fine-tuning, model merging, vLLM serving

---

## 1. Setup — Ollama via Claude Code

In Claude Code, ask:

> Install Ollama on this machine. Pull `llama3.2:3b` and `qwen2.5:7b-instruct`. Verify they work with a one-shot prompt. Tell me what the disk and memory footprint is.

Claude Code will:
- Run the right install command for your OS
- Pull the models
- Test inference
- Report back with footprint and any issues

That's it. The 30-minute "follow the README" tutorial collapses to a one-shot Claude Code session.

**Model selection (current generation — refresh with the `update-content` mode):**

| Model | Size | Best for |
|---|---|---|
| `llama3.2:3b` | ~2GB | Fast iteration, weak machines (still useful) |
| `phi4-mini:3.8b` | ~2.5GB | Microsoft's current small model, strong reasoning |
| `gemma3:4b` | ~3GB | Google's current small model |
| `qwen3:8b` | ~5GB | Alibaba's current default 8B (replaces qwen2.5:7b-instruct) |
| `llama3.3:8b`-ish or `llama3.1:8b` | ~5GB | Reliable, well-supported |
| `gemma3:12b` | ~8GB | Google's strong mid-size |
| `phi4:14b` | ~9GB | Microsoft's reasoning-strong mid |
| `qwen3:14b` | ~9GB | If you have the RAM, much smarter |
| `mistral-small3.2:24b` | ~14GB | If you have a serious GPU |

The landscape moves monthly. As of May 2026 the active generations to be aware of include Qwen 3.5 / 3.6 (vision + tools + thinking), Gemma 4 (vision + audio + tools + thinking), Granite 4.1 (enterprise-leaning, 3B/8B/30B), and the established Llama 3.3+, Phi 4, and Mistral-Small 3.2. Don't memorize tags. Build the *framework* for choosing: how much VRAM you have, what task class (chat / code / structured output / vision / multimodal), how much speed you need, and what's currently strong on the OS leaderboards.

**Where to check current rankings:**
- The classic `huggingface.co/spaces/open-llm-leaderboard` exists but the actual leaderboard space has been dormant since early 2025. Look for the **Model Comparator** space on Hugging Face for a current alternative.
- LMSys-style arenas and the various `lmarena.ai`-flavored sites for head-to-head comparisons.

## 2. Integration — hot-swap local for API

Ollama serves an OpenAI-compatible REST API on `localhost:11434`. That means:

```python
# Before
from anthropic import Anthropic
client = Anthropic()
resp = client.messages.create(model="claude-haiku-4-5", messages=[...])

# After (local)
from openai import OpenAI
client = OpenAI(base_url="http://localhost:11434/v1", api_key="ollama")
resp = client.chat.completions.create(model="qwen2.5:7b-instruct", messages=[...])
```

**Exercise:** Take one app from module 8 (your classifier or summarizer). Add a `--local` flag that swaps the backend. Ask Claude Code:

> In `summarizer.py`, add a `--backend` flag that takes `claude-haiku-4-5`, `claude-sonnet-4-6`, `qwen2.5:7b-instruct`, or `llama3.2:3b`. Route to Anthropic for claude-* and to local Ollama for the rest. Keep the rest of the code unchanged.

You now have a switchable backend.

## 3. The eval comparison rig

This is where module 10's harness pays off. Run the same eval set against:
- The local model raw
- Claude Haiku
- Claude Sonnet
- (Later: your fine-tuned local model)

In Claude Code:

> Extend my eval harness in `evals/run.py` so it can take a `--backend` arg and score outputs for each backend separately. Output a comparison table with: eval pass rate, P95 latency, $/call (or $0 for local), tokens-per-second.

You'll typically see something like:

| Backend | Pass rate | P95 latency | $/call |
|---|---|---|---|
| `llama3.2:3b` | 0.61 | 1.2s | $0.000 |
| `qwen2.5:7b-instruct` | 0.78 | 2.1s | $0.000 |
| `claude-haiku-4-5` | 0.91 | 0.9s | $0.002 |
| `claude-sonnet-4-6` | 0.96 | 1.4s | $0.012 |

This gap (61-78% vs. 91-96%) is the thing distillation closes.

## 4. Distillation pipeline ⭐ (the centerpiece)

**The premise:** Claude is too expensive to call 1M times a month for a specific task you've defined. But Claude is smart enough to *teach* a 7B local model how to do that specific task. Once trained, the local model handles it for free.

### Step 1: Pick a task

A task that's: (a) repeatable, (b) you'd happily pay Claude to do many times, (c) narrow enough that "good enough" is achievable. Examples:

- *Summarize a Strava activity into 3 bullet points + an effort score*
- *Classify a customer support ticket into one of 12 categories*
- *Extract `{name, date, amount, category}` from an invoice text*
- *Generate 3 pytest test cases for a given Python function signature*
- *Rewrite a casual message into professional tone*

Pick something *you would actually use*. The pipeline is a real project — non-trivial, but tractable. If the artifact is useless to you, you'll lose interest before it ships.

### Step 2: Generate synthetic training data

Use Claude (Sonnet or Opus — quality matters here) to generate 800-1500 high-quality input-output pairs.

In Claude Code:

> Write a script that uses the Anthropic API to generate 1000 training examples for `<your task>`. Each example should be an input and a high-quality output. Vary the inputs broadly (length, edge cases, common cases). Save to `data/synthetic_train.jsonl`. Use prompt caching to reduce costs. Show me a progress bar and the running cost.

Cost: typically $3-10 for 1000 examples with Sonnet, less with caching.

### Step 3: Quality check

Two layers:

- **Manual:** Read 30 random examples yourself. Are the outputs actually good? If not, fix the generation prompt and re-run.
- **Automated:** Have Claude score each example for quality. Drop the bottom 10%. Ask Claude Code:

> Score every example in `data/synthetic_train.jsonl` for output quality on a 1-5 scale using `claude-haiku-4-5`. Drop the bottom 10%. Save as `data/train_filtered.jsonl`.

### Step 4: Train (LoRA)

Use **unsloth** (Linux/CUDA) or **MLX** (Mac Silicon) for accessible LoRA fine-tuning. Both have great docs.

In Claude Code:

> Write me an unsloth training script that fine-tunes `qwen2.5:7b-instruct` on `data/train_filtered.jsonl` using LoRA (rank 16, alpha 32, 3 epochs). Save the adapter to `models/my-finetune/`. Use a 90/10 train/val split and print val loss every epoch.

(Or the MLX equivalent if on Mac.)

Cost: ~$2-5 if you rent. Wall-clock varies a lot by hardware — GPU is fastest, M-series MLX is workable, slower hardware works but is slow enough to be annoying for iteration.

### Step 5: Eval

Run your comparison harness with the new fine-tuned model as a backend:

| Backend | Pass rate |
|---|---|
| `qwen2.5:7b-instruct` (raw) | 0.78 |
| `qwen2.5-finetuned` | **0.93** |
| `claude-haiku-4-5` | 0.91 |
| `claude-sonnet-4-6` | 0.96 |

When this works, the fine-tuned 7B local model matches or beats Haiku on your specific task. That's the moment. Free, fast, yours.

### Step 6: Deploy

Convert the adapter to GGUF for Ollama, or serve via MLX:

> Convert the LoRA adapter at `models/my-finetune/` to a GGUF format and create an Ollama Modelfile that uses it. Tag it as `my-task:latest`. Test that I can call it through Ollama's REST API.

Now: `client.chat.completions.create(model="my-task:latest", ...)` — and the task no longer hits the Claude API.

### Step 7: Document the result

Add a `WRITEUP.md` to the repo:
- The task and why it mattered
- Cost of fine-tuning ($X) vs. cost of paying Claude for the same task over 6 months ($Y)
- Eval results (before/after table)
- What went wrong and what you'd try next

**This writeup is the portfolio piece.** Title it something like "Fine-tuning Qwen 2.5 to handle [task] — a distillation experiment." Post to your blog. Link from your resume.

## 5. The orchestrator pattern — Claude conducts, local LLMs work

A complementary pattern to distillation. Distillation collapses *one Claude task* into *one local model*. The orchestrator pattern keeps Claude in the loop — but only for the parts that need it — and dispatches the *volume* to local workers.

**The premise:** Claude is too expensive to call N times when N is large. But Claude is *smart* enough to direct local-LLM workers that handle the volume. You get Claude's reasoning where it matters and near-zero-cost execution everywhere else.

### The shape

1. **Claude plans** — given the task, designs the worker prompt and the validation criteria
2. **Local LLM executes** — runs the same prompt against every item in the batch
3. **Claude sample-validates** — checks ~5% of worker outputs, catches systematic errors
4. **Claude synthesizes** — takes the worker outputs and produces the final result, handling edge cases the workers flagged

### When it fits

- Input is large (1k+ items, a long document with many chunks, a batch of files)
- Each item needs *medium-difficulty* work — too hard for a regex, not hard enough to justify $0.012 per Claude Sonnet call
- Output needs aggregation, validation, or synthesis at the end — where Claude shines

### Use cases worth building

- Extracting structured fields from 5,000 invoices or receipts
- Summarizing each chunk of a long document before final synthesis
- First-pass classification of support tickets, with Claude handling the ambiguous middle
- Generating exam questions or flashcards from a corpus
- Tagging or categorizing a large media library

### Hard parts (where this goes wrong)

- **Worker prompts need to be air-tight.** A local model has less context-recovery than Claude; a vague prompt gets you a lot of bad batched output.
- **Validation is non-optional.** Sampling 5% of worker outputs and grading them is the difference between "this works" and "I think this works."
- **Edge cases need a fallback to Claude.** Design routing so the worker can flag "I don't know" and the orchestrator handles those cases with a Claude call.
- **Eval the pipeline, not just the workers.** A worker can score 0.85 individually and produce a 0.4 pipeline output if the synthesis step is brittle.

### Exercise

Take a real batch task you have. Build the pipeline in Claude Code:

1. **Design the worker prompt** with Claude against 10 hand-checked examples. Iterate until the local model gets all 10 right.
2. **Run the local worker on the full batch.** Cheap.
3. **Have Claude sample-validate** 50 outputs against the original criteria. Calculate worker accuracy.
4. **Have Claude synthesize** the batch outputs into the final result, handling worker uncertainty.
5. **Compare end-to-end cost** vs. "Claude does it all." Typical: 10-100× savings if the task fits the pattern.

If the worker accuracy comes in under 90%, the task probably doesn't fit — either distill a fine-tuned worker (section 4), or accept that this is a Claude-all-the-way job.

### Why this is career signal

This is the production pattern at companies running AI at scale: cheap workers handle volume, expensive orchestrator handles judgment. Most engineers haven't built one. If you can describe one of these in an interview — concrete task, real cost savings, eval results — you sound several years older than you are.

### How this relates to module 4

Module 4 covers Claude orchestrating *Claude subagents*. The orchestrator pattern is the same shape with *local LLMs* as the workers. The trade-off: Claude-subagent workers are smart and expensive; local-LLM workers are dumb and free. Pick based on task difficulty and volume.

## 6. Stretch — embedding fine-tuning

For RAG workloads, often higher ROI than generative fine-tuning. The idea: train a small embedding model on your specific domain so retrieval actually works.

In Claude Code:

> Generate 500 (query, relevant document) and 500 (query, irrelevant document) pairs from my RAG corpus using Claude. Use them to fine-tune `sentence-transformers/all-MiniLM-L6-v2` with a contrastive loss. Compare retrieval@5 before and after on a held-out test set.

Genuinely useful for your module-9 RAG.

## 7. Stretch — model merging

Combining two fine-tuned models' weights to get capabilities from both. Tools: `mergekit`. Mostly experimental, sometimes magical. Ask Claude Code to walk you through a merge of your fine-tuned model with another task-specialized model — see if the result is better at both tasks.

## 8. Stretch — vLLM serving

For production-grade serving (high concurrency, batching, optimized inference). Ollama is great for dev; vLLM is what you'd run if your local model were behind a real service. Worth knowing exists.

## When to use local vs. API — decision matrix

| Scenario | Use |
|---|---|
| Iterating on a prompt, dev sandbox | Local |
| Building/debugging a feature | Local until working, then promote |
| Workload you call >100k times/month, narrow task | Distill to local |
| Workload you call <10k times/month | Stay on API |
| Anything user-facing in production right now | API (probably Haiku or Sonnet) |
| Privacy-sensitive personal data | Local |
| Need reasoning quality of frontier model | Opus |
| Need cost of nothing | Local |
| Multi-turn agentic work with tool use | API (local tool use is still shaky) |

## Hardware honesty

- **M-series Mac with 16GB RAM:** comfortable for 7B inference, slow but workable for 7B LoRA training via MLX
- **M-series Mac with 32GB+ RAM:** comfortable for 14B inference, real training territory
- **NVIDIA GPU 8GB VRAM:** comfortable for 7B inference, doable for LoRA training
- **NVIDIA GPU 16GB+ VRAM:** comfortable for 14B inference, fast training
- **Lower-end laptop:** 1-3B models for inference only; rent GPU for training. $1-5/run on Modal or Lambda.

If your hardware is limiting you, *don't skip the distillation exercise* — rent a GPU for the training step. That's a normal AI engineering reality, not a workaround.

## What to read next

- **unsloth** documentation — `github.com/unslothai/unsloth` (Apple Silicon training, MLX + GGUF inference all supported as of May 2026; NVIDIA RTX 30/40/50/Blackwell + DGX; AMD chat/data shipped, full AMD training coming. Multi-GPU with ongoing improvements. Unsloth Studio gives a cross-platform web UI.)
- **MLX-LM** — `github.com/ml-explore/mlx-lm` (standalone repo). Install with `pip install mlx-lm`.
- **HuggingFace fine-tuning guide** — official docs, deepest reference
- **Hamel Husain on fine-tuning** — his posts on when fine-tuning actually helps (and when it doesn't)
- **Simon Willison on local LLMs** — practical posts on what's worth running
- **Open LLM Leaderboard** — `huggingface.co/spaces/open-llm-leaderboard` for current model rankings

## Self-assessment

1. Walk through your distillation pipeline in 2 minutes — could you do this in an interview?
2. Your fine-tuned model dropped from 0.93 → 0.80 after re-training. What are the first three things you check?
3. Why doesn't anyone use local models for everything?
4. When does fine-tuning beat prompt engineering? When does prompt engineering beat fine-tuning?
5. What's the cost calculation that justified your specific distillation? (Be specific: $/month saved vs. one-time training cost vs. ongoing eval/maintenance.)

## A note on what ages fast

Specific model names (Llama 3.2, Qwen 2.5), tool names (unsloth, MLX), and version-specific commands in this file will be stale in 3-6 months. The *concepts* (distillation, LoRA, hybrid routing, eval-driven local development) age much slower. When something here doesn't work, ask Claude Code: "this command/model is from May 2026, what's the current equivalent?"
