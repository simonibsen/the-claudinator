# Week 3 — Skills Deep Dive

**Frame:** A skill is a unit of packaged expertise that becomes a slash command. The directory name becomes the command (`my-skill/` → `/my-skill`), and the `description` in frontmatter tells Claude when to load it automatically. Both invocation paths — user-typed slash command and model-auto-invocation from description — work simultaneously.

**Important: custom commands have been merged into skills.** A file at `.claude/commands/deploy.md` and a skill at `.claude/skills/deploy/SKILL.md` both create `/deploy` and work the same way. Old `.claude/commands/` files still work; skills add features (supporting files, frontmatter for invocation control, model auto-load).

## Objectives

1. Explain how skills are invoked: both `/skill-name` slash command and model-auto-invocation from description.
2. Write a skill `description` that triggers at the right times and not the wrong ones.
3. Design a multi-file skill that routes to sub-files instead of dumping everything in SKILL.md.
4. Use frontmatter controls: `disable-model-invocation` (manual-only), `user-invocable: false` (Claude-only), `allowed-tools` (pre-approve tools).
5. Distribute a skill — how it gets onto another machine, how it gets versioned.
6. Decide when *not* to write a skill (and what to write instead).

## Readings

- The skills documentation at `code.claude.com/docs/en/skills`.
- Read the SKILL.md of at least 3 production skills (yours, this `the-claudinator` skill, and one bundled skill like `/simplify`, `/debug`, `/loop`, or `/claude-api`).
- Skim Anthropic's "Engineering with Claude" posts on agentic patterns — search the blog.

## Frontmatter you should know

All fields are optional. `description` is recommended so Claude knows when to load it; `name` defaults to the directory name.

| Field | Purpose |
|---|---|
| `description` | When Claude should auto-invoke (recommended) |
| `name` | Display name (defaults to dir name) |
| `disable-model-invocation: true` | Only you can invoke (via `/`) — Claude won't auto-load |
| `user-invocable: false` | Only Claude can invoke — hides from `/` menu |
| `allowed-tools` | Pre-approve tools when the skill is active |
| `argument-hint` / `arguments` | Named positional args for `$ARGUMENTS` substitution |
| `context: fork` + `agent: <type>` | Run the skill in a forked subagent |

## Exercises

**1. Skill anatomy reading.** Pick 3 skills. For each, answer: when would the model load this? What's in the body? Does it route to sub-files? What scripts (if any) does it call?

**2. The description game.** Take an existing skill. Rewrite its `description` three ways: too vague, too narrow, just right. Test each — does the model load it at the right times? This is the single most underrated skill-design skill.

**3. Build a routing skill.** Build a skill with: a SKILL.md (under 80 lines) that routes by intent + a `modes/` or `patterns/` subdirectory with the actual content. Topic of your choice — something you'd actually use. Verify the model picks the right sub-file based on phrasing.

**4. Distribution.** Put your skill in a git repo. Write the README so a stranger could install it. Bonus: a one-line install command.

**5. The "don't" exercise.** Write down 3 things you almost made a skill for but shouldn't have — and what you'd write instead (a slash command? A CLAUDE.md note? A README?).

## Deliverable

- One routing skill in `~/.claude/skills/`, ≥3 sub-files, verified to load on the right phrases
- Public GitHub repo with the skill + an install README
- A short note in your study repo: "skills I considered but rejected, and why"

## Self-assessment

1. Why is the `description` more important than the body for triggering?
2. What's the relationship between `.claude/commands/deploy.md` and `.claude/skills/deploy/SKILL.md`? When would you use each?
3. Walk me through how your routing skill decides which sub-file to load.
4. Your skill loads when it shouldn't. What do you change?
5. Two teammates write conflicting skills with overlapping descriptions. What happens, and how do you avoid it?
6. Name the four frontmatter fields you'd use to: (a) prevent Claude from auto-invoking, (b) hide from the `/` menu, (c) pre-approve some tools, (d) run the skill in a forked subagent.

## Common pitfalls

- **One giant SKILL.md.** Hard to maintain, eats context. Route.
- **Descriptions that lie.** If the body does X but the description says Y, the model will load it for Y and then do X badly.
- **Skills for one-off tasks.** A skill is for *patterns*. A one-off prompt belongs in a slash command or just typed.

## Stretch

Build a "meta-skill": a skill that helps you author new skills. The recursion is the point — and shows you understand the pattern.
