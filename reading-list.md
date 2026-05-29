# Reading List

Canonical references for the curriculum. Read the docs before the tutorials. Tutorials go stale; docs are maintained.

## Claude & agents (primary)

- **Claude Code docs** — `code.claude.com/docs/en/` (overview, settings, hooks, skills, sub-agents, permissions). Read top to bottom once. Refer back constantly.
- **Anthropic API docs** — `docs.claude.com/en/docs/` — Messages, Tool Use, Prompt Caching, Batch.
- **Anthropic Cookbook** — `platform.claude.com/cookbook/` — notebook-style worked examples across tool use, RAG, evals, prompt caching, Agent SDK, and Managed Agents. Browse by section; specific module readings point at individual recipes.
- **Skills documentation** — `code.claude.com/docs/en/skills`.
- **Sub-agents documentation** — `code.claude.com/docs/en/sub-agents`.
- **Agent SDK docs** — `docs.claude.com/en/api/agent-sdk/overview` (or `code.claude.com/docs/en/agent-sdk`).
- **Model overview & current IDs** — `docs.claude.com/en/docs/about-claude/models/overview`.
- **Anthropic engineering blog** — for posts on agentic patterns, multi-agent design, model behavior.

## Spec-driven dev

- **Spec Kit** — `github.com/github/spec-kit`
- **Rust RFCs** — `github.com/rust-lang/rfcs` — read 2-3 to see the form
- **Oxide RFDs** — `rfd.shared.oxide.computer` — public engineering culture artifact

## AI engineering (the canon)

- **Simon Willison** — `simonwillison.net` — prompt injection, embeddings, local LLMs, practical posts. Subscribe.
- **Hamel Husain** — `hamel.dev` — evals, fine-tuning, applied AI engineering. The single most useful blog in this space.
- **Eugene Yan** — `eugeneyan.com` — evals, RAG, ML systems.
- **Chip Huyen** — `huyenchip.com` — ML systems, AI engineering. Author of two books listed below.
- **Lilian Weng** — `lilianweng.github.io` — deep technical posts; "LLM Powered Autonomous Agents" is foundational.

## Local LLMs / fine-tuning

- **Ollama** — `ollama.com` and its GitHub — easiest path to running models locally.
- **unsloth** — `github.com/unslothai/unsloth` — fastest accessible LoRA fine-tuning. Apple Silicon training fully supported as of May 2026; NVIDIA + AMD also covered. Cross-platform web UI via Unsloth Studio.
- **MLX-LM** — `github.com/ml-explore/mlx-lm` — Apple Silicon native LLM inference and fine-tuning. Install with `pip install mlx-lm`.
- **MLX core** — `github.com/ml-explore/mlx` — the underlying array framework.
- **HuggingFace docs** — `huggingface.co/docs` — deepest reference for fine-tuning, datasets, model hub.
- **Open LLM Leaderboard** — `huggingface.co/spaces/open-llm-leaderboard` (note: classic leaderboard space is dormant; the **Model Comparator** space is the current alternative for head-to-head comparisons).
- **mergekit** — `github.com/arcee-ai/mergekit` — model merging.

## Software engineering practice

- **Pro Git** — `git-scm.com/book` — Ch 3, 7, 10 are most useful.
- **The Twelve-Factor App** — `12factor.net` — short, opinionated, still right.
- **Will Larson** — `lethain.com` — "Scaling Engineering Teams via Writing Things Down" and many others.
- **MCP spec** — `modelcontextprotocol.io`
- **OWASP Top 10 for LLM Applications (2025 edition)** — `genai.owasp.org/llm-top-10/`. Categories: prompt injection, sensitive info disclosure, supply chain, data/model poisoning, improper output handling, excessive agency, system prompt leakage, vector/embedding weaknesses, misinformation, unbounded consumption.

## Books

- **AI Engineering** by Chip Huyen (2024+) — the field's textbook
- **Designing Machine Learning Systems** by Chip Huyen — broader, foundational
- **Designing Data-Intensive Applications** by Martin Kleppmann — for system-design grounding
- **The Pragmatic Programmer** by Hunt & Thomas — career-long fundamentals

## Newsletters & podcasts

- **Latent Space** podcast — applied AI engineering interviews
- **Pragmatic Engineer** newsletter — career, industry, eng culture
- **The Sequence** — research roundups (skim, don't deep-read)
- **Import AI** — Jack Clark's weekly AI roundup

## People to follow on X / Bluesky

- @simonw (Simon Willison) — practical AI
- @HamelHusain — evals, fine-tuning
- @eugeneyan — ML systems
- @karpathy — Karpathy, mostly fundamentals
- @jeremyphoward — fast.ai, practical ML
- @ChipHuyen — AI engineering

## What to skip

- Most YouTube tutorials over 6 months old.
- Twitter threads claiming "10 prompts that change everything." They don't.
- Medium articles by people who built one demo.
- Anything that sounds like marketing for a framework you'll never use.
