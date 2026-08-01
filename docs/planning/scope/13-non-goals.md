---
type: Decision
title: "Non-goals"
description: "What is explicitly out of scope for v1?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 13
slug: non-goals
status: decided
verdict: "Explicit list with reasons, each item marked rejected or deferred — revised after the source-of-truth, coverage and governance verdicts"
decided_via: triage
depends_on: [mvp-cut]
---

# Question

Which tempting items are written down as *out*, so they cannot creep back in as issues?

# Options

- **Minimal list** — name two or three obvious exclusions. Leaves the rest arguable.
- **Explicit list with reasons** — each non-goal paired with the reason it is out, so a
  future you can tell "deferred" from "rejected".
- **No non-goals** — decide case by case. Guarantees scope creep in the contributor
  milestone, which is the one with the fuzziest edges.

# Recommendation

Explicit list with reasons, each item marked *rejected* (won't happen) or *deferred*
(later, deliberately).

# Verdict

**Explicit list with reasons**, accepted. The user's first reaction was that non-goals are
superfluous, then retracted it ("oublie ce que j'ai dit sur les non-goals") — so the list
stands. It matters more here than in most projects: the wiki now hosts real content
([decision](/scope/06-source-of-truth.md)), which removes the natural brake that
"link, never copy" would have provided, so the boundary has to be written down instead.

Revised list, reflecting the verdicts on source of truth, coverage depth, language and
governance:

- **No invented content, in any form.** No plausible-sounding filler in a placeholder, no
  described-as-existing for anything planned, no inferred configuration that hasn't been checked
  against the code ([decision](/scope/20-documenting-the-gap.md)). *Rejected — the project's one
  non-negotiable.*
- **No completeness target for v1.** Partly-placeholdered pages are the intended state; "fill
  every section" is explicitly not a goal, because it competes with the rule above
  ([decision](/scope/14-success-criteria.md)). *Rejected.*
- **No hand-written API signature reference** — `pkg.go.dev` regenerates it per commit and
  cannot go stale. *Rejected.*
- **No re-hosting of repo internals** — architecture notes, `docs/index/*` dev logs,
  retros, `CHANGELOG.md` stay in their repos per the ownership map. *Rejected.*
- **No writes to `kern-ia/.github`** — no `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`,
  `SECURITY.md`, no issue/PR templates, no licence audit
  ([decision](/scope/08-governance-content.md)). *Deferred until that repo is cleaned up.*
- **No changes to brick code** — findings from writing the docs become issues on the
  brick. *Rejected.*
- **No French translation of the per-brick technical documentation** while the packages are
  unstable — French covers the stable front-door pages only
  ([decision](/scope/05-content-language.md)). *Deferred.*
- **No build-time generation or sync from repo docs** — the usage documentation does not
  exist upstream to be pulled; it has to be written. *Deferred.*
- **No versioned documentation trees** (`/v1/`, `/v2/`) — pre-1.0 bricks, no readers on old
  versions. *Deferred.*
- **No executed-quickstart CI job** — the honest fix for quickstart rot, but it means
  building test infrastructure for other repos' code
  ([decision](/scope/16-freshness-and-versioning.md)). *Deferred.*
- **No custom domain** — purely additive later, costs money now. *Deferred.*
- **No repo renames or Go module-path migration**
  ([decision](/scope/10-naming-and-identity.md),
  [decision](/scope/19-module-path-migration.md)). *Deferred, tracked as per-repo issues.*
- **No blog, changelog aggregation, or release notes.** *Deferred.*
- **No relocation of the `kern.*` contract fixtures** — the wiki documents and indexes them; the
  CI-asserted JSON in the repos stays authoritative
  ([decision](/scope/09-contract-registry-home.md)). *Rejected for this project.*
- **No freezing of the provisional agent-CLI protocol by documentation** — it is written up as
  provisional, with its five pending extensions recorded as open questions rather than spec.
  *Rejected.*
- **No org profile README** — it lives in `kern-ia/.github`, kept out of scope, so
  `github.com/kern-ia` stays silent in v1. *Deferred with the `.github` cleanup.*
