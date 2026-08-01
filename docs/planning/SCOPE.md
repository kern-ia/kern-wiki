---
type: Scope
title: "Kern wiki — Scope"
description: "A documentation site for the kern-ia ecosystem: the frame Kern's documentation lands in, filled progressively and never invented."
tags: [planning, scope]
timestamp: 2026-07-30T06:21:37Z
status: final
---

# Kern wiki — Scope

## Problem

`kern-ia` is a set of Go "bricks" — autonomous packages coupled only through versioned
contracts. Today: `kern-link` (unified LLM API across 35 providers), `Kern-Anon` (PII detection
and anonymization), `Kern-Orch` (graph-based agent orchestration with checkpoints), `Kern-UI`
(live run visualization), and a fifth package in progress. Each repo documents itself well *for
someone already inside it*. Nothing documents Kern.

Concretely:

- `github.com/kern-ia` says nothing about what Kern is — the org's `.github` repo holds only a
  `.gitkeep`.
- No page explains why Kern is separate bricks rather than one binary, or how they connect. The
  connective tissue — the `kern.*` contracts — is visible only inside two READMEs.
- Cross-cutting knowledge is either duplicated (a "CANONICAL BLOCK" mirrored verbatim between
  `Kern-Orch` and `Kern-UI`) or trapped in one repo (`Kern-Orch/docs/GLOSSAIRE.md` defines the
  ecosystem's vocabulary).
- Nothing tells a newcomer how to contribute, and nothing gives the team a transverse view
  across repos that each move weekly.
- Knowledge that belongs to no single repo has nowhere to live at all — the
  `Kern-Orch × kern-link` compatibility analysis is a document about the *seam* between two
  bricks, and no repo can own it.

The job: **make Kern comprehensible and usable from one place** — without becoming a second copy
of the repos ([decision](/scope/01-problem-statement.md)).

One thing shapes everything below. The ecosystem is two weeks old, its target architecture is
not settled, and packages are still arriving. So this project builds **the frame documentation
lands in** — an information architecture, page templates, a contracts registry, and a
placeholder convention — and fills it as things settle
([decision](/scope/20-documenting-the-gap.md)).

## Users

Three audiences, each getting its own milestone
([decision](/scope/02-target-audiences.md)):

1. **External readers** — Go developers who have never heard of Kern, plus the narrower case of
   someone who wants **one** brick inside their own project and doesn't care about the ecosystem.
2. **Contributors** — not hypothetical: two contributors today, more expected. Their first need
   is *how to write in this wiki*, not how to get access.
3. **Maintainers** — a transverse map across repos that each have their own roadmap.

Six journeys the wiki is accountable for
([decision](/scope/11-core-journeys.md)):

| | Journey | Milestone |
|---|---|---|
| **J1** | Understand Kern in 60 seconds — overview + one diagram, can name the bricks | M1 |
| **J2** | Run the ecosystem end to end — `kern-orch` executing a hello graph, `kern-ui` live in a browser | M1 |
| **J3** | Pick the right brick — arrive with a need, land on the right package at the right entry point | M1 |
| **J4** | Make a first contribution — set up, conventions, contracts, where to open the issue | M2 |
| **J5** | See where the project stands — one transverse status view instead of N roadmaps | M4 |
| **J6** | Adopt one brick — install, configure and use a single package from the wiki alone | M3 |

## Goals & success criteria

Ten pass/fail criteria ([decision](/scope/14-success-criteria.md)). Coverage is deliberately
**not** among them: a coverage target would reward filling placeholders, which is the one thing
this project forbids.

**M1** — 1. **No false information**: every unfilled area is an explicit marked placeholder, and
no page asserts anything unverified against the code. 2. **Extensibility**: adding a brick or a
contract is filling a template slot, not redesigning navigation — the fifth package is the real
test. 3. **Honest maturity**: a reader can tell what runs today from what is planned, per brick.
4. **Under 15 minutes** from the site to a running hello graph, using only the wiki.
5. **Ownership respected**: no page contradicts the repo docs on the same subject.

**M2** — 6. **Uniformity**: another contributor adds or fills a page matching the templates
without asking how.

**M3** — 7. **Adoption**: a developer installs, configures and uses one brick in their own Go
project from its wiki section alone. 8. Every technical page carries its version stamp.

**M4** — 9. The transverse status page actually gets used to pick a next task.

**M5** — 10. Every French page has an English original and says the same thing.

## Non-goals (out of scope for v1)

Each marked *rejected* (won't happen) or *deferred* (later, deliberately) —
[full list with reasons](/scope/13-non-goals.md):

- **No invented content, in any form** — no plausible filler in a placeholder, nothing planned
  described as existing, no configuration inferred rather than checked. *Rejected — the one
  non-negotiable.*
- **No completeness target** — partly-placeholdered pages are the intended state. *Rejected.*
- **No hand-written API reference** — `pkg.go.dev` regenerates it per commit. *Rejected.*
- **No re-hosting of repo internals** — architecture notes, dev logs, retros, changelogs stay in
  their repos. *Rejected.*
- **No writes to `kern-ia/.github`** — no CONTRIBUTING, code of conduct, security policy,
  templates, licence audit, **or org profile README**; that repo is not yet in a state its owners
  can vouch for. *Deferred.*
- **No changes to brick code** — findings become issues on the brick. *Rejected.*
- **No relocation of the `kern.*` fixtures**, and **no freezing of the provisional agent-CLI
  protocol by documentation**. *Rejected.*
- **No French translation of per-brick technical documentation** while the packages move.
  *Deferred.*
- **No build-time generation from repo docs**, **no versioned doc trees**, **no executed-quickstart
  CI job**, **no custom domain**, **no blog or changelog aggregation**. *Deferred.*
- **No repo renames or Go module-path migration** — breaking changes owned by each repo
  ([decision](/scope/19-module-path-migration.md)). *Deferred.*

## Constraints

- **Consistency, not capacity, is the binding constraint** ([decision](/scope/15-constraints.md)).
  Several people write, packages keep arriving: a wiki filled three different ways, or
  restructured whenever a brick lands, decays regardless of effort spent.
- **The wiki must absorb a new package without restructuring.**
- **Zero budget** — GitHub Pages and GitHub-native tooling only.
- **Plain markdown, generator-agnostic** — every page stays readable on GitHub whatever
  `define-specs` picks as a generator ([decision](/scope/03-delivery-form.md)). The GitHub Wiki
  tab is rejected: no PR review, no CI.
- **English is the source language; the published site is bilingual EN/FR**
  ([decision](/scope/05-content-language.md)). No French page exists without an English original.
- **Upstreams move weekly and are pre-1.0** — anything asserted about internals is stale by
  default, and there is no backward-compatibility obligation yet, so structure can still change
  freely.
- **No deadline.**

Shape of the delivery: a dedicated repo `kern-ia/kern-wiki`, published with GitHub Pages
([decision](/scope/04-hosting-and-location.md)). The wiki is **self-contained** — it hosts real
content rather than sending readers into other repos — with duplication bounded by an ownership
map ([decision](/scope/06-source-of-truth.md)):

| Subject | Authoritative home |
|---|---|
| Install / configure / use a brick, integration, examples | **Wiki** |
| Ecosystem overview, vocabulary, contribution rules, transverse status | **Wiki** |
| API signatures | `pkg.go.dev` — never re-typed by hand |
| Internal architecture, dev logs, retros | **Repo** |
| `kern.*` contract JSON fixtures | **Repo**, CI-enforced |
| Release history | **Repo** |

## Milestone 1: The frame

The information architecture and conventions, plus every page writable truthfully today. English.
Serves J1–J3. Thirteen deliverables ([decision](/scope/12-mvp-cut.md)):

- `kern-ia/kern-wiki` initialized — plain markdown, `en/` tree so adding `fr/` later moves no
  files, repo README explaining how to add a page.
- GitHub Pages publishing on push to the default branch.
- **Information architecture** — sections (ecosystem · bricks · contracts · integration ·
  contributing · status) designed so a new brick or contract fills a slot.
- **Page templates** — a brick template (identity, maturity, **exposed / needs**, install,
  configuration, usage, integration, version stamp) and a contract template (purpose, producer,
  consumer, versions, enforcement status, fields, migration). The exposed/needs block follows the
  convention `Kern-UI`'s README already states.
- **The placeholder & maturity convention** — markers *works today* / *provisional* / *planned*,
  explicit "not documented yet" blocks, and the no-invented-content rule. **The deliverable not
  to cut under time pressure**: without it the rest gets written three different ways.
- **Home / overview** — what Kern is, the brick philosophy, and plainly what runs today vs what
  is planned.
- **Ecosystem diagram** — Mermaid, rendering on GitHub and in the site, with the `kern-agent` gap
  drawn dashed and room for packages still to come.
- **Four brick pages** instantiated from the template — filled where truthful, placeholdered
  elsewhere.
- **Contracts registry** — the four known contracts, each stating its enforcement status
  ([decision](/scope/09-contract-registry-home.md)).
- **End-to-end quickstart** — J2, verified by running it, stamped with contract version and date,
  and stating plainly that its agent nodes are deterministic stubs rather than model calls.
- **Glossary** — consolidated and translated from `Kern-Orch/docs/GLOSSAIRE.md`.
- **Ownership map** — the table above, as a page.
- **Freshness table** — page → brick → version verified → date, placeholders included.

Plus the **"what's missing" page**: the `kern-agent` bridge and the pending protocol extensions —
the highest-value open work in the ecosystem, and therefore a contributor entry point rather than
an apology.

## Milestone 2: Conventions & contribution surface

Contributors (J4). The rules come *before* the bulk writing, because several people fill the
frame and it only holds if they fill it the same way
([decision](/scope/17-milestones.md)).

- **How to write here** — templates, maturity markers, version stamps, and the
  no-invented-content rule turned into a review checklist.
- **Contribution process** — setup, conventions, how a change lands, where to open an issue.
- **Brick-authoring guide** — what makes something a `kern-*` brick, including the exposed/needs
  declaration a new package must publish.
- **How to add a contract entry** when the next one arrives.
- **Canonical naming rule** — lowercase `kern-*`, with today's real repo names noted where they
  differ, and one follow-up issue per repo for the mismatches
  ([decision](/scope/10-naming-and-identity.md)).

No writes to `kern-ia/.github` ([decision](/scope/08-governance-content.md)).

## Milestone 3: Progressive package documentation

Adopters (J6). Fill each brick's section against the template
([decision](/scope/07-coverage-depth.md)): install, configuration, usage patterns, worked
examples, integration over the `kern.*` contracts — replacing placeholders as knowledge settles,
and covering the fifth package once it lands.

Includes the operational traps that only surface in production and must not be footnotes:
`kern-orch serve` under an empty service environment loses `HOME` and API keys and fails as
silent in-band "no API key" errors; and kern-link's OAuth flows impersonate first-party clients,
which its own docs warn gets accounts revoked in long-running daemons — so **API keys only** for
daemon mode.

The largest milestone; expect it to be cut roughly one brick at a time. A section that is half
placeholders and wholly true is a valid end state.

## Milestone 4: Project map & freshness

Maintainers (J5).

- **Transverse status** across the repos, and a consolidated roadmap.
- **Open architectural questions**, linked to per-repo issues: the `kern-agent` bridge, the five
  pending agent-protocol extensions, a possible `kern-contracts` extraction, module-path
  migration, the `.github` cleanup.
- **CI link checker.**
- **Staleness check** — a scheduled job comparing each page's version stamp against the brick's
  latest release and opening one issue listing what moved
  ([decision](/scope/16-freshness-and-versioning.md)).

Three page states stay distinguishable throughout: *not documented yet*, *verified against
version X*, *possibly stale*. Latest only — no versioned documentation trees.

## Milestone 5: French edition

`fr/` tree and a language switch, translating the **stable front-door pages only** — overview,
diagram, glossary, quickstart, and the conventions page if it has settled. Deliberately not the
M3 technical sections while the packages move ([decision](/scope/05-content-language.md)).

Gaps between the two languages are acceptable; contradictions are not.

## Risks & assumptions

Full list with mitigations: [decision](/scope/18-risks-and-assumptions.md).

**Risks, worst first.**

- **The wiki contradicts the repos.** Duplication is accepted against weekly-moving upstreams, so
  the failure mode is not a dead link but a page that is confidently wrong. *Mitigated by* the
  ownership map, version stamps, and the freshness table.
- **The front door overpromises.** The READMEs describe Kern as running AI agents; today no LLM
  can run in a graph, because the `kern-agent` bridge doesn't exist. *Mitigated by* maturity
  markers, the dashed edge in the diagram, and the quickstart's explicit stub note.
- **Documenting a protocol that is officially about to change** — the orch↔agent-CLI seam is
  provisional with five planned extensions. *Mitigated by* a provisional banner and recording the
  extensions as open questions, not spec.
- **Doc churn from documenting moving packages** — a deliberate bet. *Mitigated by* stability
  banners and by not translating those pages.
- **The quickstart breaks on a contract bump.** *Mitigated by* the version stamp; the CI-executed
  quickstart is the real fix, deferred.
- **Inconsistent module paths** — `github.com/julienlegoux/kern-link`,
  `github.com/yoann/kern-orch`; neither matches `kern-ia`. Any `go get` line written today is
  wrong or will be. *Mitigated by* documenting current paths verbatim and flagging the migration
  in M4.
- **Contributors find no `CONTRIBUTING.md` where GitHub shows one** — `.github` is out of scope,
  so J4 is served by a site page GitHub's own affordances won't surface. *Accepted.*
- **Scope drifts into brick work.** *Mitigated by* the no-brick-code non-goal; findings become
  issues on the brick.

**Assumptions.**

- **Two contributors, more expected** — corrected mid-planning; it is what re-based the
  constraints.
- **The ecosystem will grow during this project** — a fifth package is in progress and its name,
  role and contracts are unknown to this plan. Certain rather than assumed, which is why
  extensibility is a success criterion.
- **The target architecture will settle incrementally**, not in one design pass. Unverified, and
  the reason no milestone promises a complete architecture description.
- **The `kern-orch` + `kern-ui` pairing works today on a clean machine** — the quickstart's whole
  premise, and unverified: it must be *run*, not read. First real task of M1.
- Each package's public surface is stable enough that usage docs written now survive weeks, not
  days. If wrong, M3 splits per brick and the least stable one is postponed.
- `kern-link` stays a tracking port of `@earendil-works/pi-ai`, so its section documents usage and
  points upstream for design.
- The bricks each carry a licence. Only `kern-link` advertises MIT, and the audit that would have
  checked this is out of scope — so this stays an open unknown rather than a verified fact.
