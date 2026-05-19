# Week 4 — Subagents & Multi-Agent Orchestration

**Frame:** A subagent is a fresh context running independently. Used well: parallelism, context isolation, specialized expertise. Used poorly: token bonfire that produces nothing.

## Objectives

1. Explain when a subagent saves context vs. when it wastes it.
2. Define custom subagents in `.claude/agents/` with tight system prompts and minimal tool allowlists.
3. Run a multi-agent workflow: plan → fan-out → review.
4. Brief a subagent well (the prompt-as-ticket pattern).
5. Recognize when a multi-agent pattern is overengineering.

## Readings

- The subagents section of the Claude Code docs.
- Anthropic's posts on multi-agent patterns (search the blog for "multi-agent" or "orchestrator").
- Skim 2-3 public `.claude/agents/` directories on GitHub (search `path:.claude/agents`).

## Exercises

**1. Subagent triage drill (1 hr).** Take 10 recent tasks you did. For each, decide: should this have been a subagent? Why or why not? Build intuition for the trade-off.

**2. Custom agent (2 hrs).** Define `.claude/agents/code-reviewer.md` (or `homework-grader`, `paper-summarizer`, `bug-reporter` — pick one you'd actually use). Tight system prompt. Read-only tool allowlist if it's review-focused.

**3. The fan-out (3 hrs).** Pick a task that has independent sub-problems (e.g., "find every place we handle errors inconsistently across these 8 files"). Use a Plan subagent to enumerate, then spawn parallel Explore subagents — one per file. Compare results.

**4. Plan → Implement → Review (3 hrs).** Build a small feature using three subagents in sequence: one designs, one implements, one critiques. Note where the handoff is awkward — that's where prompting matters.

**5. The anti-exercise (1 hr).** Pick a task and *deliberately* over-architect it with subagents. Run it. Notice how much slower and more expensive it is than just doing it. Internalize.

## Deliverable

- 2 custom agents in `.claude/agents/`, with documented system prompts
- A short writeup (`week-04.md` in your study repo): one task where multi-agent helped, one where it hurt, what you'd do differently
- A "subagent brief template" — the format you'll use to spec a subagent task

## Self-assessment

1. When does a subagent save your main context? Give two cases.
2. Why does giving a reviewer subagent write tools defeat the purpose?
3. What's the "prompt-as-ticket" pattern, and what does a bad ticket look like?
4. Three Explore subagents return contradictory answers. What do you do?
5. Your fan-out used 6 subagents. Was that the right number? How would you tell?

## Common pitfalls

- **Reflexive fan-out.** "Just spawn 5 agents" is not a strategy. Ask: are these truly independent?
- **Vague briefs.** Subagents don't see your conversation — every prompt must be self-contained.
- **No verification.** A subagent's report tells you what it *intended*. Always check the actual artifacts.
- **Subagents inside subagents.** Possible, but usually a smell. Flatten when you can.

## Stretch

Write a "code-review-agent" that takes a PR URL and returns a structured review. Compare its review to a human review of the same PR. What did each miss?
