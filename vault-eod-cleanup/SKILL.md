---
name: end-of-day-cleanup
description: Use when the user wants to close out today's daily note in the Obsidian vault at /Vault, move unfinished tasks forward, defer work back to Daily/backlog.md, or leave a concise day-end summary. Triggers include end of day cleanup, shutdown routine, rolling tasks forward, and closing a daily note.
---

# End Of Day Cleanup

Use this skill to close the current day without losing task history or creating sloppy carryover.

## Files To Read

- `.obsidian/daily-notes.json` for the daily filename format
- `Daily/<today>.md` for today's note
- `Daily/<tomorrow>.md` when tasks need to move forward
- `Daily/backlog.md` for unscheduled work
- `Templates/Daily Note Template.md` if tomorrow's note must be created

## Workflow

1. Resolve today's note and inspect `## To Do`, `## Events`, and `## Notes`.
2. Mark tasks as `{x}` only when the note clearly shows they were completed.
3. For each unfinished task, choose one path:
   - move it to tomorrow's note if it is still active and date-worthy
   - move it to `Daily/backlog.md` if it should remain unscheduled
   - drop it only if the note clearly shows it is obsolete
4. Create tomorrow's note from `Templates/Daily Note Template.md` if needed.
5. Leave a short trail in today's note using `{>}` for forward moves and `{<}` for backlog deferrals.
6. Add a concise `## End of Day` summary with wins, open loops, and what moved.

## Cleanup Rules

- Do not silently delete tasks.
- Keep tomorrow's note lean; do not carry forward everything by default.
- Favor backlog for non-urgent leftovers and tomorrow's note for real commitments.
- Preserve the user's events and notes unless you are only tightening formatting.
- If a task is vague, rewrite it before carrying it forward.

## Git Workflow

When the vault is a git repository:

1. Check `git status --short` before editing the end-of-day files.
2. If the repo is already dirty, review the pending changes, stage them, commit them as a pre-cleanup checkpoint, and `git push origin main` before continuing.
3. After the repo is clean locally, run `git pull --rebase origin main` before editing.
4. Use `git diff -- Daily/ Templates/ .obsidian/daily-notes.json` as needed to verify carry-forward changes.
5. If you changed files, stage only the touched cleanup files, commit with a concise cleanup-specific message, and `git push origin main`.
6. If nothing changed, do not create an empty commit.
7. Never force push or rewrite history from an automated cleanup run.
