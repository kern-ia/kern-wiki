---
type: Epic
title: "The frame"
description: "Build the information architecture, templates and conventions the wiki's documentation lands in, plus every page writable truthfully today."
tags: [epic]
resource: https://github.com/kern-ia/kern-wiki/issues/1
timestamp: 2026-08-01T02:20:00Z
epic: 1
slug: the-frame
status: open
gh_issue: 1
milestone: 1
source: docs/planning/SCOPE.md#milestone-1-the-frame
---

# Epic 1: The frame

## Goal

`github.com/kern-ia` says nothing about what Kern is. Each brick repo documents itself well *for
someone already inside it* — nothing documents the ecosystem. This epic makes Kern comprehensible
from one place.

The ecosystem is two weeks old, its target architecture is not settled, and packages are still
arriving. So this epic does not try to write the documentation — it builds **the frame
documentation lands in**: an information architecture, page templates, a contracts registry and a
placeholder convention, filled progressively as things settle. Everything downstream (epics 2–5)
fills or maintains this frame; nothing else can start until it exists.

Serves journeys **J1** (understand Kern in 60 seconds), **J2** (run the ecosystem end to end) and
**J3** (pick the right brick).

## Scope

The information architecture and conventions, plus every page writable truthfully today. English
only. Thirteen deliverables:

- **Repo initialized** — `kern-ia/kern-wiki`, plain markdown, an `en/` tree so adding `fr/` later
  moves no files, and a repo README explaining how to add a page.
- **GitHub Pages publishing** on push to the default branch.
- **Information architecture** — sections (ecosystem · bricks · contracts · integration ·
  contributing · status) designed so that a new brick or a new contract *fills a slot* rather than
  forcing a redesign.
- **Page templates** — a **brick template** (identity, maturity, exposed / needs, install,
  configuration, usage, integration, version stamp) and a **contract template** (purpose, producer,
  consumer, versions, enforcement status, fields, migration). The exposed/needs block follows the
  convention `Kern-UI`'s README already states.
- **The placeholder & maturity convention** — the markers *works today* / *provisional* /
  *planned*, explicit "not documented yet" blocks, and the no-invented-content rule. **This is the
  deliverable not to cut under time pressure**: without it the rest gets written three different
  ways.
- **Home / overview** — what Kern is, the brick philosophy, and plainly what runs today versus what
  is planned.
- **Ecosystem diagram** — Mermaid, rendering both on GitHub and in the published site, with the
  `kern-agent` gap drawn dashed and room left for packages still to come.
- **Four brick pages** instantiated from the brick template — `kern-link`, `Kern-Anon`, `Kern-Orch`,
  `Kern-UI` — filled where truthful, placeholdered elsewhere.
- **Contracts registry** — the four known contracts, each stating its enforcement status.
- **End-to-end quickstart** (J2) — `kern-orch` executing a hello graph with `kern-ui` live in a
  browser. **Verified by actually running it**, stamped with contract version and date, and stating
  plainly that its agent nodes are deterministic stubs rather than model calls.
- **Glossary** — consolidated and translated from `Kern-Orch/docs/GLOSSAIRE.md`, which currently
  holds the ecosystem's vocabulary trapped inside one repo.
- **Ownership map** — the subject → authoritative home table, as a page.
- **Freshness table** — page → brick → version verified → date, placeholders included.

Plus the **"what's missing" page**: the `kern-agent` bridge and the pending protocol extensions.
This is the highest-value open work in the ecosystem, and is therefore framed as a contributor
entry point rather than an apology.

## Out of scope

- **No writes to `kern-ia/.github`** — no org profile README, no CONTRIBUTING, no code of conduct,
  no security policy or templates. That repo is not yet in a state its owners can vouch for.
  *Deferred.*
- **No hand-written API reference** — `pkg.go.dev` regenerates it per commit. *Rejected.*
- **No re-hosting of repo internals** — architecture notes, dev logs, retros and changelogs stay in
  their repos. *Rejected.*
