---
type: Epic
title: "Conventions & contribution surface"
description: "Turn the frame's conventions into a contributor-facing surface, so several people fill the wiki the same way."
tags: [epic]
timestamp: 2026-08-01T02:00:05Z
epic: 2
slug: conventions-contribution-surface
status: draft
gh_issue: null
milestone: null
source: docs/planning/SCOPE.md#milestone-2-conventions--contribution-surface
---

# Epic 2: Conventions & contribution surface

## Goal

Nothing today tells a newcomer how to contribute to Kern. There are two contributors already and
more expected, and their first need is *how to write in this wiki*, not how to get access.

The rules come **before** the bulk writing, deliberately. Several people fill the frame built in
[Epic 1](/epic-1-the-frame/EPIC_1.md), and it only holds if they fill it the same way — consistency,
not capacity, is the binding constraint. A wiki filled three different ways decays regardless of
effort spent.

Serves journey **J4** (make a first contribution).

## Scope

- **How to write here** — the templates, maturity markers, version stamps and the
  no-invented-content rule, turned into a **review checklist**. Epic 1 *decides* these conventions;
  this deliverable makes them usable by someone who wasn't there when they were decided.
- **Contribution process** — setup, conventions, how a change lands, where to open an issue.
- **Brick-authoring guide** — what makes something a `kern-*` brick, including the exposed/needs
  declaration a new package must publish.
- **How to add a contract entry** when the next contract arrives.
- **Canonical naming rule** — lowercase `kern-*`, with today's real repo names noted where they
  differ, plus **one follow-up issue per repo** for the mismatches. The issues are the deliverable;
  the renames themselves are not.

## Out of scope

- **No writes to `kern-ia/.github`** — no CONTRIBUTING.md, no code of conduct, no security policy,
  no issue or PR templates in that repo. It is not yet in a state its owners can vouch for.
  *Deferred.* This epic serves J4 entirely from wiki pages.
- **No repo renames and no Go module-path migration.** This epic writes the naming *rule* and opens
  the follow-up issues; the breaking changes stay owned by each repo. *Deferred.*
- **No changes to brick code.** *Rejected.*
- Filling the per-brick technical sections is
  [Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md).

## Acceptance criteria

6. **Uniformity** — another contributor adds or fills a page matching the templates **without
   asking how**.

## Dependencies

Depends on [Epic 1](/epic-1-the-frame/EPIC_1.md): the templates, maturity markers, placeholder
convention and version stamps must exist before they can be written up as rules and a checklist.

Should land before the bulk of [Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md) — that
is the whole reason this milestone comes second rather than after the writing.

## Context

- [Technical specs](../../planning/SPECS.md)
- [Conventions](../../planning/CONVENTIONS.md)

## Notes

**Project-wide constraints relevant here:**

- **No invented content, in any form** — the rule this epic's checklist exists to enforce.
- **Consistency, not capacity, is the binding constraint**, and **the wiki must absorb a new package
  without restructuring** — the brick-authoring guide and the contract-entry guide are what make
  that true for people rather than only for the file layout.
- **English is the source language** — the conventions page is translated in
  [Epic 5](/epic-5-french-edition/EPIC_5.md) only if it has settled by then.
- **Zero budget** — GitHub-native tooling only.

**Accepted risk:** contributors will find no `CONTRIBUTING.md` where GitHub shows one, because
`.github` is out of scope. J4 is therefore served by a site page that GitHub's own affordances will
not surface. Accepted, not mitigated.

**Assumption:** two contributors today, more expected. This was corrected mid-planning and is what
re-based the constraints onto consistency — if the contributor count turns out to be one, this
epic's urgency drops but its content does not change.
