# Week 8 — Claude API Direct: Caching, Tools, Structured Outputs

**Frame:** Claude Code, Claude.ai, and the API are three surfaces on the same underlying model. To build production AI features, you need to know the API directly — and the primitives that make production work: prompt caching, structured outputs, batch.

## Objectives

1. Use the Anthropic SDK directly (not via Claude Code) for at least 3 different tasks.
2. Implement prompt caching and verify the cost reduction.
3. Use structured outputs (JSON schema, tool-use-as-output) reliably.
4. Pick the right model for each task: Haiku, Sonnet, Opus.
5. Build cost/latency awareness as a habit, not a chore.

## Readings

- Anthropic API docs — Messages, Tool Use, Structured Outputs, Prompt Caching, Batch.
- The `anthropic-cookbook` repo on GitHub.
- One blog post on prompt caching economics (e.g. "Anthropic prompt caching saves us X").

## Exercises

**1. SDK setup.** Install the Python or TypeScript Anthropic SDK. Set up an API key (in a `.env`, never committed). Make your first request.

**2. Three small apps.**
- A summarizer (long input, short output).
- A classifier returning structured JSON (use tool use or `response_format` if applicable).
- A multi-turn assistant with conversation history.

**3. Prompt caching.** Take one of the apps where you reuse a long system prompt. Add caching. Measure: tokens before/after, cost before/after. Document the savings.

Key facts to know:
- **Two TTLs:** 5-minute (default, `{"type": "ephemeral"}`) and 1-hour (`{"type": "ephemeral", "ttl": "1h"}`).
- **Cost ratios:** cache *write* is 1.25× base input (5-min) or 2× (1-hour); cache *read* is 0.1× base input.
- **Cache hit requires 100% exact prefix match** up to the breakpoint. Lookback window is 20 blocks.
- **Up to 4 breakpoints per request.** Hierarchy: `tools` → `system` → `messages` — a change at any level invalidates that level and below.
- **Minimum cacheable length:** 4,096 tokens (Opus 4.7/4.6/4.5, Haiku 4.5); 1,024 tokens (Sonnet).
- Track via `usage.cache_creation_input_tokens` and `usage.cache_read_input_tokens` in the response.

**4. Model routing.** For each of your three apps, run with Haiku, Sonnet, and Opus. Compare quality, latency, cost. Pick the right one. Justify in writing.

**5. Cost dashboard.** Add a simple cost logger to your apps: tokens in, tokens out, cache hits, $ per call. Print at the end of every run. (Make this a habit going forward.)

## Deliverable

- A repo with 3 small API-based apps, each with a README explaining the use case
- A `costs.md` writeup: prompt caching savings, model routing decisions, $/call for each app
- Your `.env` is in `.gitignore` and your API key is not in the repo (verify with `git log -p`)

## Self-assessment

1. What's the difference between using Claude Code and using the API directly? When is each right?
2. Prompt caching: what's the TTL, what counts as a cache hit, and what breaks the cache?
3. Two ways to get structured JSON out of the model. Which is more reliable and why?
4. When is Haiku the right choice over Sonnet? Give a concrete example.
5. Your API bill spikes 10x. What are your first three diagnostic steps?

## Common pitfalls

- **API key in git.** Even if you delete the commit, it's compromised. Rotate immediately.
- **Reinventing JSON parsing.** Use tool use or `response_format` — don't regex JSON out of free text.
- **Always Opus.** Most workloads don't need it. The cost adds up.
- **No cost logging.** "I'll add it later" is how surprise bills happen.
- **Cache misses you didn't expect.** Cache requires *exact* prefix match; appending then prepending breaks it.

## Stretch

Use the Batch API for a job that doesn't need real-time response (overnight summarization of a backlog). Measure cost vs. the synchronous version.

## Sidebar — local models as a sandbox

While you're here building API skills, build the *swap-the-backend* muscle. Set up Ollama with a 7B model (Claude Code can install + configure it for you), and add a `--backend` flag to one of your apps so it can route to a local model instead. You don't have to use local everywhere — but knowing how, and developing the reflex *"do I need an API model for this?"*, is a real AI engineering skill. After week 12, the `concentrations/local-llms.md` deep-dive turns this into a distillation pipeline. Worth previewing now.
