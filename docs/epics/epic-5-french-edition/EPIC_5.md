---
type: Epic
title: "French edition"
description: "Add the fr/ tree and a language switch, translating the stable front-door pages only."
tags: [epic]
timestamp: 2026-08-01T02:00:05Z
epic: 5
slug: french-edition
status: draft
gh_issue: null
milestone: null
source: docs/planning/SCOPE.md#milestone-5-french-edition
---

# Epic 5: French edition

## Goal

The published site is bilingual EN/FR. English is the source language, so this epic adds the second
half — without committing the project to translating pages that are still moving.

## Scope

- The **`fr/` tree** and a **language switch**. The `en/` tree from
  [Epic 1](/epic-1-the-frame/EPIC_1.md) exists precisely so that adding `fr/` moves no files.
- Translation of the **stable front-door pages only**:
  - overview
  - ecosystem diagram
  - glossary
  - quickstart
  - the conventions page, **if it has settled** by then

**Gaps between the two languages are acceptable; contradictions are not.**

## Out of scope

- **No French translation of per-brick technical documentation** while the packages move — the
  [Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md) sections are deliberately excluded.
  *Deferred.*
- **No French page without an English original.** Not a deferral — a rule.
- The conventions page is translated only if it has settled; if it has not, it stays English and
  waits.

## Acceptance criteria

10. **Every French page has an English original and says the same thing.**

## Dependencies

Depends on [Epic 1](/epic-1-the-frame/EPIC_1.md) for the `en/` tree and for every front-door page
being translated (overview, diagram, glossary, quickstart).

Depends on [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md) **only** for the conventions
page, and only if that page has settled — otherwise this epic ships without it.

## Context

- [Technical specs](../../planning/SPECS.md)
- [Conventions](../../planning/CONVENTIONS.md)

## Notes

**Project-wide constraints relevant here:**

- **English is the source language; the published site is bilingual EN/FR.** This is the constraint
  this epic exists to satisfy, and the ordering rule (English first, always) is not negotiable.
- **No invented content** — a translation that fills in a placeholder is invented content in the
  other language.
- **Plain markdown, generator-agnostic** — the language switch must not make pages unreadable on
  GitHub.
- **Zero budget** — no translation service; GitHub-native only.

**Why this is last:** translating pages that are still churning doubles the churn. Restricting this
epic to the stable front door is the mitigation for the doc-churn risk that
[Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md) accepts on purpose.
