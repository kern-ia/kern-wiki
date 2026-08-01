---
type: Decision
title: "Freshness & versioning"
description: "How does the wiki stay true as packages move and arrive, and does it version?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 16
slug: freshness-and-versioning
status: decided
verdict: "Three page states made visible from M1 (stamps + freshness table), enforced in M4; latest-only, no versioned trees"
decided_via: triage
depends_on: [source-of-truth]
---

# Question

**Refreshed twice, and materially changed each time.** The original recommendation assumed
link-never-copy, which made link rot the only drift risk and a CI link checker a near-complete
answer. The self-contained verdict killed that: a hosted page can be confidently wrong with
perfectly valid links. Now the placeholder convention
([decision](/scope/20-documenting-the-gap.md)) adds a third state — pages that are deliberately
unwritten.

So the wiki has to distinguish **three** states, not two, and none of them is "broken":

- *not documented yet* — an explicit placeholder,
- *documented and verified* — against a known brick version,
- *documented but possibly stale* — the brick moved since.

Conflating the first and third is how a wiki loses trust: a reader who can't tell "we haven't
written this" from "this may be wrong" treats everything as unreliable.

# Options

- **Discipline only** — review pages when a brick changes. Free, and precisely the guarantee the
  Kern repos themselves rejected: *"drift is caught by tests, not by discipline"*.
- **Visible staleness** — every technical page stamped with the brick version/commit and date
  verified; placeholders marked; all of it collected in one table. Doesn't prevent drift; makes
  it legible. Cheap.
- **Enforced staleness** — CI fails (or opens an issue) when a documented brick has moved past
  its stamped version, read from the GitHub API. Turns "someone should check" into a signal.
- **Executed documentation** — CI runs the quickstart and examples against the real bricks. The
  only mechanism that catches *wrong* rather than merely *old*; needs a Go toolchain, multi-repo
  checkouts, a headless run.

# Recommendation

**Visible staleness from M1, enforced staleness in M4, executed documentation deferred**, plus
**no versioned documentation trees** (latest only — pre-1.0 packages, nobody on old versions).

- **Version stamp** on every technical page: brick + commit/tag + date verified. Written into
  the page template from day one ([decision](/scope/12-mvp-cut.md)) — retrofitting stamps is
  what never happens.
- **Freshness table** with all three states, placeholders included. This is what makes a
  partly-empty wiki honest rather than unfinished.
- **Maturity + stability markers** per page ([decision](/scope/07-coverage-depth.md),
  [decision](/scope/20-documenting-the-gap.md)).
- **Registry hygiene as packages arrive** — each contract entry records when it was added and
  its enforcement status, so the registry's own growth is legible
  ([decision](/scope/09-contract-registry-home.md)).
- **CI link checker** (M4) — still worth having, now secondary.
- **Staleness check** (M4) — a scheduled job comparing each stamp against the brick's latest
  release and opening/updating one issue listing what moved. Cheap: it reads metadata, not code.
  This is the mechanism that replaces discipline, which matters more with several contributors
  than it did with one.

The **executed quickstart** is the honest right answer to "will J2 keep working" and stays
deferred: it means a documentation repo building test infrastructure for other repos' code.
Worth revisiting the first time the quickstart breaks in the wild.

Ordering note, stated rather than hidden: the automation lands in M4, *after* M3 writes the pages
it governs. That is the wrong order on paper. It is accepted because the stamps and the table
exist manually from M1, so M4 automates a practice already in place rather than introducing
one — and building freshness tooling before any content exists to check would delay everything
visible for machinery.

# Verdict

**Visible staleness from M1, enforced in M4, executed documentation deferred; no versioned
documentation trees.** Accepted at re-triage.

The three states — *not documented yet* / *documented and verified against version X* /
*documented but possibly stale* — must stay distinguishable everywhere: in the page itself, in
the freshness table, and in the M4 staleness job's output. Conflating "unwritten" with "maybe
wrong" is what makes readers distrust every page equally.
