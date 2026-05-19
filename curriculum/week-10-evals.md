# Week 10 — Evaluating Your Own Agent

**Frame:** This is the highest-ROI week. Most teams shipping AI products are terrible at evals. The ones that aren't, dominate. Learn this and you'll be ahead of 90% of your peers, including most engineers ten years your senior.

## Objectives

1. Articulate why "it feels right" is the failure mode of AI product teams.
2. Build an eval set for an existing project (last week's RAG is the easy target).
3. Implement at least 3 eval types: deterministic checks, code-graded, LLM-as-judge.
4. Run evals on every change to your agent/prompt — make them part of the loop.
5. Diagnose a regression using your evals.

## Readings

- Hamel Husain's blog — "Your AI Product Needs Evals" (or whatever the current canonical post is).
- Eugene Yan's blog — evals posts.
- Anthropic's evals documentation, if available.
- One post on LLM-as-judge pitfalls.

## Exercises

**1. Hand-write 20 eval cases.** For your RAG (or another AI app you've built). Each case: input, expected behavior, why this is a good case. Cover happy path, edge cases, things you've seen go wrong.

**2. Deterministic evals.** What can you check with code, not a model? Format checks (valid JSON?), citations present, length bounds, refusal triggers, factual checks against known answers. Write code that scores each.

**3. LLM-as-judge.** For cases where determinism isn't enough (quality of summary, helpfulness of answer): write a judge prompt. Cheaper model (Haiku) is usually right. Make the rubric explicit. Run it. Sanity-check by manually grading 10 and seeing if the judge agrees.

**4. The eval harness.** Wire it up: one command runs all evals, prints pass/fail and rates. Commit results over time. Now every prompt change is graded automatically.

**5. Cause a regression on purpose.** Make a change you suspect will hurt quality. Run evals. Did they catch it? If not, why not, and what eval is missing?

## Deliverable

- An eval harness in your RAG repo (or other AI app) with ≥20 cases, ≥3 eval types
- Eval results tracked in a `results/` directory, one file per run
- A `evals-learnings.md`: what your evals caught, what they missed, what you'd add next

## Self-assessment

1. Why is "vibes-testing" a prompt change worse than no testing at all?
2. When is deterministic eval better than LLM-as-judge? When is the reverse?
3. LLM-as-judge can lie. Name two ways to detect when it does.
4. Your evals all pass but users complain. What's the diagnostic?
5. You changed the prompt and one eval dropped from 0.9 to 0.6. Three diagnostic steps?

## Common pitfalls

- **Vibes-only.** "It seems better" is not a result. You'll deceive yourself.
- **Tiny eval sets.** 5 cases catches nothing. 50+ is the floor.
- **Judge using the same model.** Cheaper, different model for judging avoids sycophancy.
- **No baselines.** Always compare to "before your change" — absolute scores lie.
- **Optimizing the eval, not the product.** If your evals don't capture what users care about, fix the evals.

## Stretch

Set up evals to run on every PR via GitHub Actions. Make them block merge if scores drop. Now your prompt-engineering has a regression suite.

## Sidebar — local models as judges (with caveats)

LLM-as-judge with a local 7-8B model is free, which makes it tempting for high-volume dev iteration. **Caveats are real:** local judges are often more sycophantic than Claude, have less reliable calibration, and can have systematic biases (favoring longer outputs, favoring outputs that match training style). Use them for cheap iteration, but always sanity-check by re-running 20-30 cases with a stronger judge (Haiku or Sonnet) before trusting eval results that influence decisions. The `concentrations/local-llms.md` deep-dive expands on this and shows how to build a multi-judge comparison harness.
