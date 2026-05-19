# Week 12 — Capstone: Ship an Agent

**Frame:** A real, useful agent that combines at least 5 weeks of material. This is the portfolio piece for internship interviews. Open-ended — but with a high bar.

## Why this is the capstone

The previous 11 weeks teach pieces. The capstone tests whether you can *integrate*. Five things only this week teaches:

1. **Scoping under constraint.** Real engineering is "make decisions you can't unmake quickly." Open-ended scope forces you to cut, defer, and ship. No exercise can simulate this.
2. **End-to-end ownership.** Spec → build → eval → secure → deploy → write up → support a user. Coursework usually stops at "code compiles." Real work doesn't.
3. **A portfolio artifact recruiters can actually see.** Internship interviews are won by candidates who can say "look at this thing I shipped" and link to a repo + a live URL + a writeup. Coursework is invisible. This week makes you visible.
4. **The "is it good?" judgment.** With evals from week 10 and a real user, you get the only feedback that matters: did it work for someone other than you? That feedback shapes you more than any tutor can.
5. **Proof the curriculum stuck.** If you can't combine 5 weeks of material into one project, the previous weeks were entertainment, not learning. The capstone is the regression test.

**Why "ship an agent" specifically, not "ship anything":**
- Aligns with current hiring signal — companies are hiring people who can build agents, not people who've read about them.
- Forces synthesis of the load-bearing weeks (skills, subagents, MCP, Agent SDK, evals, security) into one artifact instead of six separate toys.
- An agent that uses tools and is evaluated is qualitatively harder than a CRUD app — the difficulty itself is the signal.
- It's also the most demoable thing you could possibly build at this point in your career. Demoable wins interviews.

## Objectives

1. Ship a working agent at a public URL or installable repo.
2. Combine ≥5 of: skills, subagents, Spec Kit, MCP, Agent SDK, API features, RAG, evals, security.
3. Write the project up at blog-post quality — the kind of post someone would share.
4. Open-source it under a real license, with a README a stranger can use.
5. Get one real user (you don't count) — peer, sibling, parent, online stranger.

## How this week works

This isn't a curriculum week — it's a deliverable week. The tutor's job here is to:
- Help you scope (capstone options in `concentrations/capstone-options.md`)
- Run the spec-kit flow for the project
- Review your work as you go (use the `critique` mode)
- Pressure-test before you call it done

## Scoping rules

- **20-40 hours of work.** Less and it's a toy; more and it'll never ship.
- **Solves a real problem.** Your own counts. "Make my Strava data into a weekly digest." "Grade homework against a rubric." "Triage my dad's small-business inbox."
- **Has an evaluatable success criterion.** Not "feels useful." Concrete: "summarizes X in under N seconds with >90% factual accuracy on a 30-case eval."
- **Touches ≥5 weeks' material.** If you can't enumerate them, scope wider.

## The week's flow

1. **Day 1: Spec.** Use Spec Kit. Commit `spec.md`, `plan.md`, `tasks.md`. Get the tutor to review the spec before coding.
2. **Days 2-4: Build.** Track time. Push commits at least daily.
3. **Day 5: Evals.** ≥20 eval cases. Run them. Iterate prompts until passing.
4. **Day 6: Polish.** README, demo (GIF or asciinema), deploy, structured logging.
5. **Day 7: Ship + write up.** Blog post draft. One user uses it. Capture their feedback.

## Deliverable

- A public GitHub repo with: README, working code, eval harness with passing results, demo, license (MIT or Apache 2.0)
- A live URL OR a one-line install instruction that works
- A blog-post-quality write-up (in the repo as `WRITEUP.md`, or hosted): what it does, why it exists, what was hard, what you'd do differently
- Evidence one real user ran it (screenshot of their feedback in the writeup is fine)

## Self-assessment

1. Walk me through your architecture in 90 seconds. Could you do this in an interview?
2. What would you build differently if you had another month?
3. What's the cost per use? Could you afford 1,000 users a day?
4. One thing in the project you'd hide from a senior reviewer, and why?
5. One thing you'd point a senior reviewer at first because you're proud of it?

## Common pitfalls

- **Scope creep.** Cut features ruthlessly. Working > impressive.
- **No evals.** Without them, "it's done" means "I'm tired of working on it."
- **Skipping the writeup.** The writeup is half the value. Without it, recruiters can't find you.
- **No real user.** "I built it" is half a project. "I built it and someone uses it" is a project.
- **Polishing forever.** Ship at "good enough" and write up what's left for v2.

## After the capstone

- Add it to your resume and LinkedIn.
- Mention it in every internship application this cycle.
- Plan the next thing — see `concentrations/` for two paths.

## Stretch

Submit a talk or post about it to one of: HN, a school CS club, a meetup, a podcast. Public artifacts compound.
