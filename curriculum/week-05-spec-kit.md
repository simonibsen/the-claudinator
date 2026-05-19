# Week 5 — Spec Kit + Design Docs

**Frame:** The best engineers write before they code. Spec Kit operationalizes spec-driven development for AI-assisted work; design docs do the same thing for humans. Both teach the same underlying discipline.

## Objectives

1. Explain the Spec Kit flow (`/specify` → `/plan` → `/tasks` → `/implement`) and when each phase matters.
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

**1. Spec Kit tour (1 hr).** Install Spec Kit. Run the quickstart. Look at what each phase outputs — read the spec, plan, and tasks artifacts.

**2. The Spec-First Feature (4-5 hrs).** Pick a feature worth 1-2 days of work — non-trivial. Use Spec Kit end-to-end. Commit spec, plan, tasks, and implementation. The spec/plan files should be readable by a stranger.

**3. RFC reading (1.5 hrs).** Read the three docs from the readings. For each: (a) how is the problem framed? (b) what alternatives are considered? (c) what's the decision criterion? (d) what's left unspecified and why?

**4. Write your own (2 hrs).** Pick a real change to one of your projects (auth, caching, schema migration — something with trade-offs). Write a 1-2 page design doc: Problem / Goals / Non-Goals / Proposal / Alternatives / Risks / Rollout. Commit it to the repo.

**5. Get feedback (1 hr).** Share the doc — with a peer, a TA, or run it through this skill's `critique` mode. Take notes. Revise. The git history should show the revision.

## Deliverable

- A repo with a feature built via Spec Kit, with spec/plan/tasks committed
- A design doc (`docs/rfc-001-*.md`) with at least one round of visible revision

## Self-assessment

1. When is Spec Kit overkill? When is ad-hoc prompting better?
2. What goes in "Non-Goals" and why is that often the most important section?
3. How is plan mode in Claude Code different from Spec Kit's `/plan`?
4. After feedback, what changed in your doc? What didn't change, and why?
5. A skeptical reader reads your doc. What's the first objection they'd raise?

## Common pitfalls

- **Specs for trivial work.** Don't write an RFC for a typo. Judgement of *when* to spec is half the skill.
- **Strawmanned alternatives.** "Option B: do nothing" doesn't count.
- **Decorative specs.** If you wrote the spec and ignored it during implementation, you wasted the spec.
- **Vague goals.** "Make it fast" is not a goal. "P95 latency under 200ms for the search endpoint" is.

## Stretch

Find an open RFC in a project you care about. Read it, then write a substantive comment. This is how senior engineers signal their thinking publicly.
