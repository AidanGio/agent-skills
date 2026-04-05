---
name: backlog-triage
description: Use when the user wants to reorganize Daily/backlog.md in the Obsidian vault at /Vault, apply simple prioritization, rewrite vague tasks, identify stale items to drop or clarify, or prepare a weekly backlog review. Triggers include backlog cleanup, weekly triage, stale task review, and prioritizing unscheduled work.
---

# Backlog Triage

Use this skill to keep `Daily/backlog.md` small enough to trust and simple enough to maintain.

## Files To Read

- `Daily/backlog.md`
- the last 7-14 daily notes in `Daily/` when recent activity matters
- `Templates/Weekly Review Template.md` if a review note or report is requested

## Workflow

1. Read `Daily/backlog.md` first.
2. Read recent daily notes to see what is active, repeatedly deferred, or quietly abandoned.
3. Reorganize backlog items into the existing sections:
   - `Next Up`
   - `Later`
   - `Waiting or Scheduled`
   - `Someday or Maybe`
   - `Needs Rewrite or Drop`
4. Keep `Next Up` to a small set of truly near-term items.
5. Rewrite vague items into action-shaped tasks whenever the next action is obvious.
6. Move stale, duplicate, ambiguous, or low-value items into `Needs Rewrite or Drop`.
7. If the prompt requests a report, create a concise markdown note in `output/weekly-reviews/`.

## Prioritization Rules

- Use simple prioritization only; do not invent heavy scoring systems.
- Prioritize deadlines, blocked follow-ups, repeated carryover, and tasks that unblock clusters of work.
- Treat project nouns as backlog smells. Rewrite them before promoting them.
- A stale item is one that keeps lingering without a clear next action, owner, or reason to stay active.
- It is acceptable to recommend dropping work, but do not remove it silently without recording that recommendation.

## Git Workflow

When the vault is a git repository:

1. Check `git status --short` before triaging.
2. If the repo is already dirty, review the pending changes, stage them, commit them as a pre-triage checkpoint, and `git push origin main` before continuing.
3. After the repo is clean locally, run `git pull --rebase origin main` before editing.
4. Use `git diff -- Daily/ Output/` as needed to verify backlog and review-note changes.
5. If you changed files, stage only the touched triage files, commit with a concise triage-specific message, and `git push origin main`.
6. If nothing changed, do not create an empty commit.
7. Never force push or rewrite history from an automated backlog-triage run.
