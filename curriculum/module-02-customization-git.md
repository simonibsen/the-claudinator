# Module 2 — Customization & Hooks + Git at Team Scale

**Frame:** Productivity scaffolding — the investments that pay you back daily for the next year. Plus the git workflow that real teams use.

By the end of this module, your `~/.claude/` directory should look meaningfully different from when you started. Settings deliberately set, at least one hook running, 2-3 custom slash commands for tasks you actually do. *That's* the productivity playbook — code, not prose.

## Objectives

1. Configure `settings.json` (user + project + project-local) deliberately, with a written reason for each setting.
2. Understand the permissions system: rule syntax (`Bash(git *)`, `Skill(name *)`, `mcp__server__.*`), the four scopes, and conditional permissions in hooks. **Note:** pipe-OR (`Edit|Write`) is **hook matcher** syntax, not permission rule syntax — permissions take one entry per tool.
3. Write at least one hook that catches a class of mistakes you've made. Know the **complete event list** (not just `PreToolUse`/`PostToolUse`/`Stop`).
4. Write 2-3 custom slash commands for tasks you do weekly.
5. Open a PR on an OSS project, navigate review, and merge it.
6. Use `git bisect` to find a regression in a real repo.

## Readings

- `code.claude.com/docs/en/settings` and `code.claude.com/docs/en/hooks` — the full hook event list and matcher syntax.
- `code.claude.com/docs/en/permissions` — rule syntax, four scopes, conditional rules.
- `git-scm.com/book` Ch 3 (branching) and Ch 7 (rebasing, bisect, reflog).
- "How to write a good PR description" (search; multiple good posts exist — pick one).
- One open-source project's `CONTRIBUTING.md`.

## Exercises

**1. Settings audit.** Open `~/.claude/settings.json`. Document each key with a comment explaining why. Set up the four scopes appropriately:

- `~/.claude/settings.json` — your personal defaults across all projects
- `.claude/settings.json` — project defaults (shared, committed)
- `.claude/settings.local.json` — your personal project overrides (gitignored)
- Managed (enterprise) — set by your org, top priority

**2. Permissions deep-dive.** The `permissions.allow` and `permissions.deny` fields take rule strings, not just tool names. Practice writing rules:

- `Bash(git *)` — allow any git command via Bash
- `Bash(rm *)` — deny anything that looks like an rm
- `Edit` — allow Edit (separate entry from Write — permissions don't take pipe-OR)
- `Write` — allow Write
- `Skill(deploy *)` — allow the deploy skill (and any args)
- `mcp__memory__.*` — match all tools from one MCP server
- `WebFetch(domain:docs.anthropic.com)` — domain-scoped matchers (where supported)

**Watch out:** pipe-OR (`Edit|Write`) is hook **matcher** syntax (matches multiple tool names in one hook), not permission rule syntax. Mixing the two is a common new-user mistake — Claude will silently treat `Edit|Write` as an unknown tool name rather than as "Edit or Write."

Write 5 allow rules and 3 deny rules for your own daily workflow. Commit to your dotfiles.

**3. Hooks.** Write a `PostToolUse` hook that runs your linter or formatter after Edit/Write. Test it by editing a file and watching it run. Write a `Stop` hook that reminds you to commit if you've made >5 edits.

**Awareness — the broader event list.** Beyond `PreToolUse`/`PostToolUse`/`Stop`, Claude Code supports many more hook events. Skim the list and pick one less-obvious event to experiment with:

- Session lifecycle: `SessionStart`, `SessionEnd`, `Setup`
- Prompt flow: `UserPromptSubmit`, `UserPromptExpansion`, `MessageDisplay`
- Tools: `PreToolUse`, `PermissionRequest`, `PermissionDenied`, `PostToolUse`, `PostToolUseFailure`, `PostToolBatch`
- Agents: `SubagentStart`, `SubagentStop`, `TaskCreated`, `TaskCompleted`
- Context: `PreCompact`, `PostCompact`, `InstructionsLoaded`, `ConfigChange`, `CwdChanged`, `FileChanged`
- Worktrees: `WorktreeCreate`, `WorktreeRemove`
- MCP: `Elicitation`, `ElicitationResult`
- Other: `Notification`, `Stop`, `StopFailure`, `TeammateIdle`

Hooks take handler types: `command` (shell), `http` (POST JSON), `mcp_tool`, `prompt` (model decision), `agent` (subagent verification). Don't try to use them all — just know they exist.

**3. Custom slash commands.** Add 2-3 commands in `.claude/commands/` for repeated workflows — examples: `/test` (run your test suite with a useful flag set), `/prep-pr` (summarize staged changes as a PR description with test plan). Pick ones for workflows *you actually did this module*, not hypotheticals. **Before you write `/review`-style commands, check the bundled ones:** `/code-review`, `/code-review --fix`, and `/simplify` are shipped and battle-tested. Don't reinvent — write thin wrappers if you want project-specific defaults.

**4. The OSS PR.** Find a project you actually use. Look at their issue tracker for `good-first-issue` or a typo/docs bug. Open the PR. Respond to review feedback. Get it merged.

**5. Bisect drill.** In any repo with a non-trivial history, intentionally introduce a bug 10 commits back (or pick a known-fixed bug), then `git bisect` your way to it.

## Deliverable

- `~/.claude/settings.json` checked into a dotfiles repo, with comments
- At least one custom hook running on your main project
- A merged PR (URL in `progress.md`)
- A short writeup (`module-02.md` in your study repo) of what your hooks do and why

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
