# Scope decision ledger — Kern wiki

Durable triage view. Statuses: `open` (awaiting verdict) / `decided` / `na`.

**19 decided · 0 open · 1 n/a** — [SCOPE.md](../SCOPE.md) written from this ledger.

* [Problem & job-to-be-done](01-problem-statement.md) - decided: build the frame Kern's documentation lands in — front door, usage manual, filled progressively
* [Target audiences](02-target-audiences.md) - decided: all three, phased; contributors are a present internal audience (2 today)
* [Delivery form](03-delivery-form.md) - decided: generator-agnostic markdown + GitHub Pages site; not the GitHub Wiki tab
* [Repo location & hosting](04-hosting-and-location.md) - decided: dedicated `kern-ia/kern-wiki` on Pages; no org profile README, no custom domain
* [Content language](05-content-language.md) - decided: documents authored in English, published site bilingual EN/FR
* [Source of truth vs the repos](06-source-of-truth.md) - decided: self-contained wiki, duplication accepted and bounded by an ownership map
* [Coverage depth](07-coverage-depth.md) - decided: per-brick technical usage docs as the target shape, reached progressively; no hand-written API reference
* [Open-source governance files](08-governance-content.md) - decided: `.github` stays untouched; wiki documents the process only
* [Home of the cross-brick contracts](09-contract-registry-home.md) - decided: a growing registry — document each contract as it arrives, per package exposed/needs; repos keep authority
* [Naming & identity consistency](10-naming-and-identity.md) - decided: document canonical lowercase `kern-*`, no renames here
* [Core user journeys](11-core-journeys.md) - decided: six journeys — J1–J5 plus J6 (adopt one brick)
* [MVP feature cut](12-mvp-cut.md) - decided: the frame — 13 deliverables incl. templates and the placeholder convention; partly-placeholdered pages are the intended state
* [Non-goals](13-non-goals.md) - decided: explicit list with reasons; no invented content is the one non-negotiable
* [Success criteria](14-success-criteria.md) - decided: ten criteria on truthfulness, extensibility, uniformity and walkability — never coverage
* [Constraints](15-constraints.md) - decided (reopened once): consistency-driven, small growing team — supersedes the solo-maintainer premise
* [Freshness & versioning](16-freshness-and-versioning.md) - decided: three page states, visible from M1, enforced in M4; latest-only
* [Milestones / phasing](17-milestones.md) - decided: five — Frame / Conventions & contribution / Package docs / Project map / French
* [Risks & assumptions](18-risks-and-assumptions.md) - decided: named risks; content drift and overpromising lead
* [Go module-path migration](19-module-path-migration.md) - na: breaking change owned by each brick repo, tracked as issues + a risk
* [Documenting what doesn't exist yet](20-documenting-the-gap.md) - decided: target architecture with maturity markers and explicit placeholders; never invented content
