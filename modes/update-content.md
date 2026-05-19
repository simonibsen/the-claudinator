# Update-content mode

The curriculum makes claims about external things: URLs, API features, model names, command syntax, doc structure, **what Claude Code actually does when you press X**, and **which tools to recommend**. All of those change. This mode audits the curriculum against current sources and proposes edits — for *both* stale citations and incorrect instructions.

## When to invoke

- User says: *"update the curriculum"*, *"refresh content"*, *"check for stale stuff"*, *"is this still current"*, *"run an audit"*, *"verify the instructions"*, *"correctness check"*, *"deep audit"*.
- Automatically at the start of any week: glance at `last-refreshed.txt`. If >30 days old, mention it once and offer to refresh before teaching.
- Anytime the student pushes back on something the curriculum claims and the claim isn't obvious from current docs — audit that specific claim before defending it.

## Behavior

1. **Read `last-refreshed.txt`** at the skill root. If missing, treat as "never refreshed."
2. **Identify the scope:**
   - "Update everything" → all weeks + concentrations + reading-list
   - "Update week N" → that week's file only
   - "Check the API stuff" → weeks 6-8 (MCP, Agent SDK, API direct) + reading list
3. **For each file in scope, extract auditable claims in three categories:**

   **A. Citations (freshness)** — easy diffs against fetched sources:
   - URLs (any `http(s)://` reference)
   - Model IDs (`claude-haiku-4-X`, `claude-sonnet-4-Y`, `claude-opus-4-Z`)
   - SDK/library install commands (`pip install anthropic`, `npm install @anthropic-ai/sdk`)
   - Specific model tags (`llama3.2:3b`, `qwen2.5:7b-instruct`)

   **B. Behavioral claims (correctness)** — claims about what *actually happens* when the user does X. These are where stale curricula mislead students worst:
   - Keyboard shortcuts (`shift+tab` for plan mode — does it toggle, or cycle modes?)
   - Slash command behavior (`/help`, `/init`, `/clear`, `/keybindings`, `/<skill-name>`)
   - In-prompt prefixes (`!` for bash, `#` for memory)
   - Hook event names and the complete event list (the curriculum may name a subset; current docs may have more)
   - Settings.json shape (matcher syntax, permission patterns, env vars)
   - File auto-loading (CLAUDE.md scope: project / user / nested / imports)
   - API features (prompt caching TTL, tool-use vs structured-outputs, batch discount, response schemas)
   - Subagent types built-in
   - MCP server protocol details
   - Spec Kit command set (`/specify`, `/plan`, `/tasks`, `/implement` — plus any new ones)

   **C. Tool/library recommendations (currency)** — concrete recommendations that may have been superseded:
   - "Use unsloth for LoRA" — still the leader, or has it been replaced?
   - "Use Ollama for local serving" — same question
   - "Use Fly.io for deploy" — still student-friendly?
   - "Use Chroma / pgvector" — still good for week-9 RAG?
   - Reading-list blogs and books — still maintained?
4. **Fetch current sources** with WebFetch:
   - Claude Code docs: `code.claude.com/docs/en/` (overview, hooks, skills, sub-agents, permissions, settings, etc.)
   - Anthropic API docs: `docs.claude.com/en/docs/` and `platform.claude.com/docs/en/`
   - Models reference: `docs.claude.com/en/docs/about-claude/models/overview`
   - MCP: `modelcontextprotocol.io` (quickstart, examples, architecture)
   - Spec Kit: `github.com/github/spec-kit` (README)
   - Anthropic blog: `anthropic.com/news` or `anthropic.com/engineering`
   - Any specific repo a week references (e.g. `github.com/ml-explore/mlx-lm`, `github.com/unslothai/unsloth`)
5. **Diff claim-by-claim.** For each claim that has likely changed:
   - Show the current claim (file + line + text)
   - Show the new source-of-truth
   - Propose a specific edit
6. **Present a proposal, don't auto-apply.** Show the full list of proposed changes. Ask: "apply all / apply some / discard." The student or their parent reviews.
7. **On apply:**
   - Make the edits
   - Append to `CHANGELOG.md` at the skill root: date, files changed, summary
   - Update `last-refreshed.txt` with today's date and a one-line summary of what was current
8. **On discard:** still update `last-refreshed.txt` so we don't re-check the same things tomorrow.

## What to look for (rough heuristics)

- **Wrong behavioral claims** — if the curriculum says "X happens when you do Y" and the docs say otherwise, this is the most damaging kind of error. Flag aggressively. A student doing exactly what the curriculum says and getting a different result will lose trust in the whole curriculum.
- **Incomplete enumerations** — when the curriculum lists "the X are A, B, C" and docs list more, flag as incomplete (not necessarily wrong, but worth fixing).
- **New API features** — if the API now exposes something that materially changes a week's content (e.g. a new batch endpoint, a new caching tier, a new model tier), flag it.
- **Renamed/moved docs** — broken URLs are an easy diff.
- **Deprecated features** — if a week teaches something that's been deprecated, flag aggressively. A student wasting a week on dead syntax is a worse failure than a missing new feature.
- **New canonical resources** — if Anthropic has published a new official guide that supersedes the current readings, prefer the official source.
- **New skills/agents/MCP servers worth mentioning** — bundled or otherwise canonical.
- **Tool succession** — if a recommended tool has been replaced by a better/more-active alternative, flag and propose the swap.

## What NOT to do

- **Don't fabricate.** If WebFetch fails or returns ambiguous content, mark the claim "unverified" and skip — don't invent updates.
- **Don't trust training-data recall for verification.** Your memory of how things worked is not a source. If you can't fetch the canonical doc, the claim stays "unverified" — period. Recall is fine for *suggesting* what to look at, never for *confirming* the curriculum is right.
- **Don't rewrite for style.** Update facts only. Tone/structure stays.
- **Don't auto-apply.** Always show the proposed edits first.
- **Don't refresh on every invocation.** Check `last-refreshed.txt`; if recent (< 30 days), no-op unless explicitly requested.
- **Don't update reading-list URLs without checking** — a renamed blog post deserves an update; a personal blog that's gone offline might just be down.

## Output format

```
## Curriculum audit — {YYYY-MM-DD}

Last refreshed: {date or "never"}
Scope: {what was checked}
Sources fetched: {n} ({list})

### Correctness issues (high priority — {n} total)
*Claims about how things work that are wrong or incomplete.*

**1. curriculum/week-01-foundations.md — line 8**
- Current claim: "Know plan mode, `!` bash prefix, `#` memory shortcut, `/` slash commands cold."
- Implied: `shift+tab` toggles plan mode (line 20).
- Source: docs.claude.com/... — `shift+tab` cycles through modes (auto-accept / plan / default).
- Proposal: change "toggles plan mode" framing to "cycles into plan mode (and other modes)".

### Freshness issues (medium priority — {n} total)
*Citations and names that have drifted.*

**N. curriculum/week-08-claude-api.md — line 27**
- Current: model ID `claude-sonnet-4-6`
- Source: docs.anthropic.com/... — current is `claude-sonnet-4-X`
- Proposal: bump model ID.

### Recommendation currency ({n} total)
*Tools/libraries that may have been superseded.*

**N. concentrations/local-llms.md — line 142**
- Current: "Use unsloth for LoRA"
- Source: still active per github.com/unslothai/unsloth — no proposal.

### Skipped (could not verify)
- ...

### No change needed
{list of claims that were checked and are still current}

---
Apply all / apply some / discard?
```

## After applying

Tell the student briefly what changed and why. If a change affects a week they are already done, note that — they may want to re-read the relevant section.
