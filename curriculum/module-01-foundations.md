# Module 1 — Daily-Driver Fluency + Reading Codebases

**Frame:** The moves that pay off Monday. Claude Code as your daily driver — and reading unfamiliar codebases (with Claude's help, not in spite of it).

**Productivity through-line starts here.** Across the next 12 modules, productively using Claude Code is *how* you do everything else. This module sets the foundation: the keyboard moves, the workflow patterns, the daily reflexes. The advanced topics later (skills, agents, MCP) only make sense after you've felt the friction this module's tools don't yet solve.

## Objectives

1. Use Claude Code for every change to one repo for the duration of this module, including commits.
2. Know the permission-mode cycle (`shift+tab`), `!` bash prefix, `@` file mention, `/` slash commands cold.
3. Understand the two parallel memory mechanisms: **CLAUDE.md** (instructions you write, loaded into every session) and **auto memory** (learnings Claude writes to `~/.claude/projects/<project>/memory/` and reloads next session). Know which belongs where.
4. Write a CLAUDE.md that another developer (or you in 3 months) could pick up.
5. Navigate an unfamiliar mid-size codebase and produce a 1-page architecture summary.

## Readings

- `code.claude.com/docs/en/overview` — Getting Started + Common Workflows.
- `code.claude.com/docs/en/memory` — both surfaces: CLAUDE.md (project / user / nested / imports) *and* auto memory (the `~/.claude/projects/<project>/memory/` directory Claude writes to itself). Read the `#auto-memory` section carefully — it's not in older Claude Code docs and behaves differently from CLAUDE.md.
- `code.claude.com/docs/en/settings` — the settings model.
- `code.claude.com/docs/en/interactive-mode` — the actual list of quick-command prefixes (`/`, `!`, `@`) and what `shift+tab` does.
- Skim one mid-size OSS Python or TypeScript repo's top-level README + main entrypoint (e.g. `pallets/flask`, `tiangolo/fastapi`, `astral-sh/ruff`).

## Exercises

**1. Install + tour.** Install Claude Code. Run `/help`. Press `shift+tab` and watch the mode indicator — it **cycles permission modes** (`default` → `acceptEdits` → `plan` plus any custom ones you've enabled), not "toggle plan mode." Try `!ls` (shell-prefix), `@some-file.txt` (file mention), and `/keybindings` (your bindings).

**2. The memory split.** Ask Claude to "remember we use uv for installs in this repo." Then run `/memory` to inspect what got written. You should find an auto-memory file under `~/.claude/projects/<project>/memory/` indexed by `MEMORY.md` — *not* an append to CLAUDE.md. Now write a line to CLAUDE.md *yourself* (any convention). Both load next session; only one of them was Claude-written. Internalize the split:

- **CLAUDE.md** = instructions you write deliberately (conventions, style, "always do X").
- **Auto memory** = learnings Claude writes from your conversations (typed `feedback` / `user` / `project` / `reference`, with a `MEMORY.md` index).

Tinker with the controls: `/memory` (view/edit), the `autoMemoryEnabled` setting (toggle), `CLAUDE_CODE_DISABLE_AUTO_MEMORY=1` (env-var disable), `autoMemoryDirectory` (relocate). When CLAUDE.md grows past ~200 lines, split it: put per-topic files in `.claude/rules/` with `paths:` frontmatter to scope which directories load each rule. (Avoids loading frontend rules in a backend session.)

**3. The Real-Repo Run.** Pick a personal repo (a class project works). Make every change for the module via Claude Code. After each session, commit. Tally: where did the tool save time? Where did it fight you?

**4. The Codebase Map.** Pick an OSS project you've used. Without reading any tutorials, navigate it and write `MAP.md`: what are the top 5 modules, what's the entrypoint, where does a request/command flow through, what's surprising? Use Claude Code to help you explore — but you write the doc.

**5. Productivity recipes.** Try at least 3 of these workflows during the module — they're patterns that pay off daily:
- **Bulk refactor.** "Rename X to Y across the codebase, update all imports." Verify the diff before accepting.
- **Codebase archaeology.** "Why does this function exist? Trace back when it was added and what problem it solved."
- **PR prep.** "Summarize my staged changes as a PR description, including a test plan."
- **Bug archaeology.** "I have this stack trace. Find the most likely cause and the file I should look at first."
- **Test scaffolding.** "Generate a pytest file for `module.py` with cases for happy path + 3 edge cases I'd likely miss."
- **Doc generation.** "Write docstrings for all public functions in this file based on what they actually do."
- **Verify behavior, not just tests.** `/verify` builds and runs your app and checks it actually does what you said. `/run-skill-generator` records the launch recipe (commands, env vars, ports) as a reusable project skill — so the next session can run the app without re-discovering how.

## Deliverable

A repo with:
- A real `CLAUDE.md` (project-level)
- At least 5 commits made via Claude Code during this module
- The `MAP.md` for an OSS project (can live in the same repo or a gist)

## Self-assessment

1. What does `CLAUDE.md` do that the system prompt doesn't?
2. What's the difference between `CLAUDE.md` and **auto memory** — who writes each, what each is for, where each lives, and when each loads?
3. What does `shift+tab` do? (Hint: it's not "toggle plan mode.")
4. When would you use plan mode vs. just going?
5. How do you get the model to run a shell command without leaving the prompt?
6. What's the difference between user-level and project-level settings?
7. In the OSS project you mapped: name the entrypoint, the data flow for one common operation, and one thing you found confusing.

## Common pitfalls

- **Reading tutorials instead of docs.** The Anthropic docs are the source of truth; YouTube tutorials go stale fast.
- **Using Claude for trivial single-character edits.** That's a fight with the tool. Reserve it for actual changes.
- **Writing a generic CLAUDE.md** ("This is a Python project. Use clean code."). Useless. Write the specific things that aren't obvious from the repo.

## Stretch

Set up Claude Code on a second machine and sync your `~/.claude/settings.json` via dotfiles. (Future modules reward having dotfiles already.)
