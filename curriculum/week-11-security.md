# Week 11 — Prompt Injection, Red-Teaming, Secrets, Logging

**Frame:** Agents that use tools are a new kind of security surface. Prompt injection is the SQL injection of this decade. Plus: handle secrets like a grown-up and log enough to debug when things go sideways.

## Objectives

1. Explain prompt injection — direct, indirect, and via tool outputs — with concrete attacks.
2. Red-team your own agent: find at least 3 ways to make it misbehave.
3. Design mitigations: scoping, allowlists, confirmation gates, output validation.
4. Handle secrets correctly: never in code, never in logs, rotate when leaked.
5. Add structured logging that you can grep months later.

## Readings

- Simon Willison's prompt-injection canon — start with "Prompt injection: what's the worst that can happen?" and follow the trail.
- **OWASP Top 10 for LLM Applications (2025 edition)** at `genai.owasp.org/llm-top-10/`. Categories:
  - LLM01 — Prompt Injection
  - LLM02 — Sensitive Information Disclosure
  - LLM03 — Supply Chain
  - LLM04 — Data and Model Poisoning
  - LLM05 — Improper Output Handling
  - LLM06 — Excessive Agency
  - LLM07 — System Prompt Leakage
  - LLM08 — Vector and Embedding Weaknesses
  - LLM09 — Misinformation
  - LLM10 — Unbounded Consumption
- A postmortem of any AI-related security incident — search "prompt injection incident".
- The 12-factor app section on configuration.

## Exercises

**1. Attack your own agent.** Take your week-7 agent or week-9 RAG. Try to:
   - Make it ignore its system prompt (direct injection).
   - Put a malicious instruction in the corpus / a tool output (indirect injection).
   - Exfiltrate something it shouldn't have access to.
   - Get it to call a dangerous tool with bad arguments.
   Write up what worked.

**2. Mitigations.** For each attack that worked, design a mitigation:
   - Confirmation gates for destructive tools
   - Input sanitization (where it helps)
   - Output validation (especially for tool calls)
   - Privilege separation (different agents with different tool sets)
   Implement at least two.

**3. Secrets audit.** Grep your repos for: `API_KEY`, `SECRET`, `password`, `token`. Anything found in code = compromised. Move to `.env` + a real secrets manager (1Password CLI, Doppler, SOPS, or your cloud provider's). Verify with `git log --all -p -S 'API_KEY'` that no key is in history.

**4. Structured logging.** Pick an agent or app. Add structured logs (JSON lines): timestamp, run_id, event, payload. Log: every tool call (name, args, result, duration), every model call (tokens in/out, cost, latency). Make sure secrets are never logged.

**5. The fire drill.** Pretend an API key leaked. Walk through: revoke, rotate, audit usage, communicate. Write the runbook so you don't have to think during a real incident.

## Deliverable

- A `security.md` in your agent repo: attacks attempted, mitigations applied
- Structured logs working in at least one project, with a sample log file in the repo (scrubbed of secrets)
- A `runbooks/key-leak.md` — the incident playbook

## Self-assessment

1. Direct vs. indirect prompt injection — give one example of each.
2. Why is "sanitize the prompt" usually insufficient as a mitigation?
3. Your agent has a `delete_file` tool. How should you constrain it?
4. An API key leaked. What are your first three actions, in order?
5. Six months from now you're debugging a weird agent failure. What logs do you wish you had?

## Common pitfalls

- **"My agent is internal, it doesn't matter."** Internal tool outputs (READMEs, PR descriptions, scraped data) are attacker-controlled too.
- **Sanitization as the only defense.** Defense in depth. Confirmation gates, allowlists, scoped tools.
- **Logging secrets.** Filter at the logger, not the call site.
- **Treating prompt injection as a prompt-engineering problem.** It's an architecture problem.

## Stretch

Submit a (responsible-disclosure!) prompt-injection finding to a project you use. Or set up a CTF-style challenge for friends: a vulnerable agent they have to make misbehave. Both teach you a lot.
