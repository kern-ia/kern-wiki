---
type: Issue
title: "Translate the home page and the ecosystem overview"
description: "Write fr/_index.md and fr/ecosystem/_index.md as transpositions of their English originals, diagram included, with identifiers and Mermaid node names left untranslated."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/55
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 05
slug: translate-home-and-ecosystem-overview
size: M
status: open
gh_issue: 55
depends_on: [01, 03]
---

# Translate the home page and the ecosystem overview

## Summary

The first two front-door pages, and the two a French reader hits first: what Kern is, and how the
bricks relate. The ecosystem overview carries the Mermaid diagram
([epic 1 issue 14](/epic-1-the-frame/issues/14-add-ecosystem-diagram.md)), so translating it means
deciding what in a diagram is prose and what is an identifier — which is why the two pages travel
together rather than the diagram being split off: a page is not split across pull requests
([decision](/conventions/05-pr-size-and-unit.md)).

Translation is transposition, not adaptation ([decision](/conventions/13-translation-authoring.md)).
Same path, same headings, same order, same claims — a French page that improves on its original is a
contradiction with extra steps.

## Scope

- **`fr/_index.md`** — the translation of `en/_index.md` at the mirror path.
- **`fr/ecosystem/_index.md`** — the translation of `en/ecosystem/_index.md`, including the Mermaid
  diagram.
- **In the diagram, only labels and the legend are translated.** Node identifiers, brick names and
  contract identifiers stay verbatim, and the dashed-line convention for planned or missing edges is
  carried over with its legend node ([decision](/specs/08-diagrams.md)). The diagram must render on
  GitHub in both trees.
- **Stamps are inherited, not re-earned**: no `verified` block on either French page. The translator
  did not read the code.
- **Glossary terms follow the glossary's French column**, and first use on a French page links the
  French glossary target once ([decision](/conventions/10-terminology-and-naming.md)).
- Links are rewritten to their French mirror paths where a French counterpart is intended, and
  otherwise point at the English page — the stub covers what does not exist yet.
- **Anything untrue in the English original is fixed in `en/` first**, in this PR or before it, and
  then translated. Never fixed only in French.

## Out of scope

- **No new content.** A French page that says something its original does not is invented content in
  the other language, and it is the failure this epic exists to avoid.
- **No omissions either.** A page is translated whole or absent; the stub covers absent
  ([issue 02](./02-add-untranslated-stub-layout.md)).
- **No translated identifiers** — brick names, contract identifiers, module paths, commands, code
  blocks and their comments stay as they are.
- **No French-only navigation or landing structure.** The trees mirror.
- **No `verified` stamp**, and no second version claim of any kind.

## Acceptance criteria / Definition of done

- [ ] Both pages exist at their mirror paths and every `##` heading matches its original in set and
      in order — the heading parity rule from
      [issue 03](./03-add-french-tree-validator-rules.md) passes.
- [ ] Neither page carries `verified`.
- [ ] Every claim on the French page is present on the English page, and every claim on the English
      page is present on the French one.
- [ ] The Mermaid diagram renders in the French tree and on GitHub, with identifiers untranslated and
      the legend translated.
- [ ] Every French term used that is not already in the glossary's French column is added to the
      glossary in this PR.
- [ ] The language switch lands on the counterpart in both directions, from both pages.
- [ ] Hard-wrapped at 100 columns; no shortcodes, no raw HTML beyond `<br>` and comments.
- [ ] `hugo --gc --minify` passes with warnings fatal and the full check suite is green.

## Relevant files / areas

No content exists in this repository yet — paths follow the decided layout
([specs](/specs/04-content-tree.md)) and epic 1's output, and are not verified locations:
`fr/_index.md`, `fr/ecosystem/_index.md`, and their originals `en/_index.md`,
`en/ecosystem/_index.md`.

## Dependencies

Blocked by [Issue 01](./01-add-fr-language-and-switch.md) and, in practice, by
[Issue 03](./03-add-french-tree-validator-rules.md) — the first translation should be checked by the
rules rather than retrofitted to them. Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) for both
originals and the diagram.

## PR size note

Target ~500 changed lines; two prose pages plus a diagram. If it approaches ~1000, the English
originals are larger than expected and the diagram page can move to its own PR — but only if the
diagram then leaves `en/ecosystem/_index.md`, which it does not, so prefer trimming nothing and
accepting the size.
