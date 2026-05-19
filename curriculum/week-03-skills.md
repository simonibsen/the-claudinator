# Week 3 — Skills Deep Dive

**Frame:** A skill is a contract: "when the user's intent looks like X, load this expertise into context." Get this right and the model invokes the right pattern automatically — without anyone retyping it.

## Objectives

1. Explain why model-invoked > slash-command-invoked for most expertise.
2. Write a skill `description` that triggers at the right times and not the wrong ones.
3. Design a multi-file skill that routes to sub-files instead of dumping everything in SKILL.md.
4. Distribute a skill — how it gets onto another machine, how it gets versioned.
5. Decide when *not* to write a skill (and what to write instead).

## Readings

- Anthropic's Skills documentation.
- Read the SKILL.md of at least 3 production skills (yours, this `the-claudinator` skill, and one bundled one).
- Skim Anthropic's "Engineering with Claude" posts on agentic patterns — search the blog.

## Exercises

**1. Skill anatomy reading (1 hr).** Pick 3 skills. For each, answer: when would the model load this? What's in the body? Does it route to sub-files? What scripts (if any) does it call?

**2. The description game (1 hr).** Take an existing skill. Rewrite its `description` three ways: too vague, too narrow, just right. Test each — does the model load it at the right times? This is the single most underrated skill-design skill.

**3. Build a routing skill (3 hrs).** Build a skill with: a SKILL.md (under 80 lines) that routes by intent + a `modes/` or `patterns/` subdirectory with the actual content. Topic of your choice — something you'd actually use. Verify the model picks the right sub-file based on phrasing.

**4. Distribution (1 hr).** Put your skill in a git repo. Write the README so a stranger could install it. Bonus: a one-line install command.

**5. The "don't" exercise (30 min).** Write down 3 things you almost made a skill for but shouldn't have — and what you'd write instead (a slash command? A CLAUDE.md note? A README?).

## Deliverable

- One routing skill in `~/.claude/skills/`, ≥3 sub-files, verified to load on the right phrases
- Public GitHub repo with the skill + an install README
- A short note in your study repo: "skills I considered but rejected, and why"

## Self-assessment

1. Why is the `description` more important than the body for triggering?
2. When is a custom slash command better than a skill? (Hint: who invokes it.)
3. Walk me through how your routing skill decides which sub-file to load.
4. Your skill loads when it shouldn't. What do you change?
5. Two teammates write conflicting skills with overlapping descriptions. What happens, and how do you avoid it?

## Common pitfalls

- **One giant SKILL.md.** Hard to maintain, eats context. Route.
- **Descriptions that lie.** If the body does X but the description says Y, the model will load it for Y and then do X badly.
- **Skills for one-off tasks.** A skill is for *patterns*. A one-off prompt belongs in a slash command or just typed.

## Stretch

Build a "meta-skill": a skill that helps you author new skills. The recursion is the point — and shows you understand the pattern.