- **No changes to brick code** — findings become issues on the brick, not commits. *Rejected.*
- **No relocation of the `kern.*` fixtures**, and **no freezing of the provisional agent-CLI
  protocol by documentation**. *Rejected.*
- **No repo renames or Go module-path migration** — breaking changes owned by each repo.
  *Deferred.*
- **No CI-executed quickstart job**, **no versioned doc trees**, **no custom domain**, **no
  build-time generation from repo docs**. *Deferred.*
- Contribution rules and the contributor-facing writing guide belong to
  [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md), not here — this epic decides the
  conventions, epic 2 turns them into a contributor surface.
- Filling the brick sections in depth belongs to
  [Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md).

## Acceptance criteria

1. **No false information** — every unfilled area is an explicit marked placeholder, and no page
   asserts anything unverified against the code.
2. **Extensibility** — adding a brick or a contract is filling a template slot, not redesigning
   navigation. The fifth package (in progress, name and role unknown to this plan) is the real
   test.
3. **Honest maturity** — a reader can tell what runs today from what is planned, per brick.
4. **Under 15 minutes** from landing on the site to a running hello graph, using only the wiki.
5. **Ownership respected** — no page contradicts the repo docs on the same subject.

## Dependencies

None — this is the first epic and every other one depends on it.

Blocks [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md),
[Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md),
[Epic 4](/epic-4-project-map-freshness/EPIC_4.md) and
[Epic 5](/epic-5-french-edition/EPIC_5.md).

## Context

- [Technical specs](../../planning/SPECS.md)
- [Conventions](../../planning/CONVENTIONS.md)

## Notes

**Project-wide constraints** (they apply to every epic, not only this one):

- **No invented content, in any form** — no plausible filler in a placeholder, nothing planned
  described as existing, no configuration inferred rather than checked. The one non-negotiable.
- **No completeness target** — partly-placeholdered pages are the intended state. Coverage is
  deliberately not a success criterion, because a coverage target would reward filling
  placeholders.
- **Consistency, not capacity, is the binding constraint**, and **the wiki must absorb a new
  package without restructuring**.
- **Zero budget** — GitHub Pages and GitHub-native tooling only.
- **Plain markdown, generator-agnostic** — every page stays readable on GitHub whatever generator
  the specs pick. The GitHub Wiki tab is rejected: no PR review, no CI.
- **English is the source language.** No French page exists without an English original.
- **No deadline.**

**Risks carried by this epic specifically:**

- **The front door overpromises.** The brick READMEs describe Kern as running AI agents; today no
  LLM can run in a graph, because the `kern-agent` bridge doesn't exist. Mitigated by the maturity
  markers, the dashed edge in the diagram, and the quickstart's explicit stub note.
- **The wiki contradicts the repos.** Duplication is accepted against weekly-moving upstreams, so
  the failure mode is not a dead link but a page that is confidently wrong. Mitigated by the
  ownership map, version stamps and the freshness table.
- **Documenting a protocol officially about to change** — the orch↔agent-CLI seam is provisional,
  with five planned extensions. Mitigated by a provisional banner, and by recording the extensions
  as open questions rather than spec.
- **The quickstart breaks on a contract bump.** Mitigated by the version stamp; the CI-executed
  quickstart is the real fix, and it is deferred to
  [Epic 4](/epic-4-project-map-freshness/EPIC_4.md)'s neighbourhood.
- **Inconsistent module paths** — `github.com/julienlegoux/kern-link`, `github.com/yoann/kern-orch`;
  neither matches `kern-ia`. Any `go get` line written today is wrong or will be. Mitigated by
  documenting current paths verbatim and flagging the migration in epic 4.

**Assumption to verify first, not read:** the `kern-orch` + `kern-ui` pairing works today on a
clean machine. That is the quickstart's whole premise and it is unverified — **running it is the
first real task of this epic**.

**Open unknown:** the bricks each carry a licence, but only `kern-link` advertises MIT, and the
licence audit that would have checked this is out of scope. This stays an open unknown rather than
a verified fact — do not assert licences on the brick pages.
