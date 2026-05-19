# The Claudinator

A self-paced, 12-module curriculum for going from *"I can code"* to *"I can ship agents."*

It lives as a Claude Code skill — you install it once, then talk to it in natural language. It tracks your progress, walks you through modules, quizzes you, critiques your work, runs mock interviews, and keeps itself fresh against the latest Claude / MCP / API docs.

## What you'll come out with

By the end of the 12 modules, you'll have:

- **A real agent you've shipped** — with a public repo, a working URL or installable CLI, an eval harness, structured logging, and a writeup someone would actually read.
- **A personal Claude Code playbook in code** — your `~/.claude/commands/`, `~/.claude/skills/`, hooks, and project `CLAUDE.md` files measurably richer than they were day 1. Productivity moves encoded, not journaled.
- **Working fluency with the core stack** — Claude Code daily-driver use, custom skills and subagents, Spec Kit, MCP (using *and* building servers), the Agent SDK, the Anthropic API directly (caching, structured outputs, tool use).
- **Real AI engineering muscle** — RAG from scratch, an eval harness you trust, prompt injection awareness, prompt caching as production craft.
- **Just enough professional SWE practice** — design docs, containers + deploy, secrets handling, structured logging, git/PR hygiene.
- **A public artifact per month** — by end of curriculum: 3 substantive things shipped (blog posts, PRs, repos) that recruiters can find.

## Who this is for

Someone with **real coding experience** but limited applied-AI / professional-dev exposure. The intended baseline:

- You write code fluently in at least one language (Python or TypeScript work best for the exercises).
- You're comfortable with git, the command line, and reading docs.
- You haven't built much that runs in production, written a design doc, or evaluated an AI system.

Roughly: a CS undergrad past the data-structures-and-algorithms stage, a bootcamp grad with a real project under their belt, or a working engineer pivoting into AI. **Not** a first-time programmer.

Time commitment: a rhythm of Twelve modules, no fixed duration. **Hours per module varies a lot** based on Claude Code fluency — exercises that pre-Claude would have been 5 hours can be 30 minutes with the tool, while the genuinely thinking-heavy parts (design, debugging, evals) take the same time as ever. Don't target hours. A module is *done* when the deliverable is in git and you can answer the self-assessment cold.

## How it works

You install the skill in Claude Code, then talk to it like a tutor:

- `/the-claudinator` — first-run setup, or pick up where you left off
- *"Teach me module 4"* — walks you through the module one step at a time
- *"Quiz me on what I just learned"* — 10 interactive questions, honest grading
- *"Review my work"* — senior-engineer-style code review of your deliverable
- *"Mock interview me on AI engineering"* — 20-30 minutes, with debrief
- *"Switch focus to builder"* — change the path you're on (more below)
- *"Update the curriculum"* — refresh content against current Claude / MCP / API docs

The tutor reads your `~/the-claudinator/progress.md` every session to know where you are. It's strict-but-encouraging: it will tell you if a deliverable is shallow, push back when you try to skip the parts that matter (evals, security, specs), and not soften feedback you'd benefit from hearing straight.

## The 12 modules

Three parallel tracks, weighted toward Claude and agents:

| Track | Weight | What it gets you |
|---|---|---|
| **A — Claude & agents** | ~60% | Skills, subagents, MCP, Agent SDK, Spec Kit, the Anthropic API directly |
| **C — AI engineering** | ~25% | RAG, evals, prompt injection, prompt caching, cost engineering |
| **B — SWE essentials** | ~15% | Just enough git, specs, containers, deploy, secrets, logging — the gap between coursework and a real job |

Module by module:

| Wk | Topic | Deliverable |
|---|---|---|
| 1 | **Daily-driver fluency + reading codebases** — moves that pay off Monday | `CLAUDE.md` + an OSS codebase map |
| 2 | **Customization, hooks, slash commands + git at team scale** | `~/.claude/` set up + a merged OSS PR |
| 3 | **Skills deep dive** — packaging, distribution, model-invoked design | A routing skill on GitHub |
| 4 | **Subagents & multi-agent orchestration** | A custom subagent + writeup on when it helped vs. hurt |
| 5 | **Spec Kit + plan mode + RFC writing** | A feature built spec-first + a design doc |
| 6 | **MCP — use existing servers, then build one** | Your own MCP server, repo + README |
| 7 | **Agent SDK — build a standalone agent** | A CLI agent in your terminal + writeup |
| 8 | **Claude API directly** — tool use, structured outputs, prompt caching | 3 small API apps + cost analysis |
| 9 | **Containers + deploy + RAG fundamentals** | A dockerized RAG app at a real URL |
| 10 | **Evals as a discipline** | An eval harness with ≥20 cases on your RAG |
| 11 | **Prompt injection, red-teaming, secrets, logging** | Attack writeup + mitigations + structured logs |
| 12 | **Capstone — ship a real agent** | Public repo, evals passing, one real user |

Full details: [`curriculum/overview.md`](curriculum/overview.md) — and each module's file in [`curriculum/`](curriculum/).

