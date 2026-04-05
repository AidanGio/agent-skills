---
name: "vault-audit"
description: "Use when working in the Obsidian vault at /Vault and the user asks to audit, lint, review, or clean up the wiki structure. This skill checks wiki integrity, index coverage, cross-links, duplicate concepts, article quality, and compile backlog in raw/ versus raw/Indexed/."
---

# Vault Audit

This skill audits the librarian-maintained Obsidian knowledge base at `/Vault`.

Use it when the user asks to audit, lint, review, clean up, or assess the health of the wiki.

## Vault model

- `raw/` is the inbox for unprocessed source material.
- `raw/Indexed/` is the processed archive. Files there should not be treated as new compile inputs.
- `wiki/` is the durable knowledge layer and should stay structurally coherent.
- `output/` is for generated reports and ad hoc deliverables, not the primary topic map.
- `wiki/_master-index.md` is the top-level navigation layer.
- Each topic folder inside `wiki/` must have its own `_index.md`.

## Audit goals

The audit should surface issues that make the vault harder to navigate, trust, or maintain.

Prioritize:

- broken or missing indexes
- missing `## Key Takeaways`
- orphan pages that are not reachable through indexes
- weak or missing `[[wiki links]]`
- duplicate or overlapping concept pages
- stale topic structure or poor topic naming
- topics that should be merged, split, or renamed for better retrieval
- raw files outside `raw/Indexed/` that appear uncompiled
- compiled pages whose `## Source` trail is missing or inconsistent

## Audit workflow

Follow this order unless the user asks for a narrower review:

1. Read `wiki/_master-index.md`.
2. Enumerate topic folders in `wiki/` and confirm each has an `_index.md`.
3. Compare topic folders against entries in `wiki/_master-index.md`.
4. Inspect each topic `_index.md` and confirm its listed articles actually exist.
5. Inspect articles in touched topics for:
   - `## Key Takeaways`
   - concise bullet-heavy structure
   - meaningful `## Related Concepts`
   - valid `## Source`
6. Look for orphan pages that are not linked from a topic `_index.md`.
7. Look for related pages that should cross-link but do not.
8. Look for duplicate or near-duplicate concept pages that should be merged, split, or clarified.
9. Review topic boundaries and names:
   - identify topics that are too broad and should be split
   - identify topics that are too thin or overlapping and should be merged
   - identify topic names that no longer match their actual contents
10. Check `raw/` for files outside `raw/Indexed/` that appear not to have been compiled yet.
11. Summarize the highest-value fixes. If the fix is mechanical and low risk, apply it directly.

## What counts as a finding

Report findings when they affect retrieval quality, maintenance quality, or trustworthiness.

Examples:

- a topic exists in `wiki/` but is missing from `wiki/_master-index.md`
- an article exists in a topic folder but is missing from the topic `_index.md`
- an article has no `## Key Takeaways`
- a topic has multiple pages covering the same concept with unclear differentiation
- two topic folders cover the same concept cluster and should be merged
- a topic has become a grab bag and should be split into clearer subtopics
- a topic name no longer reflects the material it contains
- a comparison page has no links to the topics it compares
- a raw source is still in `raw/` even though the wiki clearly absorbed it

## Fix policy

Apply fixes directly when they are straightforward and low risk:

- add missing `_index.md` references
- update `wiki/_master-index.md`
- add missing `## Key Takeaways`
- add a small number of strong `[[wiki links]]`
- clarify article descriptions in indexes
- recommend topic merges, splits, or renames when the structure is the real problem

Do not make large conceptual rewrites unless the user asks for them.

## Output shape

Prefer a concise audit report with findings ordered by impact.

For each finding, include:

- what is wrong
- why it matters
- the affected file or topic
- whether you fixed it or are recommending a follow-up

If there are no major issues, say so explicitly and mention any minor maintenance gaps.

## Heuristics

- Treat navigation quality as the primary standard. If a future query would struggle to find or trust a note, that is an audit issue.
- Prefer strong conceptual links over many shallow links.
- Prefer updating an existing topic structure over creating new topics during an audit, unless the current organization is clearly broken.
- Recommend a merge when two topics force the same retrieval path or duplicate the same concepts.
- Recommend a split when a topic is broad enough that its `_index.md` no longer acts as a useful filter.
- Recommend a rename when the current topic name hides the actual concept cluster a future query would look for.
- Distinguish between "missing coverage" and "not yet worth its own page." Do not create filler content.

## Boundaries

- Do not reprocess files already in `raw/Indexed/` as if they were new inbox material.
- Do not move files from `raw/Indexed/` back into `raw/`.
- Do not rewrite raw source documents in full.
- Do not create speculative articles just to eliminate every gap.
- Do not answer from memory when the correct action is to inspect the vault.

## Relationship to compile

Use `vault-audit` to assess structure and maintenance quality.

Use `vault-compile` when the work involves processing raw source material into canonical wiki pages.
