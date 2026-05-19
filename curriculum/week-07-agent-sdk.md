# Week 7 — Agent SDK: Build a Standalone Agent

**Frame:** Claude Code is one agent built on the platform. Now build your own — a custom agent that runs without the Claude Code harness, with your own tools, system prompt, and control loop.

## Objectives

1. Explain how the Claude Agent SDK relates to Claude Code (Claude Code is built on it).
2. Build a working CLI agent that uses tools and produces useful output.
3. Implement the agent loop: model call → tool call → tool result → model call.
4. Handle the things you took for granted in Claude Code: streaming, errors, retries, cost.
5. Decide when an Agent SDK app is the right answer vs. just Claude Code.

## Readings

- Claude Agent SDK docs at `claude.com/claude-code/docs` (or Anthropic API docs).
- One reference Agent SDK project on GitHub.
- Read `anthropic-cookbook` examples for tool use, if available.

## Exercises

**1. Hello agent (1.5 hrs).** Build the smallest possible agent: one Python script, one tool (e.g. `read_file`), a loop that takes a user prompt and runs to completion. Make it work end to end.

**2. Pick a useful target (30 min).** What should your agent *do*? Something concrete and personal: triage your inbox, grade your homework, summarize your Strava week, monitor a long-running build, scrape a syllabus and turn it into a study schedule. Write a 1-paragraph spec.

**3. Build it (4-5 hrs).** Implement. Three tools minimum. Real input, real output. Push to GitHub with a README a stranger could follow.

**4. The polish pass (2 hrs).** Add: error handling (what if a tool fails?), streaming output (so the user sees progress), cost logging (print tokens and dollars per run), and a `--dry-run` flag.

**5. The honest tradeoff writeup (30 min).** When would Claude Code have been a better answer than your standalone agent? When wouldn't it?

## Deliverable

- A public repo: standalone agent CLI with README, install instructions, demo (asciinema or GIF)
- 3+ real runs in your terminal history
- A blog-post-quality writeup of what you built and what you learned (this can be the basis of your monthly public artifact)

## Self-assessment

1. Walk through one iteration of the agent loop with a concrete example.
2. Your agent gets stuck in a loop calling the same tool. Why might that happen, and how do you stop it?
3. Streaming vs. non-streaming — when does each make sense?
4. What's your agent's cost per run? How would you cut it in half?
5. When is a standalone agent overkill compared to Claude Code + a custom skill?

## Common pitfalls

- **Infinite loops.** Always have a max-iteration cap.
- **Silent failures.** If a tool errors, the agent needs to know — not just retry blindly.
- **No cost awareness.** Print tokens. Print dollars. Build the habit.
- **Skipping streaming.** "I'll add it later" — you won't.
- **Building Claude Code badly.** If you find yourself reimplementing Claude Code's features, ask whether you should be using Claude Code instead.

## Stretch

Deploy the agent as a cron job (GitHub Actions on a schedule, or Fly Machines). It runs without you. Send results to email or Slack.
