# Module 9 — Containers + Deploy + RAG Fundamentals

**Frame:** Two things this module: ship something to the internet (containers + a PaaS), and learn the foundational pattern of applied AI (retrieval-augmented generation).

## Objectives

1. Write a Dockerfile from scratch, explain each line, and understand multi-stage builds.
2. Deploy a real app to Fly.io (or Railway / Render) with a public URL.
3. Explain RAG: embeddings, vector search, chunking, retrieval, generation.
4. Build a working RAG system over a corpus you care about (lecture notes, papers, a codebase).
5. Recognize when RAG is the right answer vs. just stuffing context vs. fine-tuning.

## Readings

- Docker's official "Get Started" + the multi-stage builds page.
- Fly.io's "Hands-on" tutorial.
- One canonical RAG post — try Pinecone's "Learn" guide or LangChain's docs (read for concepts, not the framework).
- Simon Willison's posts on embeddings, if available.

## Exercises

**1. Dockerize one app.** Pick a project (your agent from module 7 is a good candidate, but a web app is better). Write a Dockerfile. Multi-stage build. Run it locally. The image should be lean (<200MB if possible).

**2. Deploy it.** Push to Fly.io. Set env vars (including your Anthropic API key) via `flyctl secrets`. Visit the URL. Pat self on back.

**3. RAG from scratch.** No frameworks. Build it yourself:
   - Pick a corpus (your lecture notes work great)
   - Chunk it (start simple: ~500 token chunks, ~50 token overlap)
   - Embed each chunk (Anthropic embeddings or OpenAI, your choice)
   - Store in a local vector DB (`chromadb` or `pgvector` — Chroma is easier)
   - Build a query function: embed query → retrieve top-k → put in prompt → generate answer
   - Wrap in a CLI or simple FastAPI endpoint

**4. The retrieval problem.** Run 10 questions through your RAG. Where does retrieval fail? Try: different chunk sizes, different k values, query rewriting. Write down what helped and what didn't.

## Deliverable

- One Dockerized app deployed at a real URL (in README)
- A working RAG CLI/API over a real corpus, public repo with README and demo
- A `retrieval-notes.md` documenting what you tried for retrieval quality, with results

## Self-assessment

1. What's a multi-stage Docker build for, and what's wrong with not using one?
2. Your image is 1.5GB. What are the top 3 causes?
3. Why chunk? Why not just embed the whole document?
4. Walk me through your retrieval pipeline. Where's the most likely failure point?
5. When is RAG the wrong answer? Give two cases.

## Common pitfalls

- **`FROM ubuntu:latest`-everything.** Use small base images (`python:3.12-slim`, `alpine` if you can manage).
- **Secrets baked into the image.** Use the platform's secrets store.
- **Chunking by character count blindly.** Sentence/paragraph boundaries matter for quality.
- **No retrieval evaluation.** "It feels right" is not a metric — that's the next module.
- **Reaching for LangChain too early.** Build it once from scratch so you know what's happening.

## Stretch

Add a reranker step (a second model that scores retrieved chunks for relevance before sending to the generator). Measure whether it helps.