## Focus paths

The curriculum has five focuses you can pick (after module 2, when you know what you want):

| Focus | What changes |
|---|---|
| **`full`** *(default)* | All 12 modules, full depth — pick this if undecided |
| **`builder`** | Compress theory, skip stretches, ~2x time on building; for hackathon/internship application speed |
| **`ai-engineer`** | Light on modules 4-6, heavy on 8-11; for AI/ML eng job signal |
| **`productivity`** | Stop at module 5; replace capstone with "use Claude Code daily on a real project for a month" |
| **`oss`** | Replace modules 6-12 with a public-contribution streak (5 substantive contributions in code, music, hardware, games, datasets — anything with a community) |

Focus is a *default*, not a contract. You can override per-session ("for this module, go deep on security even though I'm `builder`"). The tutor pushes back if you try to skip load-bearing items like evals or specs.

Details: [`modes/focus.md`](modes/focus.md).

## The capstone

Module 12 is where pieces become a project. You ship a real, useful agent that combines at least 5 modules of material:

- Spec'd via Spec Kit (module 5)
- Built with the Agent SDK or as a Claude Code skill (modules 3, 7)
- Often using MCP for external tools (module 6) and RAG for context (module 9)
- Evaluated with a real harness (module 10)
- Security-aware (module 11)
- Deployed at a public URL or installable repo (module 9)
- With a blog-post-quality writeup
- And **one real user** other than you

Four scoped project options live in [`concentrations/capstone-options.md`](concentrations/capstone-options.md):
1. Personal study copilot
2. Domain-specific MCP server + agent
3. Eval-driven prompt optimizer
4. Public-contribution streak (5 merged contributions in your domain of choice)

Plan it as a real project, not a homework set. The artifact is what you point recruiters at.

## Concentrations (after the 12 modules)

Post-curriculum deep dives, each scoped as a small project:

- **[AI engineering](concentrations/ai-engineering.md)** — evals as a profession, prompt caching, embedding work, agent architectures, fine-tuning. The career leverage track for AI/ML eng jobs.
- **[Local LLMs](concentrations/local-llms.md)** — running and *developing* local models with Claude as a force multiplier. Centerpiece is a real **distillation pipeline**: use Claude to teach a 7B local model your specific task, then stop paying for that task.

## The through-line: productive Claude use

This isn't "learn Claude in modules 1-2 then move on." Across every module and every focus, productively using Claude Code is *how* you do the work. The "playbook" is code — your accumulating `~/.claude/commands/`, `~/.claude/skills/`, hooks, and `CLAUDE.md` files — not a journal.

Each module's deliverable is built with Claude Code. By module 12, your `~/.claude/` directory should look visibly different than it did module 1. That accumulation is itself a portfolio piece.

## Install

```bash
git clone https://github.com/simonibsen/the-claudinator ~/.claude/skills/the-claudinator
```

Then open Claude Code in any working directory and run the slash command:

```
/the-claudinator
```

The skill appears in the `/` menu and walks you through first-run setup. After that, you can use either:

- The slash command — `/the-claudinator quiz me on module 3`
- Natural language — *"quiz me on module 3"*, *"continue"*, *"switch focus"* — Claude Code will route phrases that match the skill's description back into it.

**Restart caveat:** if `~/.claude/skills/` didn't exist before you cloned this in, restart Claude Code so the skills directory gets watched. If the directory was already there, no restart needed — the skill is picked up immediately.

See [`INSTALL.md`](INSTALL.md) for details on prerequisites, tuning, and keeping content fresh.

## What's inside

```
the-claudinator/
├── SKILL.md              # entry point — the model loads this first
├── curriculum/           # 12 module files + the overview
├── modes/                # teach, quiz, critique, interview, coach, focus, update-content
├── concentrations/       # AI engineering, local LLMs, capstone briefs
├── habits.md             # daily/weekly/monthly practices
├── reading-list.md       # canonical sources (docs, blogs, books, people)
├── state-template.md     # template for your ~/the-claudinator/progress.md
├── INSTALL.md            # detailed install + tuning guide
└── CHANGELOG.md          # curriculum revisions over time
```

Your progress lives in `~/the-claudinator/` (created on first run). Push it to a private repo — a year of tracked learning is itself a portfolio.

## Keeping it fresh

The Claude / MCP / API surface area moves fast. Ask:

> Update the curriculum

The tutor checks the major sources, proposes edits where claims have gone stale, and (with your approval) applies them. Tracked in `last-refreshed.txt`.

## Tuning

Everything is plain markdown — edit anything that doesn't fit. Pace, track weighting, tone, exercises, module order. See [`INSTALL.md`](INSTALL.md#tuning-it-for-yourself).

## License

MIT. Fork it, adapt it, share it.

## Contributing

PRs welcome — especially for keeping content current, adding capstone options, refining mode prompts, or improving the local-LLM and AI-engineering concentrations. Open an issue first for larger changes.
