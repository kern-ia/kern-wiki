---
type: Decision
title: "Constraints"
description: "What externally imposed limits bound this project?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 15
slug: constraints
status: decided
verdict: "Consistency-driven: small growing team, extensibility required, zero budget, no deadline"
decided_via: discussion
depends_on: []
---

# Question

**Reopened** — the first verdict rested on a false premise. Nothing in the repos indicated a
deadline or budget, so I concluded the binding constraint was one maintainer's attention. It
isn't: there are **two contributors today, with more expected**, and a fifth package already in
progress.

That changes which limit actually binds.

# Options

- **Deadline-driven** — a launch date exists and content is cut to fit it. Still no evidence of
  one.
- **Capacity-driven** — the previous verdict: maintenance attention is the scarce resource, so
  every decision is judged on upkeep cost.
- **Consistency-driven** — with several people writing and packages arriving one after another,
  the scarce resource is not hours but **uniformity**: a wiki filled three different ways by
  three people, or restructured every time a brick lands, decays regardless of how much
  attention it gets.

# Recommendation

**Consistency-driven.** Stated constraints:

- **Small growing team (2 now, more expected), several packages still to come.** The binding
  constraint is cross-contributor consistency and structural extensibility — which is exactly
  why the project's own shape changed to structure-and-conventions first, content progressively
  ([decision](/scope/20-documenting-the-gap.md),
  [decision](/scope/17-milestones.md)).
- **The wiki must absorb a new package without restructuring.** A new brick or contract should
  be a filled template slot, not a navigation redesign
  ([decision](/scope/09-contract-registry-home.md)).
- **Zero budget** — GitHub Pages and GitHub-native tooling only; no paid domain, no hosted
  search, no analytics in v1.
- **Content must stay readable as plain markdown on GitHub** — forbids generator-specific
  syntax whatever `define-specs` picks ([decision](/scope/03-delivery-form.md)).
- **Upstreams move weekly and are pre-1.0** — anything asserted about brick internals is stale
  by default, and no backward-compatibility obligation exists yet, so structure can still
  change freely. That freedom expires; it is worth spending now.
- **No deadline** — nothing in the repos or the conversation indicates one.

What this reopening *relaxes*: the earlier verdict flagged a tension — hosted usage docs across
four bricks plus a second language looked over-committed for one person. With two contributors
and more coming, that tension is much weaker, and the choices in
[decision](/scope/06-source-of-truth.md), [decision](/scope/07-coverage-depth.md) and
[decision](/scope/05-content-language.md) get easier rather than harder. The guardrails
(version stamps, freshness table, "don't translate moving pages") stay — not because capacity
is short, but because they are what keeps several people telling the same story.

# Verdict

**Consistency-driven**, accepted at re-triage. The binding constraint is cross-contributor
consistency and structural extensibility, not maintenance hours: a wiki filled three different
ways, or restructured each time a package lands, decays no matter how much attention it gets.
Zero budget, plain-markdown readability, weekly-moving pre-1.0 upstreams and no deadline all
stand.

This is what justifies conventions-before-volume in [decision](/scope/17-milestones.md), and it
relaxes rather than tightens the earlier trade-offs: hosted usage documentation
([decision](/scope/06-source-of-truth.md), [decision](/scope/07-coverage-depth.md)) and a
bilingual site ([decision](/scope/05-content-language.md)) are tenable with several people. The
guardrails stay — version stamps, the freshness table, "don't translate moving pages" — now
serving coherence across contributors rather than survival of one.

**Superseded verdict, kept as history** — *"Capacity-driven: solo maintainer, zero budget, no
deadline"* (accepted at triage 2026-07-30). Reopened the same day: the solo-maintainer premise
was wrong (two contributors, `kern-orch`'s module path pointing at a second account was the
clue), and it was load-bearing for several trade-offs.
