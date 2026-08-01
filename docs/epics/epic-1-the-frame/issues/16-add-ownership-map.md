---
type: Issue
title: "Add the ownership map"
description: "Publish the subject → authoritative home table, so no wiki page silently competes with the repo that owns its subject."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/21
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 16
slug: add-ownership-map
size: S
status: open
gh_issue: 21
depends_on: [13]
---

# Add the ownership map

## Summary

Deliverable 12, and the mitigation for the epic's second risk: the wiki duplicates content against
upstreams that move weekly, so the failure mode is not a dead link but a page that is confidently
wrong. The ownership map states, per subject, which home is authoritative — which is what
acceptance criterion 5 (*no page contradicts the repo docs on the same subject*) is checked against.

## Scope

- `en/ecosystem/ownership.md` — the subject → authoritative home table from the scope, as a page:
  which subjects live in the wiki, which live in a brick repo, and which live in both with the repo
  winning.
- The rule stated explicitly for each row: when the two disagree, which one a reader should believe,
  and where to open the issue.
- The categories the scope already settled — architecture notes, dev logs, retros and changelogs
  stay in their repos; API reference stays on `pkg.go.dev`; the ecosystem view, the contracts
  registry, the quickstart and the glossary are the wiki's.
- A pointer to it from the ecosystem section page and from the repository README's "how to add a
  page" section.

## Out of scope

- **No writes to any brick repo**, and no issues opened against them here. Findings become issues on
  the brick — that is epic 2's naming follow-ups and epic 4's open questions.
- **No re-hosting decision changes.** This page records the ownership already decided in scope; it
  does not relitigate it.
- **No hand-written API reference** — `pkg.go.dev` regenerates it per commit.
- No `kern-ia/.github` content of any kind.

## Acceptance criteria / Definition of done

- [ ] Every subject the wiki documents appears in the table with exactly one authoritative home.
- [ ] Each row names where to raise a disagreement.
- [ ] Nothing in the table asserts what a repo contains without that having been checked and cited.
- [ ] The ecosystem section page links it.
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/ecosystem/ownership.md`, linked from
`en/ecosystem/_index.md` and `README.md`.

Source: the ownership table in [the scope](../../../planning/SCOPE.md), plus the actual repositories
for what each currently documents.

## Dependencies

Blocked by [Issue 13](./13-write-home-and-ecosystem-overview.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
