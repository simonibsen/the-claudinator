# Capstone Options

For week 12. Four briefs at different shapes. Pick one — or invent one and validate the scope with the tutor.

## 1. Personal study copilot ("Notebook Copilot")

**Pitch:** A CLI agent that ingests your lecture notes, slides, and readings; lets you query them; auto-generates quizzes for spaced repetition; tracks what you've gotten wrong.

**Architecture sketch:**
- Ingestion script: PDFs/slides/notes → chunks → embeddings → local vector DB
- Query CLI: question → RAG → answer with citations
- Quiz generator: select chunks → generate question → store in `srs.json` for spaced repetition
- Eval harness: 30 hand-written Q&A pairs from your real materials

**Touches:** RAG (week 9), evals (week 10), Agent SDK (week 7), Skills (week 3), API direct (week 8), security/secrets (week 11). Optional: MCP server (week 6) if you want Claude Code integration.

**Hard parts:** Retrieval quality on mixed PDF/slide content, spaced-repetition scheduling, quiz quality.
**Easy parts:** The CLI scaffolding, basic RAG.

**Why this is good:** Real use case (yourself). Visible at every demo. Clearly your work. Other students want to use it.

---

## 2. Domain-specific MCP + agent

**Pitch:** Identify a tool/API/dataset that lacks good MCP coverage. Build the MCP server. Build a small agent or web UI that exercises it for a real use case.

**Examples:** Your university's course catalog + scheduler agent. Strava → training-plan critic. A specific scientific dataset + research assistant. Your library catalog + paper-finder.

**Architecture sketch:**
- MCP server (Python or TS): 5-8 well-shaped tools over the underlying API
- Agent or UI: a workflow that uses the tools to do something useful
- Evals on the workflow, not just the tools

**Touches:** MCP (week 6), Agent SDK or Claude Code (week 7), Skills (week 3), evals (week 10), security (week 11), containers/deploy (week 9).

**Hard parts:** API auth, rate limits, designing the right tool boundary.
**Easy parts:** The MCP scaffolding itself.

**Why this is good:** Useful to a community, not just you. The MCP server is independently valuable — you can publish it.

---

## 3. Eval-driven prompt optimizer

**Pitch:** A tool that, given a prompt + an eval set, mutates the prompt and finds variants that score higher. Open source. Like a fuzzer for prompts.

**Architecture sketch:**
- Eval runner (you mostly built this in week 10)
- Prompt mutator: small set of strategies (rephrase, restructure, add few-shot examples)
- Orchestrator: try variants, score, keep the best
- Reporting: shows you what changes helped and why

**Touches:** Evals (week 10), API direct + prompt caching for cost (week 8), Agent SDK (week 7), security (week 11) — your tool runs untrusted prompts.

**Hard parts:** Useful mutation strategies, avoiding overfitting to the eval set, cost control.
**Easy parts:** None, really. This is the most ambitious option.

**Why this is good:** AI engineering — both the *substance* and a useful tool. Strong portfolio piece for AI/ML jobs.

---

## 4. Public-contribution streak (formerly "OSS")

**Pitch:** Not a single project — land 5 substantive merged contributions over 4-6 weeks in 1-2 public projects you use *and care about*. Doesn't have to be code: a music library bug fix, an LMMS preset, sheet music transcribed to Mutopia, a Godot docs improvement, an Anki deck, an OpenStreetMap mapping streak — all count.

**Start with a conversation, not an issue tracker.** The tutor should walk you through: what projects you use day-to-day, what domains pull you (code, music, hardware, games, science, education, art), what annoyances you've hit. Pick from passion, not from convenience — the resulting contributions are better and the learning sticks.

**Use Claude Code throughout.** Navigate unfamiliar codebases / projects with it, draft contributions with it, prep PR or submission descriptions with it, respond to maintainer review with it. The streak doubles as a real-world test of weeks 1-2's productivity foundation.

**Architecture sketch:** N/A. The artifact is the merged PR list, the conversations with maintainers, and a writeup of what you learned navigating unfamiliar codebases.

**Touches:** Reading codebases (week 1), git (week 2), Claude Code productivity throughout, maybe spec/RFC writing (week 5) for larger PRs.

**Hard parts:** Picking the right projects, maintainer responsiveness, the long tail of small judgment calls.
**Easy parts:** No deploy, no infra.

**Why this is good:** Interviewers love it. Demonstrates judgment, communication, and humility. Different signal than personal projects.

**Note:** This is the same as the `oss` focus's structural replacement for weeks 6-12. If you've been on `oss` focus, you're already doing this — capstone counts as the completion of the streak.

---

## How to pick

- **Want to maximize "I built something cool"?** → Option 1 (most demoable) or 2 (most novel).
- **Want to maximize AI-eng job signal?** → Option 3.
- **Want to maximize "this person works well with others"?** → Option 4.
- **Hate one of them?** Pick another.

## Validate scope with the tutor

Whichever you pick, before starting, run it through:

> I want to build [pitch]. Scope check: what's the smallest version that's still impressive? What would you cut first?

Then go.
