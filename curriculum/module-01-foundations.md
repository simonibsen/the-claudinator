# Module 1 — Daily-Driver Fluency + Reading Codebases

**Frame:** The moves that pay off Monday. Claude Code as your daily driver — and reading unfamiliar codebases (with Claude's help, not in spite of it).

**Productivity through-line starts here.** Across the next 12 modules, productively using Claude Code is *how* you do everything else. This module sets the foundation: the keyboard moves, the workflow patterns, the daily reflexes. The advanced topics later (skills, agents, MCP) only make sense after you've felt the friction this module's tools don't yet solve.

## Objectives

1. Use Claude Code for every change to one repo for the duration of this module, including commits.
2. Know plan mode, `!` bash prefix, `#` memory shortcut, `/` slash commands cold.
3. Write a CLAUDE.md that another developer (or you in 3 months) could pick up.
4. Navigate an unfamiliar mid-size codebase and produce a 1-page architecture summary.

## Readings

- `code.claude.com/docs/en/overview` — Getting Started + Common Workflows.
- `code.claude.com/docs/en/memory` — what CLAUDE.md actually does (project, user, nested, imports).
- `code.claude.com/docs/en/settings` — the settings model.
- Skim one mid-size OSS Python or TypeScript repo's top-level README + main entrypoint (e.g. `pallets/flask`, `tiangolo/fastapi`, `astral-sh/ruff`).

## Exercises

**1. Install + tour.** Install Claude Code. Run `/help`. Try plan mode (`shift+tab`). Try `!ls` and `# remember to use uv for installs`. Read your own keybindings via `/keybindings`.

**2. The Real-Repo Run.** Pick a personal repo (a class project works). Make every change for the module via Claude Code. After each session, commit. Tally: where did the tool save time? Where did it fight you?

**3. The Codebase Map.** Pick an OSS project you've used. Without reading any tutorials, navigate it and write `MAP.md`: what are the top 5 modules, what's the entrypoint, where does a request/command flow through, what's surprising? Use Claude Code to help you explore — but you write the doc.

**4. Productivity recipes.** Try at least 3 of these workflows during the module — they're patterns that pay off daily:
- **Bulk refactor.** "Rename X to Y across the codebase, update all imports." Verify the diff before accepting.
- **Codebase archaeology.** "Why does this function exist? Trace back when it was added and what problem it solved."
- **PR prep.** "Summarize my staged changes as a PR description, including a test plan."
- **Bug archaeology.** "I have this stack trace. Find the most likely cause and the file I should look at first."
- **Test scaffolding.** "Generate a pytest file for `module.py` with cases for happy path + 3 edge cases I'd likely miss."
- **Doc generation.** "Write docstrings for all public functions in this file based on what they actually do."

## Deliverable

A repo with:
- A real `CLAUDE.md` (project-level)
- At least 5 commits made via Claude Code during this module
- The `MAP.md` for an OSS project (can live in the same repo or a gist)

## Self-assessment

1. What does `CLAUDE.md` do that the system prompt doesn't?
2. When would you use plan mode vs. just going?
3. How do you get the model to run a shell command without leaving the prompt?
4. What's the difference between user-level and project-level settings?
5. In the OSS project you mapped: name the entrypoint, the data flow for one common operation, and one thing you found confusing.

## Common pitfalls

- **Reading tutorials instead of docs.** The Anthropic docs are the source of truth; YouTube tutorials go stale fast.
- **Using Claude for trivial single-character edits.** That's a fight with the tool. Reserve it for actual changes.
- **Writing a generic CLAUDE.md** ("This is a Python project. Use clean code."). Useless. Write the specific things that aren't obvious from the repo.

## Stretch

Set up Claude Code on a second machine and sync your `~/.claude/settings.json` via dotfiles. (Future modules reward having dotfiles already.)
