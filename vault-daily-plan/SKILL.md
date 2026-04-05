---
name: daily-plan
description: Use when the user wants help planning the current day in the Obsidian vault at /Vault, selecting realistic priorities, shaping today's note in Daily/, or turning backlog items from Daily/backlog.md into a focused plan. Triggers include morning planning, daily focus, choosing top tasks, and cleaning up overloaded daily notes.
---

# Daily Plan

Use this skill to shape a realistic daily note from the vault's existing operating layer.

## Files To Read

- `.obsidian/daily-notes.json` for the filename format
- `Daily/<today>.md` for the current note
- `Daily/backlog.md` for unscheduled work
- `Templates/Daily Note Template.md` if today's note does not exist
- the previous 1-3 daily notes when carryover matters

## Workflow

1. Resolve today's note using the `MM-DD-YYYY` format from `.obsidian/daily-notes.json`.
2. Create today's note from `Templates/Daily Note Template.md` if it is missing.
3. Read today's note, `Daily/backlog.md`, and recent daily notes for carryover.
4. Pick at most 3 primary commitments for `## Focus`.
5. Keep `## To Do` lean
6. Rewrite vague task labels into action language with a clear verb and outcome.
7. Move overflow back to `Daily/backlog.md` instead of letting the day become a dumping ground.
8. Add a short planning note only when it changes execution.

## Selection Rules

- Favor tasks with real deadlines, blocked follow-ups, recurring carryover, or high cost of delay.
- Prefer next actions over project nouns.
- Do not schedule more than the day can realistically hold.
- If a backlog item is too vague to execute, rewrite it or leave it in backlog.
- Respect priorities already written by the user unless the note is overloaded or unclear.

## Editing Rules

- Preserve completed items, events, and user-written notes.
- Do not mark anything complete unless the note already makes that explicit.
- Keep the note concise; the goal is execution clarity, not perfect categorization.
- When moving items between notes and backlog, leave a light movement trail when practical.

## Git Workflow

When the vault is a git repository:

1. Check `git status --short` before editing the daily note.
2. If the repo is already dirty, review the pending changes, stage them, commit them as a pre-plan checkpoint, and `git push origin main` before continuing.
3. After the repo is clean locally, run `git pull --rebase origin main` before editing.
4. Use `git diff -- Daily/ Templates/ .obsidian/daily-notes.json` as needed to verify the planning changes.
5. If you changed files, stage only the touched planning files, commit with a concise planning-specific message, and `git push origin main`.
6. If nothing changed, do not create an empty commit.
7. Never force push or rewrite history from an automated daily-plan run.
