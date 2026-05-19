# Module 7 — Agent SDK: Build a Standalone Agent

**Frame:** Claude Code is one agent built on top of the Claude Agent SDK. Now build your own — a custom agent that runs outside the Claude Code harness, with your own tools, system prompt, and orchestration.

**Important distinction:** the **Agent SDK** (`claude-agent-sdk` / `@anthropic-ai/claude-agent-sdk`) is a high-level wrapper that bundles the Claude Code binary and runs the agent loop *for you* — you call `query()` and iterate over messages. The lower-level **Client SDK** (`anthropic` / `@anthropic-ai/sdk`) gives you raw access to the Messages API and you write your own loop. This module is about the Agent SDK; module 8 covers the Client SDK directly.

## Objectives

1. Explain how the Claude Agent SDK relates to Claude Code (Claude Code is built on it) and how it differs from the lower-level Client SDK (`anthropic` package).
2. Build a working CLI agent using the Agent SDK's `query()` async iterator.
3. Configure the agent's tools, system prompt, and permissions.
4. Handle the things you took for granted in Claude Code: streaming output, errors, cost tracking.
5. Decide when an Agent SDK app is the right answer vs. just Claude Code vs. the lower-level Client SDK.

## Readings

- Claude Agent SDK docs at `docs.claude.com/en/api/agent-sdk/overview` (or `code.claude.com/docs/en/agent-sdk`).
- The official Python SDK repo: `github.com/anthropics/claude-agent-sdk-python`.
- The TypeScript SDK: `@anthropic-ai/claude-agent-sdk` on npm.

## Exercises

**1. Hello agent.** Install the SDK (`pip install claude-agent-sdk` or `npm install @anthropic-ai/claude-agent-sdk`). Build the smallest possible agent: one script that uses `query()` to get an answer with at least one tool available (e.g. `Read`). The SDK runs the agent loop for you — you iterate over its message stream.

**2. Pick a useful target.** What should your agent *do*? Something concrete and personal: triage your inbox, grade your homework, summarize your Strava week, monitor a long-running build, scrape a syllabus and turn it into a study schedule. Write a 1-paragraph spec.

**3. Build it.** Implement. Use the SDK's built-in tool support and add at least one custom tool of your own. Real input, real output. Push to GitHub with a README a stranger could follow.

**4. The polish pass.** Add: error handling (what if a tool fails?), streaming output (so the user sees progress), cost logging (print tokens and dollars per run), and a `--dry-run` flag.

**5. The honest tradeoff writeup.** When would Claude Code have been a better answer than your standalone agent? When wouldn't it?

## Deliverable

- A public repo: standalone agent CLI with README, install instructions, demo (asciinema or GIF)
- 3+ real runs in your terminal history
- A blog-post-quality writeup of what you built and what you learned (this can be the basis of your monthly public artifact)

## Self-assessment

1. What's the difference between the Agent SDK (`claude-agent-sdk`) and the Client SDK (`anthropic`)? When would you pick each?
2. Walk through what `query()` does internally — what loop is it running on your behalf?
3. Your agent gets stuck in a loop calling the same tool. Why might that happen, and how do you stop it?
4. Streaming vs. non-streaming — when does each make sense?
5. What's your agent's cost per run? How would you cut it in half?
6. When is a standalone agent overkill compared to Claude Code + a custom skill?

## Common pitfalls

- **Infinite loops.** Always have a max-iteration cap.
- **Silent failures.** If a tool errors, the agent needs to know — not just retry blindly.
- **No cost awareness.** Print tokens. Print dollars. Build the habit.
- **Skipping streaming.** "I'll add it later" — you won't.
- **Building Claude Code badly.** If you find yourself reimplementing Claude Code's features, ask whether you should be using Claude Code instead.

## Stretch

Deploy the agent as a cron job (GitHub Actions on a schedule, or Fly Machines). It runs without you. Send results to email or Slack.
