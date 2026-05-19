# Install — The Claudinator

A self-paced, 12-week curriculum for going from "I can code" to "I can ship agents." Lives as a Claude Code skill, so you talk to it in natural language inside Claude Code.

## What you'll need

- **Claude Code** installed and working. (`claude.com/claude-code`)
- An **Anthropic API key** — you'll use it directly starting in week 8.
- A **GitHub account** — most weeks end with a deliverable you push.
- Your own **dev environment** — Python or TypeScript, your call. Most exercises are language-agnostic but examples lean Python.

A rhythm of "a week per week" for 12 weeks. **Hours-per-week varies a lot** based on Claude Code fluency — don't target a fixed number. A week is *done* when the deliverable is in git and you can answer the self-assessment cold.

## Install

```bash
# 1. Clone this repo (or copy the directory) into Claude's skills dir
git clone https://github.com/simonibsen/the-claudinator ~/.claude/skills/the-claudinator

# 2. Verify it's there
ls ~/.claude/skills/the-claudinator/
# Should show: SKILL.md, curriculum/, modes/, concentrations/, etc.
```

That's it. Open Claude Code in any working directory and run:

```
/the-claudinator
```

The skill appears in the `/` menu and the slash command kicks off first-run setup — a short intro, creating `~/the-claudinator/progress.md`, and offering to start week 1.

**Restart caveat:** if `~/.claude/skills/` didn't exist before you cloned this in, restart Claude Code so the skills directory gets watched. If the directory was already there, no restart needed.

After the first invocation, you can use the slash command (`/the-claudinator quiz me on week 3`) or just natural language (`"quiz me on week 3"`, `"continue"`, etc.) — Claude Code routes both back into the skill.

## What you can ask

Either via the `/the-claudinator` slash command, or in natural language once the skill is in the conversation:

| You say... | What happens |
|---|---|
| `/the-claudinator` | First-run setup, or "you're on week N, want to continue?" |
| "Teach me week 3" / "continue" | Walks you through the current/specified week |
| "Quiz me on week 4" | 10-question interactive quiz |
| "Review my work for week 5" | Senior-engineer-style code review of your deliverable |
| "Mock interview me on AI engineering" | 20-30 minute mock interview with debrief |
| "Show me capstone options" | Loads the capstone briefs |
| "Update the curriculum" | Audits the content against current Claude/MCP/API docs |

## What's in the skill

```
the-claudinator/
├── SKILL.md                     # entry point; routes by intent
├── state-template.md            # progress.md template (used on first run)
├── last-refreshed.txt           # when the content was last verified vs current docs
├── CHANGELOG.md                 # curriculum changes over time
├── curriculum/
│   ├── overview.md              # the 12-week map
│   └── week-01..12-*.md         # the weeks themselves
├── modes/
│   ├── teach.md                 # walk through a week
│   ├── quiz.md                  # interactive quiz
│   ├── critique.md              # code review your deliverable
│   ├── interview.md             # mock interview
│   ├── coach.md                 # orient / unstick / next step
│   └── update-content.md        # refresh against current docs
├── concentrations/
│   ├── ai-engineering.md        # post-curriculum AI deep dive
│   └── capstone-options.md      # capstone project briefs
├── habits.md                    # daily/weekly/monthly practices
├── reading-list.md              # canonical sources
└── INSTALL.md                   # this file
```

## What lives where

- **The skill** (`~/.claude/skills/the-claudinator/`) holds the curriculum and instructions.
- **Your progress** (`~/the-claudinator/`) is yours — your `progress.md` log, your notes, anything you accumulate. Push it to a private GitHub repo. A year of progress is portfolio + memory.

## Tuning it for yourself

Everything is markdown — edit anything that doesn't fit you.

- **Pace.** 12 weeks is the rhythm. Hours-per-week varies a lot based on your Claude Code fluency and the week — don't target a fixed number. A week is *done* when the deliverable is in git and you can answer the self-assessment cold, not when a clock has hit some number.
- **Track weighting.** Currently ~60% Claude/agents, ~25% AI engineering, ~15% SWE essentials. To rebalance, edit `curriculum/overview.md` and the relevant week files.
- **Tone.** The tutor is "strict-but-encouraging" by default. If you want softer or harder, edit the **Tone** section in `SKILL.md`.
- **Skip / reorder weeks.** Tell the skill "skip to week 6" or "I'm starting from week 4 — I've already done the earlier stuff." It will adjust.
- **Add a week.** Drop a new `week-NN-*.md` in `curriculum/` and add a row to `overview.md`. The skill picks it up automatically.

## Keeping content fresh

The curriculum references real docs, APIs, model names, and tool syntax — those change. Run:

> Update the curriculum

The skill will check the major sources (Claude Code docs, Anthropic API docs, MCP spec, Spec Kit, etc.), diff against current claims, and propose edits for you to approve. It tracks the last-refreshed date so you don't have to remember.

## One promise

The tutor is honest. If it says your deliverable is shallow, it means it. Push back if it's wrong — but the default move is to fix the work.
