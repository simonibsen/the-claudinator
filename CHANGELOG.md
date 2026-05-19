# Changelog

Notable changes to the curriculum. Newest first.

## 2026-05-19

**Local LLMs concentration added.**
- New `concentrations/local-llms.md` — post-curriculum, ~8-12 hours.
- Framed not as "how to use local LLMs" but "how to use Claude as a force multiplier to develop your own local model."
- Centerpiece: a real **distillation pipeline** — pick a task you've been paying Claude for, use Claude to generate ~1000 synthetic training examples, fine-tune a 7-8B local model with LoRA (unsloth/MLX), eval against Claude, deploy.
- Covers: Ollama setup via Claude Code, hot-swap backend integration, eval comparison rig, distillation, embedding fine-tuning, model merging, vLLM serving, when-to-use-local decision matrix, hardware honesty.
- Sidebar mentions added to week 8 (preview local backend swap) and week 10 (local LLM-as-judge with caveats).
- Reading list updated with Ollama, unsloth, MLX, HuggingFace, Open LLM Leaderboard, mergekit.
- SKILL.md routing now triggers the concentration on "local LLMs", "ollama", "fine-tuning", "distillation", "run a model locally".

**Renamed: AI Forge → The Claudinator.** A nod to Dr. Doofenshmirtz. Directory, slug, state path (`~/the-claudinator/`), display name updated throughout.

**Public-contribution streak broadened (formerly OSS-only).**
- `oss` focus and capstone option 4 now explicitly invite contributions in non-code domains: music software (Ardour, LMMS, music21, Mutopia), hardware/embedded, games, scientific computing, creative tools, education, datasets, docs/translations.
- Contribution form is flexible: a music21 bug fix, an LMMS instrument preset, a transcribed sheet music score, an Anki deck, an OpenStreetMap streak — all count.
- "What matters is real contribution to something a community uses, in a domain you care about."

**Interest discovery added to `builder` and `ai-engineer` focuses.**
- On focus switch, the tutor asks 2-3 questions about what they care about. Answers steer exercise examples, capstone selection, and reading-list emphasis — not week selection.
- Pattern parallels what `oss` already does.

**Focus mode added.**
- New `modes/focus.md` — five focuses (`full`, `builder`, `ai-engineer`, `productivity`, `oss`).
- Three are behavioral hints (same 12 weeks, different depth/pace); two are structural (`productivity` ends at week 5, `oss` replaces weeks 6-12 with an OSS streak).
- Focus is a default — per-session overrides always honored, but the tutor pushes back on skipping load-bearing items (evals, security, specs).
- Proactively offered once, after week 2 finishes. Not at first-run.
- Stored as `focus:` line in `~/the-claudinator/progress.md`; default `full`.
- Other modes (teach, coach) updated to consult focus.
- `oss` focus and the capstone option 4 both start with an **interest-discovery conversation** before any issue hunting — pick from passion, not from convenience. Claude Code is the operating tool throughout the OSS work (navigate, draft, PR-prep, review responses).

**Productivity through-line reframe.**
- SKILL.md now states explicitly that productive Claude use is the operating mode across every week and path, not a topic graduated from in week 2.
- The "playbook" is *code* — slash commands, skills, hooks, CLAUDE.md additions — not a journal. No prose-writing requirement.
- Critique mode now flags productivity-encoding misses (repeated prompts, unencoded conventions).
- Quiz mode now includes one applied-productivity question per session.
- Coach mode runs a monthly diagnostic ("name one Claude move you started using this month") and watches `~/.claude/` growth as a health signal.
- Teach mode reads `~/.claude/commands/` and `~/.claude/skills/` at session start; surfaces productivity moments during work.
- Weeks 1-2 reframed as the productivity foundation. Week 1 gains a "productivity recipes" exercise.
- Curriculum overview adds a 4th rule: every week must grow `~/.claude/` by something concrete.

**Initial authoring.**
- 12-week curriculum, tracks A/B/C weighted ~60/15/25.
- Six interactive modes (teach, quiz, critique, interview, coach, update-content).
- Two post-curriculum concentrations (AI engineering, capstone options).
