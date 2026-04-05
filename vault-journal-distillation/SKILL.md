---
name: journal-distillation
description: Use when the user wants to distill recent daily notes in the Obsidian vault at /Vault into patterns, repeated open loops, follow-ups, ideas, or durable insights. Triggers include journal distillation, weekly reflection, extracting patterns from Daily/ notes, and summarizing recent days into output/ or the wiki.
---

# Journal Distillation

Use this skill to turn a run of daily notes into a concise reflection and action signal.

## Files To Read

- recent notes in `Daily/`
- `Templates/Journal Distillation Template.md` for report structure
- `wiki/_master-index.md` and relevant topic `_index.md` files only if a durable insight clearly belongs in `wiki/`

## Workflow

1. Read the requested date range or default to the last 7 daily notes.
2. Extract repeated themes, unfinished commitments, people to follow up with, decisions, ideas, and recurring blockers.
3. Write a concise markdown report in `output/journal-distillations/`.
4. Separate evidence from inference.
5. If a reusable concept clearly belongs in `wiki/`, navigate through `wiki/_master-index.md` and update the right topic page or create a focused new one.

## Distillation Rules

- Prefer patterns over diary recap.
- Surface repeated open loops, not every minor task.
- Keep personal details proportionate; do not promote ephemeral noise into `wiki/`.
- Promote something into `wiki/` only if future retrieval would be useful.
- Otherwise keep the result in `output/`.

## Git Workflow

When the vault is a git repository:

1. Check `git status --short` before distilling.
2. If the repo is already dirty, review the pending changes, stage them, commit them as a pre-distillation checkpoint, and `git push origin main` before continuing.
3. After the repo is clean locally, run `git pull --rebase origin main` before editing.
4. Use `git diff -- Daily/ Output/ Wiki/` as needed to verify the distillation report and any wiki promotion.
5. If you changed files, stage only the touched distillation files, commit with a concise distillation-specific message, and `git push origin main`.
6. If nothing changed, do not create an empty commit.
7. Never force push or rewrite history from an automated distillation run.
