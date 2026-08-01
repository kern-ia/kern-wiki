---
type: Issue
title: "Translate the glossary"
description: "Write fr/ecosystem/glossary.md from the English glossary and its French column, keeping one canonical French spelling per thing and every identifier untranslated."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/56
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 06
slug: translate-glossary
size: M
status: open
gh_issue: 56
depends_on: [01, 03]
---

# Translate the glossary

## Summary

The glossary is normative from M1 ([decision](/conventions/10-terminology-and-naming.md)), and it
already carries a French column — kept from the source material at
[epic 1 issue 15](/epic-1-the-frame/issues/15-add-glossary.md) precisely so this issue is a
transposition rather than a vocabulary invention exercise.

This page matters more than its size suggests: every other French page's terminology is checked
against it, so a French term decided loosely here propagates into every translation that follows.

## Scope

- **`fr/ecosystem/glossary.md`** — the translation of `en/ecosystem/glossary.md` at the mirror path,
  same headings, same order, same term set.
- **The French column becomes the term**, and the English form is what the page records alongside it
  — the same rows, read from the other side. One canonical French spelling per thing, exactly as the
  English page holds one canonical English spelling per thing.
- **Identifiers are never translated**: brick names stay lowercase and backticked, contract
  identifiers keep their version, module paths are quoted verbatim as they exist today.
- **Aliases carry over.** Where the glossary records a repository's own term as an alias rather than
  correcting it, the French page records the same alias — including where that alias is already
  French, which the source material makes likely.
- **Any French term this PR settles is written back into the English page's French column** in the
  same PR, so the column and the French page cannot disagree.
- No `verified` stamp — the stamp is inherited from the original.

## Out of scope

- **No new terms.** A term that belongs in the glossary is added to the English page first, by the
  PR that first uses it; this PR translates the set that exists.
- **No re-definition.** If a French definition reads better than its English original, the English
  original is fixed first and then translated.
- **No French-only aliases invented for readability.**
- **No changes to the glossary column check** — [issue 03](./03-add-french-tree-validator-rules.md)
  owns it, and this page is its first real subject.

## Acceptance criteria / Definition of done

- [ ] `fr/ecosystem/glossary.md` exists at the mirror path with the same `##` headings in the same
      order as its original, and the same number of terms.
- [ ] Every term in the English glossary appears, and no term appears that is not in the English
      glossary.
- [ ] Identifiers — brick names, contract identifiers with versions, module paths, commands — are
      byte-identical to the English page.
- [ ] The English page's French column matches the French page's terms exactly, after this PR.
- [ ] The page carries no `verified` stamp.
- [ ] Every alias recorded in English is recorded in French.
- [ ] Hard-wrapped at 100 columns, tables exempt; the check suite is green including the glossary
      column rule.

## Relevant files / areas

No content exists in this repository yet — paths follow the decided layout
([specs](/specs/04-content-tree.md)) and epic 1's output, and are not verified locations:
`fr/ecosystem/glossary.md`, `en/ecosystem/glossary.md`.

## Dependencies

Blocked by [Issue 01](./01-add-fr-language-and-switch.md) and
[Issue 03](./03-add-french-tree-validator-rules.md) — the glossary column rule is what keeps this
page and the English column from drifting apart the day after this merges. Blocked by
[Epic 1](/epic-1-the-frame/EPIC_1.md) for the glossary itself. Should land before
[Issue 07](./07-translate-quickstart.md) and
[Issue 08](./08-translate-conventions-page-if-settled.md), which follow its vocabulary.

## PR size note

Target ~500 changed lines; one table-heavy page plus the column write-back. If it approaches ~1000,
the glossary has grown past what one page should hold and that is an English-side problem to raise,
not a reason to translate half of it.
