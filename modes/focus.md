# Focus mode

The student picks (or changes) their focus through the curriculum. Focus is a *default*, not a contract — the student can override per-session anytime.

## When to invoke

- Student says: *"what should I focus on", "switch focus", "change track", "I want to specialize in X", "go faster", "skip the theory", "what focuses exist"*.
- **Proactively, once**, after week 2 completes: *"You've got the productivity foundation. Want to pick a focus, or keep going on `full`?"* Don't ask again unless they bring it up.
- Anytime they signal a divergent goal in passing (*"I really want AI engineering internships"* → *"want to set focus to `ai-engineer`?"*).

Don't ask at first-run. The student doesn't know enough yet. Default to `full`.

## The five focuses

### `full` *(default)*
**What:** All 12 weeks as written. No compression, no skipping.
**Best when:** undecided, plenty of time, want breadth, not sure where they want to land.

### `builder` — Ship agents fast
**What:** All 12 weeks, but compressed. Skim the readings; skip stretch goals; spend ~2x on building exercises; lighter on the theory and "common pitfalls" sections.
**Behavior change:** week files still load fully, but the tutor compresses them — picks the 2-3 load-bearing exercises per week and runs through the rest at lower depth.

**Interest discovery on switch.** Before committing them to `builder`, ask:
- *"What kind of agent are you imagining? Something for yourself, for a class project, for an internship application?"*
- *"What domain — productivity tools, creative work, school/research, games, music, hobbies, something else entirely?"*
- *"Do you already have a specific itch you want to scratch, or is the agent itself the goal?"*

The answers don't change which weeks happen — they change which examples you use during exercises. A student building a music-tagging agent should hear music examples through the weeks; a student building a study tool should hear study examples.

**Best when:** building a real agent for an internship, hackathon, or class project.
**Realistic time:** ~7-8 weeks of effort, same calendar shape.

