---
name: "vault-compile"
description: "Use when working in the Obsidian vault at /Vault and the user asks to compile raw notes, ingest source material, maintain the wiki, update topic indexes, or keep the master index current. This skill turns raw/ inputs into concise wiki/ articles with [[wiki links]], topic _index.md updates, and wiki/_master-index.md maintenance."
---

# Vault Compile

This skill implements the librarian workflow for the Obsidian knowledge base at `/Vault`.

Use it when the user asks to compile, ingest, process `raw/`, update `wiki/`, or maintain vault structure after new source material arrives.

## Vault model

- `raw/` is the inbox and source layer. Treat raw files as inputs, not the final knowledge product.
- `raw/Indexed/` is the processed archive inside `raw/`. Files moved there are already compiled and must not be reprocessed as new inbox items.
- `wiki/` is the maintained knowledge layer. The model owns this structure and is expected to keep it coherent.
- `output/` is for generated reports and query results, not canonical topic knowledge unless the user explicitly wants content promoted back into the wiki.
- `wiki/_master-index.md` is the top-level navigation file.
- Every topic folder inside `wiki/` must have its own `_index.md`.

## Core rules

- Read the raw source before deciding where it belongs.
- Treat only files outside `raw/Indexed/` as unprocessed inbox material.
- Keep articles concise, but match depth to the note type rather than forcing every page into the same short shape.
- Every wiki article must contain a `## Key Takeaways` section.
- Always add `[[wiki links]]` to related concepts across topics when relevant.
- If a raw source spans multiple topics, create or update articles in both places and cross-link them.
- Keep the wiki navigable through indexes first. Do not default to heavier retrieval machinery.
- Do not compress away distinctions, mechanisms, tradeoffs, or concrete examples that would matter in a future query.
- When answering questions from this vault, navigate in this order:
  1. `wiki/_master-index.md`
  2. relevant topic `_index.md`
  3. specific article files

## Compile workflow

Follow this sequence unless the user asks for a narrower edit:

1. Inspect `wiki/_master-index.md` to understand the existing topic map.
2. Identify unprocessed source files in `raw/`, excluding anything already inside `raw/Indexed/`.
3. Read the relevant raw file or files.
4. Decide whether the material belongs in an existing topic or requires a new topic folder.
5. Create or update one or more wiki articles with:
   - short `## Summary`
   - `## Key Takeaways`
   - one or more optional explanatory sections when the source warrants them, such as `## Architecture`, `## Workflow`, `## Tradeoffs`, `## Decision Criteria`, or `## Open Questions`
   - `## Related Concepts`
   - `## Source`
6. Update the topic `_index.md` with a one-line description for each article in that topic.
7. Update `wiki/_master-index.md` with every topic folder and a one-line description.
8. Add cross-links between related articles using `[[wiki links]]`.
9. After the compile succeeds, move each processed source file into `raw/Indexed/`, preserving the filename unless a collision requires a disambiguating rename.
10. Check for duplication, broken structure, or missing navigation files before finishing.

## Git workflow

When the vault is a git repository:

1. Check `git status --short` before compiling.
2. If the repo is already dirty, review the pending changes, stage them, commit them as a pre-compile checkpoint, and `git push origin main` before continuing.
3. After the repo is clean locally, run `git pull --rebase origin main` so new raw files and wiki changes are present locally.
4. Use `git diff` and `git status` during the run to review touched files and confirm the compile scope stayed tight.
5. If the compile changed files, stage only the files involved in the compile, commit with a concise compile-specific message, and `git push origin main`.
6. If nothing changed, do not create an empty commit.
7. Never force push or rewrite history from an automated compile run.

## Topic selection heuristics

- Reuse an existing topic when the source extends an established concept cluster.
- Create a new topic only when the source introduces a durable concept area that would otherwise overload an existing folder.
- Prefer stable concept topics over source-type topics. Organize by idea, not by where the note came from.
- If a source is mostly comparative, place it in the topic where the comparison is most reusable and cross-link to the neighboring topic.

## Article shape

Use concise markdown, but vary depth by note type.

- Atomic reference notes can stay around `100-200` words.
- Concept, comparison, or framework notes should usually land around `250-500` words.
- Strategy or decision notes should usually include at least one extra explanatory section beyond `Summary` and `Key Takeaways`.
- Prefer bullets by default, but use a short prose paragraph when it preserves meaning better than fragmented bullets.

A typical article should look like this:

```md
# Title

## Summary

- Short bullets summarizing the source or concept.

## Key Takeaways

- Durable points worth preserving for future queries.

## Architecture

- Optional section for concept-heavy notes.

## Related Concepts

- [[topic-a/article-a|Article A]]
- [[topic-b/article-b|Article B]]

## Source

- `raw/path/to/source.md`
```

## Index standards

### Topic `_index.md`

- Title should be the topic name in readable form.
- List every article in the topic with a one-line description.
- Include a `## Related Topics` section when cross-topic navigation helps.

### `wiki/_master-index.md`

- Must list every topic folder in `wiki/`.
- Each entry should have exactly one short description focused on what the topic covers.
- Keep descriptions oriented toward retrieval, not source provenance.

## Cross-linking rules

- Link concepts, not just matching words.
- Prefer a few strong links over noisy link stuffing.
- Add links across topics when they reduce future rereading.
- If you create a new topic, ensure at least one existing topic links to it or it links back out.

## Duplicate and update rules

- Before creating a new article, search the topic folder for overlapping concepts.
- If the concept already exists, update the existing page instead of creating a near-duplicate.
- If two files overlap heavily but serve different purposes, make the distinction explicit in their summaries and cross-links.
- Keep sources traceable in the `## Source` section. After compile, reference the exact archived path in `raw/Indexed/` when that is the file's final location.

## Audit pass after compile

Before finishing a compile task, quickly check:

- every touched article has `## Key Takeaways`
- every touched topic has an `_index.md`
- `wiki/_master-index.md` reflects any new topic
- newly created articles are linked from at least one index
- related pages have meaningful `[[wiki links]]`
- each successfully processed source has been moved into `raw/Indexed/`

## Boundaries

- Do not rewrite the raw source in full.
- Do not create speculative topics with no durable use.
- Do not move canonical wiki content into `output/`.
- Do not answer user questions from memory when the answer should come from vault navigation.
- Do not treat files already in `raw/Indexed/` as new compile targets unless the user explicitly asks to revisit archived sources.

## Rationale

This workflow follows the curated markdown wiki pattern described by the vault's own notes:

- the wiki is the durable asset, not the chat session
- indexes and summaries are the primary retrieval layer
- maintenance compounds over time through compile and audit loops
- human-readable markdown is preferred over opaque retrieval storage for this vault size
