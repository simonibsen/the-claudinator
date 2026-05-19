# Module 4 — Subagents, Agent Teams & Multi-Agent Orchestration

**Frame:** A subagent is a fresh context running independently. Used well: parallelism, context isolation, specialized expertise. Used poorly: token bonfire that produces nothing.

**Three related concepts the docs distinguish:**
- **Subagents** — spawned in-session via the `Agent` tool, run with isolated context, return results to the main thread. The focus of this module.
- **Agent teams** — multiple agents running simultaneously on different parts of a task, with a lead agent coordinating. Built on subagents but framed as a team pattern.
- **Background agents** — independent parallel sessions you can view side-by-side (see `/en/agent-view`). Useful when you want multiple long-running tasks visible at once.

You'll focus on subagents this module; the other two are good to be aware of and try once.

## Objectives

1. Explain when a subagent saves context vs. when it wastes it.
2. Define custom subagents in `.claude/agents/<name>.md` with **`name` + `description` required** in frontmatter, plus system prompt and tool allowlist (`tools:` field).
3. Know that **subagents are loaded at session start** — adding a new one via file edit requires restarting; using `/agents` to create one takes effect immediately.
4. Know that **subagents cannot spawn subagents** — only the main thread can. If you need recursion-like behavior, plan it at the main level.
5. Run a multi-agent workflow: plan → fan-out → review.
6. Brief a subagent well (the prompt-as-ticket pattern).
7. Recognize when a multi-agent pattern is overengineering.

## Readings

- The subagents docs at `code.claude.com/docs/en/sub-agents`.
- Background agents / agent-view docs (for awareness): `code.claude.com/docs/en/agent-view`.
- Anthropic's posts on multi-agent patterns (search the blog for "multi-agent" or "orchestrator").
- Skim 2-3 public `.claude/agents/` directories on GitHub (search `path:.claude/agents`).

## Exercises

**1. Subagent triage drill.** Take 10 recent tasks you did. For each, decide: should this have been a subagent? Why or why not? Build intuition for the trade-off.

**2. Custom agent.** Define `.claude/agents/code-reviewer.md` (or `homework-grader`, `paper-summarizer`, `bug-reporter` — pick one you'd actually use). Required frontmatter: `name` + `description`. Tight system prompt. Read-only `tools:` allowlist if it's review-focused. Create it via `/agents` if you want it loaded without restarting.

**3. The fan-out.** Pick a task that has independent sub-problems (e.g., "find every place we handle errors inconsistently across these 8 files"). Use a Plan subagent to enumerate, then spawn parallel Explore subagents — one per file. Compare results.

**4. Plan → Implement → Review.** Build a small feature using three subagents in sequence: one designs, one implements, one critiques. Note where the handoff is awkward — that's where prompting matters.

**5. The anti-exercise.** Pick a task and *deliberately* over-architect it with subagents. Run it. Notice how much slower and more expensive it is than just doing it. Internalize.

## Deliverable

- 2 custom agents in `.claude/agents/`, with documented system prompts
- A short writeup (`module-04.md` in your study repo): one task where multi-agent helped, one where it hurt, what you'd do differently
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
- **Trying to spawn subagents from inside a subagent.** Not possible — only the main thread can spawn subagents. If you need that pattern, flatten the plan at the main level.
- **Forgetting the restart rule.** File-edited subagent definitions don't take effect until session restart; `/agents`-created ones do. If your new agent isn't showing up, that's why.

## Stretch

Write a "code-review-agent" that takes a PR URL and returns a structured review. Compare its review to a human review of the same PR. What did each miss?

## Sidebar — orchestrating local-LLM workers (preview)

This module's pattern is Claude orchestrating *Claude subagents* — smart and expensive workers. The same architecture works with *local LLMs* as the workers — dumb and free. Useful when you have a large batch of medium-difficulty items where Claude-on-everything is overkill and a regex isn't enough.

Full pattern (the *orchestrator pattern*) is in `concentrations/local-llms.md` section 5, after the curriculum. Worth knowing it exists before you encounter a "I need to process 5,000 of these" problem and reflexively reach for Claude.
