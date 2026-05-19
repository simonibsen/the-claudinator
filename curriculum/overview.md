# Curriculum Overview

A 12-week curriculum. Heavy on Claude & agents (Track A), serious on AI engineering (Track C), light on SWE practice (Track B) — just the essentials that close the coursework-to-job gap (spec kit, design docs, deploy, secrets).

**The through-line is productive Claude use.** Not a topic taught in week 1 and graduated from — the *operating mode* for every week. Each deliverable is built with Claude Code. Each week, your `~/.claude/commands/`, `~/.claude/skills/`, and project `CLAUDE.md` files should get a bit richer. That's the playbook, accumulated as code instead of journaled as prose.

**On pacing:** "a week" is the rhythm, not a contract. With Claude Code as a force multiplier, the time per exercise varies hugely — and unevenly. Scaffolding, navigation, boilerplate: minutes. Design decisions, debugging, evaluating tradeoffs: same as ever. **Don't aim for hours-per-week targets.** A week is *done* when the deliverable is in git and you can answer the self-assessment cold — see the four rules below.

| Track | Weight | Why |
|---|---|---|
| **A — Claude & agents** | ~60% | The lever; multiplies everything else |
| **C — AI engineering** | ~25% | Where the field is going; differentiator |
| **B — SWE essentials** | ~15% | Just enough to ship and not embarrass yourself |

## Week map

| Wk | A — Claude & Agents | B — SWE essentials | C — AI engineering |
|---|---|---|---|
| 1 | Daily-driver fluency + reading codebases | | |
| 2 | Customization, hooks, slash commands | Git & PRs (just enough) | |
| 3 | **Skills deep dive** — packaging, distribution, design | | |
| 4 | **Subagents & multi-agent orchestration** | | |
| 5 | **Spec Kit + plan mode** | RFC / design-doc writing | |
| 6 | **MCP — use, then build a server** | | |
| 7 | **Agent SDK — build a standalone agent** | | |
| 8 | **Claude API direct** (tool use, structured outputs, prompt caching) | | Tokens, models, costs |
| 9 | | Containers + deploy (Fly.io) | **RAG fundamentals** |
| 10 | **Evaluating your own agent** | | **Evals as a discipline** |
| 11 | **Prompt injection & red-teaming** | Secrets + structured logging | |
| 12 | **Capstone: ship an agent** | | |

## Four rules

1. **Every week has a deliverable in git.** Time spent without an artifact does not count.
2. **Every week ends with a self-assessment.** If you can't answer cold, the week is not done.
3. **Every week grows your `~/.claude/`.** A new slash command, skill, hook, or CLAUDE.md line — *something*. If you went a week without encoding a single productivity move, the through-line snapped. Fix it before moving on.
4. **One public artifact per month.** Blog post, OSS PR, or public repo with a real README.

## How to use this with the skill

- "Start week 3" / "teach me week 3" / "continue" — opens that week's file and walks through it
- "Quiz me on week 3" — runs the self-assessment as an interactive quiz
- "Review my work on week 3" — critiques the deliverable
- "Where am I" — reads `~/the-claudinator/progress.md` and tells you

## After the 12 weeks

Two paths, not mutually exclusive:
- **AI engineering concentration** — see `concentrations/ai-engineering.md`
- **OSS contribution streak** — pick a project, land 5 PRs over a quarter

The capstone (week 12) is the portfolio piece for internship interviews.