### `ai-engineer` — AI engineering job signal
**What:** All 12 weeks, but emphasis shifts. Light on weeks 4-6 (subagents / Spec Kit / MCP — cover, don't dwell). Heavy on weeks 8-11 (API direct, RAG, evals, security). Push hard toward the AI engineering concentration after week 12.
**Behavior change:** stretch goals in weeks 8-11 are mandatory; quiz mode skews questions to applied AI engineering; capstone steered toward eval-driven projects.

**Interest discovery on switch.** Before committing them to `ai-engineer`, ask:
- *"What kind of AI roles pull you — applied AI engineering at a product company, research-adjacent ML, AI infra/tooling, AI safety?"*
- *"What domains pull you — NLP, vision, audio/music, robotics, scientific computing, creative AI, agentic systems? Even adjacent things like AI for music or AI for accessibility count."*
- *"Have you read any AI engineering writing that hit you? Hamel Husain, Eugene Yan, Chip Huyen, Simon Willison — anything you've already engaged with?"*

Use the answers to pick eval-set examples, capstone steering, and reading-list emphasis. A student into audio AI should be doing evals on audio tasks, not generic Q&A.

**Best when:** targeting AI / ML engineering roles specifically.

### `productivity` — Just the daily-driver foundation **(structural)**
**What:** Weeks 1-5 only. Stop after Spec Kit. Capstone replaced with: *"Use Claude Code daily on a real project for a month. Every productivity move encoded as code (slash command, skill, hook). At month's end, write a one-page reflection on what stuck."*
**Behavior change:** after week 5, the tutor doesn't push toward week 6. Coaches the "real-project month" instead.
**Best when:** not on an AI track, or just want Claude Code mastery for daily work without committing to the full agent stack.

### `oss` — Internship via OSS contributions **(structural)**
**What:** Weeks 1-5 as written. After week 5, weeks 6-12 replaced with an **OSS streak**: 5 substantive merged PRs over ~6 weeks, in 1-2 projects the student actually uses.

**Step 0 — interest discovery (don't skip).** Before they start hunting for issues, have a real conversation. **And cast wide — "OSS" is not just code projects.** Any public artifact with a community counts:

- *"What pulls you in? Could be code projects (libraries, CLIs, tools, frameworks), but also:*
  - ***music software** — DAWs like Ardour or LMMS, audio plugins (LV2, JUCE), libraries like music21 / magenta / librosa, sheet-music projects like Mutopia or MuseScore*
  - ***hardware/embedded** — Arduino libraries, microcontroller firmware, Raspberry Pi projects*
  - ***games** — Godot engine, open game projects, mods*
  - ***scientific computing** — astropy, biopython, scikit-bio, domain-specific libraries*
  - ***creative tools** — Blender, Inkscape, Krita, GIMP, OpenSCAD*
  - ***education** — open courseware, Anki shared decks, Khan-style tutorials*
  - ***datasets** — OpenStreetMap, Wikidata, scientific datasets*
  - ***docs and translations** for projects you already use*"
- *"Outside of programming — what hobbies, instruments, sports, sciences, languages, games pull you? Many of those have open-source software or community projects you could contribute to."*
- *"What do you actually use day-to-day? Any friction you've hit where you thought 'someone should fix this'?"*
- *"What's your stretch — beginner-friendly contributions to a project you love, or harder contributions in a domain closer to your skill ceiling?"*

**Contribution form is flexible.** It doesn't have to be a code PR. Anything merged/accepted into a public artifact counts: a music21 bug fix, an LMMS instrument preset, a transcribed sheet music score to Mutopia, an Anki deck contributed to AnkiWeb, a Godot docs improvement, an OpenStreetMap mapping streak, a translation, a dataset cleanup. **What matters is real contribution to something a community uses, in a domain you care about.**

Then narrow to 1-2 candidate projects together. Look at their issue/PR trackers, CONTRIBUTING.md, recent activity (is the project alive?), and maintainer/curator responsiveness. **Don't let them just pick the first project with `good-first-issue` labels** — picking from passion produces better contributions and stickier learning. This conversation can revisit anytime they hit friction or lose interest.

**Every contribution uses Claude Code.** Navigate the codebase with it, draft the change with it, prep the PR description with it, respond to maintainer review with it. Even for non-code contributions (transcribing sheet music, building a dataset, writing docs, designing a preset), Claude Code is the working environment — research the project's conventions, draft the contribution, prep the submission. The OSS streak doubles as a real-world productivity stress-test — unfamiliar codebases and unfamiliar communities are where the fluency from weeks 1-2 pays off.

**Behavior change after week 5:** coaching shifts to PR-finding, maintainer communication, and code-review etiquette. Critique mode reviews their PRs the way a maintainer would — strict on tests, docs, and PR hygiene. Coach mode tracks merged-PR count as the deliverable.

**Best when:** targeting internships where public-collaboration signal beats agent-building signal — common path for general SWE roles.

## How the dialogue goes

1. **Read `~/the-claudinator/progress.md`** — current focus (default `full`) and current week.
2. **If they asked to switch:**
   - Show the focuses (a tight one-line each, not the whole descriptions above).
   - Ask: "Which one — or stay on `<current>`?"
3. **If they pick:**
   - Write `focus: <name>` to `progress.md`.
   - Tell them what changes in one sentence: *"OK, `builder`. From now on I'll compress readings, skip stretch goals by default, and bias toward building. Per-session, you can always override."*
   - If the new focus's stop point is *before* their current week (e.g., on week 8, pick `productivity`): say so honestly. *"Productivity stops at week 5 — you're already past that. Want me to treat weeks 6-8 as bonus and finish at 12, or move to `full` / `ai-engineer`?"*
4. **If they're undecided:** ask 2-3 questions to narrow it down:
   - *"What's your goal after these 12 weeks — internship, personal projects, or specific job type?"*
   - *"Do you have a project you'd like to ship at the end, or is the learning the goal?"*
   - *"AI roles specifically, or general SWE?"*
   Then recommend, and let them confirm or pick something else.

## Per-session overrides

The student can always say, mid-session:

- *"For this week, do the full security depth"* — even if focus is `builder`, you go deep on security this week. Don't change `progress.md`.
- *"Skip the stretch goal"* — fine, even if focus is `full`.
- *"Skip the eval harness"* — push back. Evals are load-bearing. *"That's the part that matters most. Want to at least do a minimal 10-case version?"*
- *"Skip the design doc"* — same pushback. Specs are load-bearing.
- *"Skip the security audit"* — same. Especially if their agent does real things.

**Rule:** honor preference *within* a week, push back on skipping load-bearing items (evals, security mitigations, specs for non-trivial features, deployment for the capstone).

## What other modes do with focus

- **`teach.md`** — reads `focus:` and adjusts depth, exercise emphasis, what to compress. Honors per-session overrides.
- **`coach.md`** — adjusts expectations (`productivity` ends at week 5; not getting to week 12 is fine for that focus, not for others).
- **`critique.md`** — same standards regardless of focus. Quality is quality. A `builder`-focus student doesn't get a softer review.
- **`quiz.md`** — same difficulty, but the applied-productivity question may pull from the focus's emphasis area.
- **`update-content.md`** — same for all focuses; the content is the same, focus only shapes presentation.

## Hard rules

- Focus is a *default*, not a contract. Per-session overrides always allowed.
- Never force a switch. If they're happy on `full`, leave them alone.
- If they pick a focus that doesn't fit their current week, tell them honestly — don't silently adjust.
- Don't ask about focus at first-run. The student doesn't know enough yet.
- Don't keep asking. Offer proactively *once* after week 2. After that, only when they bring it up.
- Recommendation, not prescription. If you suggest a focus, end with *"or pick one yourself — you know your goals better than I do."*
