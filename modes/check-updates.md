# Check-updates mode

The skill lives in a git repo at `github.com/simonibsen/the-claudinator`. Curriculum fixes, audits, new sections, and content refreshes land on `main` periodically. This mode checks whether the local install is behind upstream and offers to pull.

## When to invoke

**By name:**
- *"check for updates"*, *"any updates"*, *"sync"*, *"pull latest"*, *"is there a new version"*, *"update the skill"*

**Automatically, at the start of a session:**
- Read `~/the-claudinator/last-update-check.txt`. If absent or >24 hours old, run a silent check.
- **If there are no updates, say nothing.** Just stamp the timestamp and move on.
- **If there are updates, mention once:** *"There are N new commits on the skill upstream since your last sync. Want me to summarize and pull?"*

Don't nag — at most once per session, and only when there's actually news.

## Behavior

1. **Find the skill directory:**
   ```bash
   readlink -f ~/.claude/skills/the-claudinator
   ```
   This handles the symlink case (skill could be a direct clone or a symlink to one).

2. **Check if it's a git checkout:**
   ```bash
   git -C <resolved-dir> rev-parse --git-dir 2>/dev/null
   ```
   If not a git repo, tell the student:
   > *"The skill isn't installed as a git checkout, so I can't auto-update it. To update, re-clone the repo or download the latest. See the install instructions in the README."*

   Stamp the timestamp anyway so we don't re-check tomorrow. Stop.

3. **Fetch upstream silently:**
   ```bash
   git -C <dir> fetch --quiet origin main
   ```
   If fetch fails (offline, auth, repo gone), report briefly (one line) and stop. Don't block the session.

4. **Compare local HEAD to origin/main:**
   ```bash
   git -C <dir> rev-list --left-right --count HEAD...origin/main
   ```
   Returns `<behind> <ahead>` counts.

5. **If `0 0` (in sync):** say *"You're up to date."* (or stay silent if auto-check). Stamp timestamp. Done.

6. **If behind > 0:**
   - Summarize commits:
     ```bash
     git -C <dir> log HEAD..origin/main --oneline --no-merges
     ```
   - Group what you see, if you can read the messages: correctness fixes vs. new content vs. tweaks.
   - Tell the student:
     > *"N new commits on upstream. Highlights: {summary}. Pull now / show me the details first / skip for this session?"*

7. **On "pull now":**
   ```bash
   git -C <dir> pull --ff-only origin main
   ```
   - Report success briefly: *"Updated. {N} commits applied. Notable: ..."* — call out anything user-facing (new mode, renamed command, new section in a week).
   - If pull fails (local changes, conflict, non-ff): explain and let the student decide. Don't force-resolve.

8. **On "show details":**
   ```bash
   git -C <dir> log HEAD..origin/main --no-merges
   ```
   Show full messages. Then re-ask: *"Pull now or skip?"*

9. **On "skip":** stamp the timestamp so we don't re-prompt for ~24 hours. Done.

10. **Always update the timestamp at the end:**
    ```bash
    date -Iseconds > ~/the-claudinator/last-update-check.txt
    ```
    Whether sync, behind, pulled, or skipped — the timestamp gets stamped so we respect the 24h floor.

## What NOT to do

- **Don't pull without asking.** The student should see what's changing.
- **Don't nag.** Silent when in sync; at most once per session when not. The timestamp file enforces this.
- **Don't auto-resolve conflicts** or use `git reset --hard`. If `pull --ff-only` fails, hand control back.
- **Don't check too often.** 24-hour floor between auto-checks.
- **Don't fail the session if the check fails.** Network down, GitHub flaky — skip silently and try again tomorrow.
- **Don't update the skill directly if symlinked to a working copy.** If `readlink -f` resolves outside `~/.claude/skills/`, mention that the resolved location is a working repo and ask the student before pulling — they may not want to fast-forward their own work.

## Where the timestamp lives

`~/the-claudinator/last-update-check.txt` — in the student's progress directory, not the skill. The skill itself stays read-only as far as user state goes.

## Hard rules

- The mode is **non-destructive**. Read, fetch, propose. Apply only on explicit consent.
- The mode is **silent by default**. If there's nothing to say, say nothing.
- The mode **always stamps the timestamp**, even when it didn't do anything, so it respects the 24h floor.
