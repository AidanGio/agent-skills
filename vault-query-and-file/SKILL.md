---
name: "vault-query-and-file"
description: "Use when working in the Obsidian vault at /Vault and the user asks a question that should be answered from the wiki, or when a useful answer should be filed back into the knowledge base. This skill navigates the wiki by indexes first, answers from compiled notes, and decides whether to file the result into wiki/ or output/."
---

# Vault Query And File

This skill handles question answering and durable filing for the librarian-maintained Obsidian knowledge base at `/Vault`.

Use it when the user asks for an answer based on the vault, asks for a report from the wiki, or wants useful outputs filed back into the system.

## Vault model

- `wiki/` is the canonical knowledge layer.
- `output/` is for query results, reports, and generated deliverables.
- `raw/` is source inbox material and should not be treated as the first stop for answering normal questions.
- `wiki/_master-index.md` is the starting point for retrieval.
- Each topic `_index.md` narrows the search to the right article set.

## Query workflow

Always navigate the vault in this order:

1. Read `wiki/_master-index.md`.
2. Choose the most relevant topic or topics.
3. Read the topic `_index.md` files.
4. Read the specific article files needed to answer the question.
5. Answer from the compiled wiki, not from memory.

If the wiki is missing an obvious durable concept needed for the answer:

- prefer updating or creating a wiki article when the missing concept is reusable
- prefer `output/` when the result is mostly one-off analysis or a user-specific deliverable

## Filing decision

After answering, decide whether the result should be filed.

### File into `wiki/` when

- the answer creates durable knowledge worth reusing later
- the answer clarifies a concept, comparison, pattern, or workflow
- the answer resolves an ambiguity that future queries are likely to hit again
- the answer improves topic coverage rather than only serving the current request

### File into `output/` when

- the result is a one-off report, memo, synthesis, or deliverable
- the answer is temporary, highly situational, or tied to a specific moment
- the user asks for a report rather than a canonical note

### File into both when

- the user asked a specific question that produces a one-off report, but the process also surfaces a durable concept worth preserving in the wiki

## Wiki filing rules

When filing into `wiki/`:

- reuse an existing topic when possible
- create a new topic only when the concept is durable and distinct
- write concise bullet-heavy pages
- include:
  - `## Summary`
  - `## Key Takeaways`
  - `## Related Concepts`
  - `## Source`
- update the topic `_index.md`
- update `wiki/_master-index.md` if a new topic is created
- add strong `[[wiki links]]`

## Output filing rules

When filing into `output/`:

- write a concise markdown report
- prefer descriptive filenames over generic names
- include enough context that the file is useful without reopening the entire chat
- avoid turning `output/` into a second wiki

## Answer quality rules

- Be explicit about what came from the wiki and what is an inference.
- Prefer concise synthesis over long quotation.
- If the wiki has conflicting or thin coverage, say so.
- Do not pretend the vault contains evidence it does not contain.

## Heuristics

- Default to `wiki/` for concepts and `output/` for deliverables.
- A good test: if a future version of you would benefit from finding this answer again through topic navigation, it likely belongs in `wiki/`.
- If the best reusable unit is smaller than the full answer, file only that smaller durable insight into the wiki and keep the full response in `output/` or chat.
- Prefer updating an existing page over creating a near-duplicate note.

## Boundaries

- Do not bypass `wiki/_master-index.md` when the user asked for a vault-grounded answer.
- Do not answer from memory when the vault should be consulted.
- Do not file every answer into the wiki; avoid noise.
- Do not promote temporary or weakly supported claims into canonical notes.

## Relationship to other skills

- Use `vault-compile` when the job is to turn raw source material into wiki knowledge.
- Use `vault-audit` when the job is to inspect the health of the structure.
- Use `vault-query-and-file` when the job is to answer from the wiki and preserve durable results.
