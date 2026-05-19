# Week 2 — Customization & Hooks + Git at Team Scale

**Frame:** Productivity scaffolding — the investments that pay you back daily for the next year. Plus the git workflow that real teams use.

By the end of this week, your `~/.claude/` directory should look meaningfully different from when you started. Settings deliberately set, at least one hook running, 2-3 custom slash commands for tasks you actually do. *That's* the productivity playbook — code, not prose.

## Objectives

1. Configure `settings.json` (user + project) deliberately, with a written reason for each setting.
2. Write at least one hook that catches a class of mistakes you've made.
3. Write 2-3 custom slash commands for tasks you do weekly.
4. Open a PR on an OSS project, navigate review, and merge it.
5. Use `git bisect` to find a regression in a real repo.

## Readings

- `claude.com/claude-code/docs/settings` and the hooks section.
- `git-scm.com/book` Ch 3 (branching) and Ch 7 (rebasing, bisect, reflog).
- "How to write a good PR description" (search; multiple good posts exist — pick one).
- One open-source project's `CONTRIBUTING.md`.

## Exercises

**1. Settings audit (1 hr).** Open `~/.claude/settings.json`. Document each key with a comment explaining why. Add `permissions.allow` entries for tools you use without prompts and `permissions.deny` for anything you never want auto-run.

**2. Hooks (2 hrs).** Write a `PostToolUse` hook that runs your linter or formatter after Edit/Write. Test it by editing a file and watching it run. Write a `Stop` hook that reminds you to commit if you've made >5 edits.

**3. Custom slash commands (2 hrs).** Add 2-3 commands in `.claude/commands/` for repeated workflows — examples: `/test` (run your test suite with a useful flag set), `/review` (have the model critique the current diff), `/prep-pr` (summarize staged changes as a PR description with test plan). Pick ones for workflows *you actually did this week*, not hypotheticals.

**4. The OSS PR (3 hrs).** Find a project you actually use. Look at their issue tracker for `good-first-issue` or a typo/docs bug. Open the PR. Respond to review feedback. Get it merged.

**5. Bisect drill (1 hr).** In any repo with a non-trivial history, intentionally introduce a bug 10 commits back (or pick a known-fixed bug), then `git bisect` your way to it.

## Deliverable

- `~/.claude/settings.json` checked into a dotfiles repo, with comments
- At least one custom hook running on your main project
- A merged PR (URL in `progress.md`)
- A short writeup (`week-02.md` in your study repo) of what your hooks do and why

## Self-assessment

1. What's the difference between `PreToolUse` and `PostToolUse`? Give one good use case for each.
2. When would you use a project-level `.claude/settings.json` vs. user-level?
3. What does `git rebase -i` do, and when would you (carefully) use it?
4. After your PR got review comments, how did you handle them — new commits, amend, or rebase? Why?
5. What's the difference between `merge` and `rebase` workflows, and which does the project you contributed to use?

## Common pitfalls

- **Hooks that block the agent unnecessarily.** Slow hooks make the tool painful. Time-box and short-circuit.
- **Force-pushing to a shared branch.** Don't. Practice on your own forks.
- **Treating PR review as adversarial.** It's not. The reviewer is helping. Thank them and address the feedback.

## Stretch

Set up `pre-commit` hooks (the Python tool) on your project — lint + typecheck + tests on every commit. Make them fast.
