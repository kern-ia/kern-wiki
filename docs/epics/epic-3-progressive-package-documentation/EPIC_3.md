---
type: Epic
title: "Progressive package documentation"
description: "Fill each brick's section against the template — install, configuration, usage, examples, integration — replacing placeholders as knowledge settles."
tags: [epic]
timestamp: 2026-08-01T02:00:05Z
epic: 3
slug: progressive-package-documentation
status: draft
gh_issue: null
milestone: null
source: docs/planning/SCOPE.md#milestone-3-progressive-package-documentation
---

# Epic 3: Progressive package documentation

## Goal

A developer should be able to install, configure and use a single Kern brick in their own Go
project **from the wiki alone** — including the narrower case of someone who wants one brick and
doesn't care about the ecosystem. Today that knowledge is inside each repo, written for someone
already there.

This is the largest milestone, and the one that turns the frame from
[Epic 1](/epic-1-the-frame/EPIC_1.md) into a wiki that is actually useful to adopters.

Serves journey **J6** (adopt one brick).

## Scope

Fill each brick's section against the brick template:

- **Install**
- **Configuration**
- **Usage patterns**
- **Worked examples**
- **Integration over the `kern.*` contracts**

replacing placeholders as knowledge settles, and covering the **fifth package** once it lands.

**Operational traps** — these only surface in production and must **not** be footnotes:

- `kern-orch serve` under an empty service environment loses `HOME` and API keys, and fails as
  silent in-band "no API key" errors.
- `kern-link`'s OAuth flows impersonate first-party clients, which its own docs warn gets accounts
  revoked in long-running daemons — so **API keys only** for daemon mode.

**Expect this epic to be cut roughly one brick at a time.** A section that is half placeholders and
wholly true is a valid end state.

## Out of scope

- **No hand-written API reference** — `pkg.go.dev` regenerates it per commit, and it is never
  re-typed by hand. *Rejected.*
- **No re-hosting of repo internals** — internal architecture, dev logs, retros and changelogs stay
  in their repos. *Rejected.*
- **No changes to brick code** — anything found while documenting becomes an issue on the brick.
  *Rejected.*
- **No French translation of per-brick technical documentation** while the packages move.
  *Deferred* — deliberately excluded from [Epic 5](/epic-5-french-edition/EPIC_5.md).
- **No completeness target.** *Rejected* — there is no "all placeholders filled" finish line here.
- Design rationale for `kern-link` — it stays a tracking port of `@earendil-works/pi-ai`, so its
  section documents **usage** and points upstream for design.

## Acceptance criteria

7. **Adoption** — a developer installs, configures and uses one brick in their own Go project from
   its wiki section alone.
8. Every technical page carries its **version stamp**.

Both of the operational traps above are documented as first-class content, not footnotes.

## Dependencies

Depends on [Epic 1](/epic-1-the-frame/EPIC_1.md) — the brick template, the maturity markers and the
contracts registry are the slots this epic fills.

Should follow [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md): several people write
these sections, and the conventions exist so they write them the same way.

## Context

- [Technical specs](../../planning/SPECS.md)
- [Conventions](../../planning/CONVENTIONS.md)

## Notes

**Project-wide constraints relevant here:**

- **No invented content, in any form** — no configuration inferred rather than checked, nothing
  planned described as existing. The highest-risk epic for this rule, because it is the one writing
  concrete technical claims.
- **Upstreams move weekly and are pre-1.0** — anything asserted about internals is stale by default.
- **Ownership map**: install / configure / use / integration / examples are the **wiki's** to own;
  API signatures belong to `pkg.go.dev`, internal architecture and release history belong to the
  repos, and the `kern.*` contract JSON fixtures belong to the repos, CI-enforced.
- **English is the source language** (and these pages stay English-only — see out of scope).

**Risks:**

- **Doc churn from documenting moving packages** — a deliberate bet, mitigated by stability banners
  and by not translating these pages.
- **Inconsistent module paths** — `github.com/julienlegoux/kern-link`, `github.com/yoann/kern-orch`;
  neither matches `kern-ia`. **Any `go get` line written in this epic is wrong or will be.**
  Mitigated by documenting the current paths verbatim; the migration is flagged in
  [Epic 4](/epic-4-project-map-freshness/EPIC_4.md).
- **Scope drifts into brick work** — mitigated by the no-brick-code rule: findings become issues on
  the brick.

**Assumptions:**

- Each package's public surface is stable enough that usage docs written now survive weeks, not
  days. **If this is wrong, split this epic per brick and postpone the least stable one.**
- The ecosystem will grow during the project — a fifth package is in progress and its name, role and
  contracts are unknown to this plan. Certain rather than assumed.
