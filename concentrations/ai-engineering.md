# AI Engineering Concentration

After module 12. This is where the career leverage is for the next 3-5 years. Six topics, each scoped as a small focused project.

## 1. Evals as a profession

You started this in module 10. The real skill is *operationalizing* it: eval-driven development, regression suites, A/B testing prompt changes, eval data flywheels (capturing prod failures back into the eval set).

**Read:** Hamel Husain's eval canon (every post). Eugene Yan's evals series.
**Build:** Take one of your projects from production-quality. Set up: nightly eval runs, dashboards, automatic failure capture, regression alerts.

## 2. Prompt caching as production craft

Real money. Real latency. Real architectural choices.

**Read:** Anthropic's prompt caching docs (deeply — not skim). Case studies on caching economics.
**Build:** Take one app to "caching-aware architecture." Measure: cache hit rate over time, $/request, P95 latency. Optimize.

## 3. Embeddings as a swiss army knife

Beyond RAG: semantic dedup, classification, clustering, anomaly detection, search-as-a-service. Most engineers under-use this.

**Build:** Three small apps that all use embeddings but for different jobs: search, dedup of a noisy dataset, and a "find related" feature.

## 4. Latency engineering

Streaming, parallelism, speculative decoding, prefetching, batch APIs, smaller models for cheap pre-filtering.

**Read:** Latency-focused posts (search "LLM latency" on Hamel/Eugene Yan's blogs, Pragmatic Engineer, Latent Space).
**Build:** Take an app, profile it, get its P95 latency down by 2x without quality loss.

## 5. Agent architectures

You've seen Claude Code's pattern. There are others: ReAct, Plan-and-Execute, Reflexion, multi-agent debate, swarm patterns. Know the literature.

**Read:** The ReAct paper, the Reflexion paper, Anthropic's posts on agentic patterns, Lilian Weng's "LLM Powered Autonomous Agents" post.
**Build:** Re-implement a small ReAct loop from scratch (no framework). Then build the same thing with Plan-and-Execute. Compare.

## 6. Fine-tuning when it's actually worth it

Most teams shouldn't fine-tune. Knowing *when to* — and how — is the differentiator.

**Read:** Hamel Husain's "Fine-tuning is dead" post and their fine-tuning posts (they are contrarian about it both ways for good reasons). OpenAI's fine-tuning guide for concepts.
**Build:** Fine-tune a small open model (Llama 3, Mistral) on a task where you have data. Compare quality against an API model with a good prompt. Notice when each wins.

## Books to read

- **AI Engineering** by Chip Huyen — the field's textbook
- **Designing Machine Learning Systems** by Chip Huyen — broader, foundational
- **Reading research papers** as a skill — find a paper-club or do "paper a week"

## People to follow

- Simon Willison (`simonwillison.net`)
- Hamel Husain (`hamel.dev`)
- Eugene Yan (`eugeneyan.com`)
- Chip Huyen (`huyenchip.com`)
- Andrej Karpathy (X, YouTube)
- Jeremy Howard (X, fast.ai)

## What "done with the concentration" looks like

- One public artifact per topic (post, repo, or contribution)
- Six topics, scoped to fill roughly a quarter
- Your blog has six posts about AI engineering work you've actually shipped
- You can hold a 30-minute conversation with a senior AI engineer without bluffing
