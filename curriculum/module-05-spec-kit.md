# Module 5 — Spec Kit + Design Docs

**Frame:** The best engineers write before they code. Spec Kit operationalizes spec-driven development for AI-assisted work; design docs do the same thing for humans. Both teach the same underlying discipline.

## Objectives

1. Explain the Spec Kit flow (`/speckit.specify` → `/speckit.plan` → `/speckit.tasks` → `/speckit.implement`) and when each phase matters. Know the supporting commands (`/speckit.constitution`, `/speckit.clarify`, `/speckit.analyze`, `/speckit.checklist`, `/speckit.taskstoissues`).
2. Build one non-trivial feature entirely spec-first via Spec Kit.
3. Read 3 real-world RFCs/design docs and identify the shared structure.
4. Write a design doc for a feature, get feedback on it, and revise.
5. Decide when *not* to write a spec.

## Readings

- `github.com/github/spec-kit` README + quickstart.
- Rust RFC #2113 (async/await) and Oxide RFD 1 (the RFD process itself).
- "Scaling Engineering Teams via Writing Things Down" (Will Larson) — search; widely cited.
- Skim one ADR (Architecture Decision Record) example.

## Exercises

**1. Spec Kit install + tour.** Install with:

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

Run the quickstart. Spec Kit installs as `/speckit.*` slash commands inside Claude Code. Look at what each phase outputs:
- `/speckit.constitution` → `.specify/memory/constitution.md` (project principles)
- `/speckit.specify` → `specs/[feature-id]/spec.md` (requirements + user stories)
- `/speckit.plan` → technical implementation details (data models, API specs, research)
- `/speckit.tasks` → `tasks.md` (ordered, dependency-aware task breakdown)
- `/speckit.implement` → executes the tasks

**2. The Spec-First Feature.** Pick a feature worth 1-2 days of work — non-trivial. Use Spec Kit end-to-end via the `/speckit.*` commands. Commit spec, plan, tasks, and implementation. The spec/plan files should be readable by a stranger.

**3. RFC reading.** Read the three docs from the readings. For each: (a) how is the problem framed? (b) what alternatives are considered? (c) what's the decision criterion? (d) what's left unspecified and why?

**4. Write your own.** Pick a real change to one of your projects (auth, caching, schema migration — something with trade-offs). Write a 1-2 page design doc: Problem / Goals / Non-Goals / Proposal / Alternatives / Risks / Rollout. Commit it to the repo.

**5. Get feedback.** Share the doc — with a peer, a TA, or run it through this skill's `critique` mode. Take notes. Revise. The git history should show the revision.

**6. The constitution exercise.** A spec answers "what should this feature do." A constitution answers "what does this project value when those answers conflict." Run `/speckit.constitution` to seed one for a project of yours.

Constraints (this is where most people fail):
- **5-10 principles, no more.** Long constitutions get ignored.
- **Each principle has to be specific enough to disagree with.** *"We write good code"* is meaningless. *"We prefer obvious code over clever code, even when the obvious version is longer"* is a real principle.
- **Each principle has a trade-off.** If accepting it doesn't cost you anything, it's a platitude. *"We prioritize correctness over speed"* says nothing if no one cares about speed. *"We prioritize correctness over speed of merging — fast PRs that get reverted twice are slower than careful ones"* is a real claim.

Look at examples first: the Rust language's design principles, the Oxide product principles, or any open-source project with a stated philosophy doc. Notice what makes them load-bearing vs. decorative. Then commit yours as `.specify/memory/constitution.md`.

**7. The iteration exercise — when the spec is wrong.** This is the realistic case. Pure waterfall ("spec is right, implement, done") never happens. Implementation always reveals something — a constraint that was unrealistic, a goal that was vague, a "non-goal" that turns out to be necessary.

Take the feature you built in exercise 2. Force the loop:
- **Identify one place** where the spec was wrong (or pick a new place — there's usually one).
- **Update the spec first** (not the code). Edit `specs/[feature-id]/spec.md` to reflect the new understanding. Commit the change with a message explaining what implementation revealed.
- **Re-run `/speckit.plan`** to regenerate the plan. Diff against the old plan. Notice what changed.
- **Decide:** does this require new tasks, or just edits to existing ones?
- **Re-derive tasks** if needed, then implement the delta.
- **Self-check:** would a stranger reading the spec + git history understand both the original intent *and* what changed about it?

This is the spec-as-living-document discipline. The point of the spec isn't to be right the first time — it's to give you something concrete to update when reality pushes back.

## Deliverable

- A repo with a feature built via Spec Kit, with spec/plan/tasks committed
- A design doc (`docs/rfc-001-*.md`) with at least one round of visible revision
- A `.specify/memory/constitution.md` with 5-10 disagree-able principles
- The git history shows at least one spec revision driven by implementation feedback

## Self-assessment

1. When is Spec Kit overkill? When is ad-hoc prompting better?
2. What goes in "Non-Goals" and why is that often the most important section?
3. How is plan mode in Claude Code different from Spec Kit's `/speckit.plan`?
4. After feedback, what changed in your doc? What didn't change, and why?
5. A skeptical reader reads your doc. What's the first objection they'd raise?
6. Read me one of your constitution principles and tell me the trade-off it expresses. If you can't name what it's trading off, the principle isn't load-bearing yet.
7. Walk me through your spec-revision episode: what did implementation reveal, what did you change in the spec, and how did the downstream artifacts (plan, tasks) react?

## Common pitfalls

- **Specs for trivial work.** Don't write an RFC for a typo. Judgement of *when* to spec is half the skill.
- **Strawmanned alternatives.** "Option B: do nothing" doesn't count.
- **Decorative specs.** If you wrote the spec and ignored it during implementation, you wasted the spec.
- **Vague goals.** "Make it fast" is not a goal. "P95 latency under 200ms for the search endpoint" is.

## Stretch

Find an open RFC in a project you care about. Read it, then write a substantive comment. This is how senior engineers signal their thinking publicly.
