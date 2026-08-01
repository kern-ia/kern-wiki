---
type: Issue
title: "Translate the quickstart"
description: "Write fr/integration/quickstart.md and its section page as transpositions, with every command, module path and code comment left verbatim and the English original's stamp inherited rather than re-earned."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/57
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 07
slug: translate-quickstart
size: M
status: open
gh_issue: 57
depends_on: [01, 03, 06]
---

# Translate the quickstart

## Summary

The quickstart is the page the scope measures in minutes rather than in words, and the only
front-door page whose content was verified by being run
([epic 1 issue 23](/epic-1-the-frame/issues/23-write-verified-quickstart.md)). That makes its
translation the sharpest test of two rules at once: identifiers are never translated, and stamps are
inherited rather than re-earned.

A translated quickstart whose commands were "helpfully" localized is a page that fails the first
time someone follows it — the exact failure the wiki's fifteen-minutes-to-a-hello-graph budget
exists to prevent.

## Scope

- **`fr/integration/quickstart.md`** — the translation of `en/integration/quickstart.md` at the
  mirror path.
- **`fr/integration/_index.md`** — the section page, translated with the page it introduces. A
  section page is a handful of navigational lines, and serving a stub at section level while its only
  child is translated reads as a broken tree rather than as an honest gap.
- **Commands, module paths, output samples and code comments stay verbatim.** Only prose around them
  is translated. Module paths are quoted as they exist today, never normalized to what they ought to
  become.
- **The original's `verified` stamp is inherited, not copied**: the French page carries no `verified`
  block of its own, and the reader sees the original's version claim through the mechanism, not
  through a second assertion.
- Prerequisites, versions and any *"tested on"* statement are transposed exactly — a version-specific
  statement names its version in both languages, and it is the same version.
- Glossary terms follow the French column settled in
  [issue 06](./06-translate-glossary.md).

## Out of scope

- **No re-running of the quickstart to re-verify it**, and no French stamp resulting from having run
  it. If someone does run it and finds it broken, that is a `fix:` to the English page first.
- **No localized commands, paths, environment variables or example names.**
- **No French-only troubleshooting notes**, however useful — the English page gets them first.
- **No adaptation of the walkthrough's ordering or examples** to a different audience.
- **No other page under `integration/`** — the cross-brick guides are not front-door pages and stay
  English, served as stubs.

## Acceptance criteria / Definition of done

- [ ] Both files exist at their mirror paths, with `##` headings matching their originals in set and
      order.
- [ ] Every command, module path, code block and code comment is byte-identical to the English
      original — verified by diffing the fenced blocks, not by reading.
- [ ] Neither file carries `verified`; the version the quickstart was verified against is visible to
      a French reader through the inherited stamp.
- [ ] Every version named in the English page is named, identically, in the French one.
- [ ] The language switch lands on the counterpart in both directions.
- [ ] No claim appears in French that is absent in English, and none is dropped.
- [ ] Hard-wrapped at 100 columns, fenced blocks exempt; the check suite is green.

## Relevant files / areas

No content exists in this repository yet — paths follow the decided layout
([specs](/specs/04-content-tree.md)) and epic 1's output, and are not verified locations:
`fr/integration/quickstart.md`, `fr/integration/_index.md`, `en/integration/quickstart.md`.

## Dependencies

Blocked by [Issue 01](./01-add-fr-language-and-switch.md) and
[Issue 03](./03-add-french-tree-validator-rules.md). Blocked by
[Issue 06](./06-translate-glossary.md) for the French vocabulary this page uses. Blocked by
[Epic 1](/epic-1-the-frame/EPIC_1.md) for the verified English quickstart.

## PR size note

Target ~500 changed lines; one walkthrough page plus a short section page. Code blocks are copied
rather than written, so the reviewable surface is smaller than the diff.
