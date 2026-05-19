# The Claudinator

A self-paced, 12-week curriculum for going from *"I can code"* to *"I can ship agents."*

It lives as a Claude Code skill — you install it once, then talk to it in natural language inside Claude Code. It tracks your progress, walks you through weeks, quizzes you, critiques your work, runs mock interviews, and keeps itself fresh against the latest Claude / MCP / API docs.

## The 12 weeks

The curriculum runs three parallel tracks:

| Track | Weight | What it gets you |
|---|---|---|
| **A — Claude & agents** | ~60% | Skills, subagents, MCP, Agent SDK, Spec Kit, the API directly |
| **C — AI engineering** | ~25% | RAG, evals, prompt injection, prompt caching, cost engineering |
| **B — SWE essentials** | ~15% | Just enough git, specs, containers, deploy, secrets, logging |

Each week ends with a deliverable you push to git. The capstone (week 12) is a real agent you ship — the portfolio piece for internship interviews.

Full week-by-week map: [`curriculum/overview.md`](curriculum/overview.md)

## Install

```bash
git clone https://github.com/<you>/the-claudinator ~/.claude/skills/the-claudinator
```

Open Claude Code, say *"Start the study plan"*, and follow along. See [`INSTALL.md`](INSTALL.md) for details.

## How you talk to it

| You say... | What happens |
|---|---|
| "Start the study plan" / "where am I" | First-run setup, or "you're on week N, want to continue?" |
| "Teach me week 3" / "continue" | Walks through the current/specified week |
| "Quiz me on week 4" | 10-question interactive quiz |
| "Review my work for week 5" | Senior-engineer-style code review |
| "Mock interview me on AI engineering" | 20-30 minute mock interview with debrief |
| "Show me capstone options" | Capstone project briefs |
| "Update the curriculum" | Audits the content against current docs and proposes edits |

## What's inside

```
the-claudinator/
├── SKILL.md              # entry point — the model loads this first
├── curriculum/           # 12 week files + the overview
├── modes/                # teach, quiz, critique, interview, coach, update-content
├── concentrations/       # AI engineering deep dive + capstone briefs
├── habits.md             # daily/weekly/monthly practices
├── reading-list.md       # canonical sources (docs, blogs, books, people)
├── state-template.md     # template for your progress.md
├── INSTALL.md            # detailed install + tuning guide
└── CHANGELOG.md          # curriculum revisions over time
```

Your progress lives in `~/the-claudinator/` (created on first run). Push it to a private repo — a year of tracked learning is a portfolio in itself.

## Keeping it fresh

The Claude/MCP/API surface area moves fast. Run:

> Update the curriculum

The tutor will check the major sources, propose edits where claims have gone stale, and (with your approval) apply them. It tracks `last-refreshed.txt` so you don't have to remember.

## Tuning

Everything is plain markdown — edit anything that doesn't fit you. Pace, track weighting, tone, exercises, week order. See the "Tuning" section in [`INSTALL.md`](INSTALL.md).

## License

MIT. Fork it, adapt it, share it.

## Contributing

PRs welcome — especially for keeping content current, adding capstone options, or improving any of the modes. Open an issue first for larger changes.
