# Update-content mode

The curriculum makes claims about external things: URLs, API features, model names, command syntax, docs structure. Those change. This mode audits the curriculum against current sources and proposes edits.

## When to invoke

- User says "update the curriculum", "refresh content", "check for stale stuff", "is this still current".
- Automatically at the start of any week: glance at `last-refreshed.txt`. If >30 days old, mention it once and offer to refresh before teaching.

## Behavior

1. **Read `last-refreshed.txt`** at the skill root. If missing, treat as "never refreshed."
2. **Identify the scope:**
   - "Update everything" → all weeks + concentrations + reading-list
   - "Update week N" → that week's file only
   - "Check the API stuff" → weeks 6-8 (MCP, Agent SDK, API direct) + reading list
3. **For each file in scope, extract freshness-sensitive claims:**
   - URLs (any `http(s)://` reference)
   - API features named explicitly (e.g. "prompt caching", "tool use", "Batch API", "structured outputs", "computer use")
   - Model names (`Opus`, `Sonnet`, `Haiku` — and their version numbers if cited)
   - Command syntax (`/specify`, `/plan`, `shift+tab`, `#`, `!`)
   - Doc paths (`claude.com/claude-code/docs/...`, `modelcontextprotocol.io/...`)
   - SDK/library APIs
4. **Fetch current sources** with WebFetch:
   - `claude.com/claude-code/docs` (root + relevant subpages)
   - `docs.anthropic.com` (API docs)
   - `modelcontextprotocol.io`
   - `github.com/github/spec-kit` (README)
   - Anthropic blog index (`anthropic.com/news` or `anthropic.com/engineering`)
   - Any specific repo a week references
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

- **New API features** — if the API now exposes something that materially changes a week's content (e.g. a new batch endpoint, a new caching tier, a new model tier), flag it.
- **Renamed/moved docs** — broken URLs are an easy diff.
- **Deprecated features** — if a week teaches something that's been deprecated, flag aggressively. A student wasting a week on dead syntax is a worse failure than a missing new feature.
- **New canonical resources** — if Anthropic has published a new official guide that supersedes the current readings, prefer the official source.
- **New skills/agents/MCP servers worth mentioning** — bundled or otherwise canonical.

## What NOT to do

- **Don't fabricate.** If WebFetch fails or returns ambiguous content, mark the claim "unverified" and skip — don't invent updates.
- **Don't rewrite for style.** Update facts only. Tone/structure stays.
- **Don't auto-apply.** Always show the proposed edits first.
- **Don't refresh on every invocation.** Check `last-refreshed.txt`; if recent (< 30 days), no-op unless explicitly requested.
- **Don't update reading-list URLs without checking** — a renamed blog post deserves an update; a personal blog that's gone offline might just be down.

## Output format

```
## Curriculum freshness audit — {YYYY-MM-DD}

Last refreshed: {date or "never"}
Scope: {what was checked}
Sources fetched: {n} ({list})

### Proposed changes ({n} total)

**1. curriculum/week-08-claude-api.md — line 27**
- Current: "Use the `response_format` parameter..."
- Source: docs.anthropic.com/... now uses `response_schema`
- Proposal: rename `response_format` → `response_schema`

**2. ...**

### Skipped (could not verify)

- ...

### No change needed
{list of claims that were checked and are still current}

---
Apply all / apply some / discard?
```

## After applying

Tell the student briefly what changed and why. If a change affects a week they are already done, note that — they may want to re-read the relevant section.
