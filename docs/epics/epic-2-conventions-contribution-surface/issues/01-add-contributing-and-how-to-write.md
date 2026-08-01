---
type: Issue
title: "Add the contributing section and the \"how to write here\" page"
description: "Create en/contributing/ and the page that renders the wiki's authoring rules — templates, gap blocks, maturity markers, voice and terminology — for someone who wasn't there when they were decided."
tags: [epic-2]
resource: https://github.com/kern-ia/kern-wiki/issues/30
timestamp: 2026-08-01T12:30:00Z
epic: 2
issue: 01
slug: add-contributing-and-how-to-write
size: M
status: open
gh_issue: 30
depends_on: []
---

# Add the contributing section and the "how to write here" page

## Summary

The epic's first deliverable, and the one every other issue in it hangs off. Epic 1 *decides* the
conventions and encodes half of them in `data/vocab.yaml` and the validator; this page makes them
usable by a contributor who wasn't there when they were decided.

[CONVENTIONS.md](../../../planning/CONVENTIONS.md) is the source and this page is its rendering —
where the two overlap, CONVENTIONS wins, and **a rule that exists only here is a bug to fix there**.
Neither restates the validator: anything mechanically enforced is written as *CI checks this*, so a
rule has one place to rot.

This issue also creates the section itself, since `en/contributing/` does not exist after epic 1.

## Scope

- `en/contributing/_index.md` — the section page: what lives here, and a one-line pointer to each
  of the other pages this epic adds (`type: Guide` or whatever the vocabulary settled for section
  pages).
- `en/contributing/how-to-write.md` — the authoring rules, rendered for a contributor:
  - **Start from a template.** `templates/brick.md` and `templates/contract.md` are copyable; the
    section set and their order are binding, everything below `###` is free.
  - **The gap block**, verbatim and greppable, placed inside the section that has nothing true to
    say. A section is never deleted — a missing section and an unwritten one must not look the same.
  - **The three fields, kept distinct**: `maturity` describes the code, `doc_state` describes the
    page, `timestamp` describes the file — with the closed values of each and what picking each one
    commits you to.
  - **The provisional banner**, verbatim, and why `works-today` and `planned` carry none.
  - **The no-invented-content rule at sentence level**: nothing is described from its name;
    uncertainty is a placeholder, never a hedge; every version-specific statement names its version.
  - **Voice**: second person for instructions, present tense, no first person, no marketing
    register, descriptive headings — with the reason for the last one (they get translated, and a
    clever heading makes the two languages unverifiable against each other).
  - **Terminology**: lowercase backticked brick names, contracts always with their version, module
    paths quoted verbatim as they exist today, first use links the glossary, and a term not in the
    glossary is added to it in the PR that first uses it.
  - **The markdown contract**: what is allowed, and that shortcodes, MDX and raw HTML are CI-failed.
  - Hard-wrap at 100 columns.
- Links out to the pages that carry the rest: verification and the checklist
  ([Issue 02](./02-add-verification-and-review-checklist.md)), the process
  ([Issue 03](./03-add-contribution-process-page.md)).

## Out of scope

- **No stamping, citation or review-checklist content** — that is
  [Issue 02](./02-add-verification-and-review-checklist.md). This page stops at *what a page looks
  like*; that one covers *when it is true enough to stamp*.
- **No setup or process instructions** — [Issue 03](./03-add-contribution-process-page.md).
- **No new conventions.** If writing this page surfaces a rule that is missing, undecided or wrong,
  the fix lands in [CONVENTIONS.md](../../../planning/CONVENTIONS.md) first and is rendered here
  second.
- **No validator or `vocab.yaml` changes** beyond adding the section's own `type` entry if the
  vocabulary settled in epic 1 has no fitting one — and if it does need one, it comes with its
  required-heading list and a `tools/testdata/` fixture in the same PR.
- **No French translation** — [Epic 5](/epic-5-french-edition/EPIC_5.md), and only if this page has
  settled by then.
- No `kern-ia/.github` content of any kind.

## Acceptance criteria / Definition of done

- [ ] `en/contributing/_index.md` exists and every page this epic adds is reachable from it.
- [ ] Every rule on the page traces to a section of
      [CONVENTIONS.md](../../../planning/CONVENTIONS.md); none contradicts it.
- [ ] The gap block and the provisional banner are quoted **byte-identical** to the strings in
      `templates/` and in CONVENTIONS — a paraphrase here silently breaks the greppability the whole
      convention rests on.
- [ ] Mechanically enforced rules are marked *CI checks this* rather than re-explained.
- [ ] The page itself obeys what it describes: template order, glossary terms, voice, 100-column
      wrap, no shortcodes.
- [ ] `hugo --gc --minify` builds with warnings fatal; `validate` passes; generated listings
      regenerate clean.

## Relevant files / areas

No existing content for this yet — paths follow the decided tree in
[SPECS.md](../../../planning/SPECS.md), not verified against this repository:
`en/contributing/_index.md`, `en/contributing/how-to-write.md`.

Sources to render, not to re-decide: [CONVENTIONS.md](../../../planning/CONVENTIONS.md) §Writing the
wiki, and `templates/` plus `data/vocab.yaml` as epic 1 leaves them.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) — specifically its templates and vocabulary
(Issue 04) and the page-structure checks (Issue 08); there is nothing to write up until those exist.

Blocks every other issue in this epic: they all live in the section this one creates.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
