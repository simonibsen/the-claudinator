# Changelog

Notable changes to the curriculum. Newest first.

## 2026-05-19

**Renamed: "week" → "module" throughout.** The "12-week curriculum" framing was misleading — Claude Code makes pacing wildly uneven and the calendar-week unit fights the deliverable-driven success criterion. Twelve modules, no fixed duration; a module is done when the deliverable is in git and the self-assessment is passed cold.

- All 12 curriculum files renamed: `curriculum/week-NN-*.md` → `curriculum/module-NN-*.md` (via `git mv` so blame history follows).
- Headings: `# Week N — X` → `# Module N — X`.
- Cross-references swept: ~100+ references across curriculum, modes, concentrations, README, INSTALL, SKILL.md, overview, habits, state-template.
- Pacing language in `overview.md`, `README.md`, `INSTALL.md` rewritten to match: no "8-10 hrs/week" or "a week per week" framing; "twelve modules, no fixed duration" instead.
- Self-template `Week: 1` → `Module: 1`.
- SKILL.md routing accepts both "module N" and "week N" phrasings as backward-compat alias — the description prefers "module" but the routing won't break for students who already think in week-terms.
- Kept where genuinely real-time: cost-per-week (real money over real time), habit cadences (daily/weekly/monthly), OSS streak duration ("over 4-6 weeks"), publication cadence ("Import AI weekly roundup"), real-time observations in coach mode ("no commits in 2+ weeks").

**Check-updates mode added.**
- New `modes/check-updates.md` — checks `~/.claude/skills/the-claudinator` against `origin/main`, summarizes new commits, offers a fast-forward pull.
- Auto-runs at session start with a 24-hour floor (silent when in sync; one-line mention when behind; never nags).
- Handles symlinked installs by resolving `readlink -f` first.
- Non-destructive: read + fetch + propose; pull only on explicit consent; never auto-resolves conflicts.
- Stamps `~/the-claudinator/last-update-check.txt` to respect the floor.

**Week 5 — SDD deepened.**
- New exercise 6: the constitution. 5-10 disagree-able principles, each expressing a real trade-off. Loaded into `.specify/memory/constitution.md` via `/speckit.constitution`.
- New exercise 7: the iteration loop (when the spec is wrong). Practice updating the spec, re-running `/speckit.plan`, and rederiving tasks — the realistic SDD case, not pure waterfall.
- Deliverable expanded to require a constitution + a visible spec revision in git history.
- Self-assessment grew from 5 to 7 questions covering the new exercises.

**Orchestrator pattern added** (Claude conducts, local LLMs work).
- New section 5 in `concentrations/local-llms.md`: full pattern, when it fits, hard parts, exercise, career-signal framing, relationship to week 4.
- Closes the gap where the curriculum covered Claude-orchestrating-Claude-subagents (week 4) but not Claude-orchestrating-local-LLM-workers.
- Sidebar added to week 4 pointing forward to it.
- Renumbered subsequent sections of the concentration (5→6 embedding fine-tuning, 6→7 model merging, 7→8 vLLM serving).

**Dropped per-exercise hour estimates and softened week-level framing.**
- Hour annotations like `(1 hr)`, `(30 min)`, `(4-5 hrs)` removed from all 12 week files. Estimates were inflated post-Claude-Code (parts that pre-Claude took hours can now take minutes; parts that are thinking-heavy didn't get faster). Annotations created false precision and a wrong success signal.
- Week-level "~8-10 hrs/week" softened across `curriculum/overview.md`, `README.md`, `INSTALL.md`. New framing: "a rhythm of a week per week, hours-per-week varies a lot — a week is *done* when the deliverable is in git and the self-assessment is passed cold."
- Capstone "20-40 hours of work" replaced with project-shape framing ("small but real project, not a toy; one-sentence pitch, 60-second demo").
- Local LLMs concentration: time promises stripped (Ollama setup, pipeline duration, embedding fine-tuning); cost-of-rental retained where useful for decision-making.
- Project artifacts (deliverable, self-assessment, slash-commands grown) remain the success measure — they always were, the hour annotations were just clutter.

**Comprehensive correctness audit pass.** Verified every behavioral claim against live docs (Claude Code, Anthropic API, MCP, Spec Kit, Ollama, MLX, OWASP, unsloth). Fixes:

- **Week 5 (Spec Kit):** Commands now `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement` (previously bare). Added supporting commands (`/speckit.constitution`, `/speckit.clarify`, `/speckit.analyze`, `/speckit.checklist`, `/speckit.taskstoissues`). Install: `uv tool install specify-cli --from git+...`. Output paths updated.
- **Week 6 (MCP):** Removed GitHub/Postgres from reference servers (archived); current list: Everything, Fetch, Filesystem, Git, Memory, Sequential Thinking, Time. Python SDK: `FastMCP` from `mcp.server.fastmcp` via `uv add "mcp[cli]"`. TS SDK: `@modelcontextprotocol/sdk` + `zod`. Added the three primitives (tools/resources/prompts) and two transports (stdio/Streamable HTTP) with OAuth 2.1 for HTTP.
- **Week 7 (Agent SDK):** Package is `claude-agent-sdk` (Python) / `@anthropic-ai/claude-agent-sdk` (TS), not the `anthropic` SDK. Uses `query()` async iterator, not a hand-rolled Messages loop. Added explicit distinction from the Client SDK (week 8's territory).
- **Week 3 (Skills):** Custom commands have been merged into skills — `.claude/commands/X.md` and `.claude/skills/X/SKILL.md` both create `/X`. Only `description` is recommended in frontmatter; `name` defaults to dir name. Added frontmatter reference (disable-model-invocation, user-invocable, allowed-tools, argument-hint, context: fork).
- **Week 4 (Subagents):** Subagent frontmatter `name` AND `description` ARE both required. Subagents CANNOT spawn subagents (only the main thread can). File-edited subagents need restart; `/agents`-created ones don't. Added awareness of "agent teams" and "background agents" as related concepts.
- **Week 2 (Customization):** Hook event list expanded from 3 to the ~30 actual events (`SessionStart`, `UserPromptSubmit`, `PermissionRequest`, `SubagentStart/Stop`, `PreCompact`, `Elicitation`, etc.). Permissions section deepened: rule syntax (`Bash(git *)`, `Edit|Write`, `Skill(name *)`, `mcp__server__.*`), four scopes (managed/user/project/project-local), hook handler types.
- **Week 8 (API):** Prompt caching detail added — two TTLs (5-min, 1-hour), cost ratios (1.25x/2x write, 0.1x read), 4 breakpoints max, 20-block lookback, minimum cacheable length per model.
- **Week 11 (Security):** OWASP LLM Top 10 updated to 2025 edition (10 categories listed by ID).
- **Local LLMs concentration:** Model tags refreshed (added phi4/phi4-mini, gemma3, qwen3, mistral-small3.2). MLX-LM moved from `ml-explore/mlx-examples` to `ml-explore/mlx-lm` (standalone repo, `pip install mlx-lm`). Open LLM Leaderboard noted as dormant; Model Comparator recommended instead.
- **Doc base URLs:** `claude.com/claude-code/docs` → `code.claude.com/docs/en/` (Claude Code) and `docs.claude.com/en/docs/` (Anthropic API) throughout.
- **Reading list:** All Claude/MCP/local-LLM links updated to current URLs.

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
