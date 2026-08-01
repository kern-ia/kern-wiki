---
type: Decision
title: "Coverage depth"
description: "How deep does the wiki go per brick — narrative, usage, or full reference?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 07
slug: coverage-depth
status: decided
verdict: "Per-brick technical usage documentation, maintained as living docs with stability banners; no hand-written API reference"
decided_via: discussion
depends_on: [target-audiences, source-of-truth]
---

# Question

How much does a brick page actually say? All four bricks are Go, so `pkg.go.dev` already
publishes their API reference for free (`kern-link` even advertises the badge). And the
packages are young: `Kern-UI/docs/a-trancher.md` ("to be decided") shows the design is
still live.

# Options

- **Navigation only** — one line per brick and a link. Minimal; the reader cannot tell
  whether a brick is relevant without leaving the site.
- **Narrative + orientation per brick** — one page each: what it does, when to use it and
  when not to, how it connects, where to go next. No API surface, no tutorial.
- **Technical usage documentation per brick** — install, configuration, usage patterns,
  integration with the other bricks, worked examples. Real documentation a developer
  works from. Costs the most upkeep, and the packages are still moving.
- **Full reference** — API docs re-hosted in the wiki. Duplicates `pkg.go.dev` and rots
  fastest.

# Recommendation

Narrative + orientation per brick — four short pages ending in links rather than detail,
with no API reference since `pkg.go.dev` does it automatically per commit.

# Verdict

**Deepened by the user: technical usage documentation per brick.** The packages are
"balbutiants" — some already roughly the shape they will keep, none guaranteed — and the
point is precisely to **start maintaining "how to use it" docs now** rather than after
they stabilize. Waiting for stability means writing them under pressure later, with the
knowledge already stale.

So each brick gets a documentation section, not a page:

- What it is, the problem it solves, when to use it **and when not to** (the orientation
  layer from the original recommendation — kept, it feeds journeys J1/J3).
- Install and configuration (env vars, build tags — e.g. `Kern-Anon`'s `onnx` tag,
  `Kern-UI`'s `KERN_UI_ADDR` / `KERN_UI_WEB_DIR`, `Kern-Orch`'s `KERN_STEP_REPORT_URL`).
- Usage patterns with worked, runnable examples.
- Integration with the other bricks, over the `kern.*` contracts.

Two guardrails, because documenting a moving target is the known cost of this verdict:

1. **A stability banner per section** stating the brick's maturity and that the page
   tracks a moving package — honest, and it lowers the cost of being briefly wrong.
2. **A version stamp** (brick commit/tag + date verified) on every technical page
   ([decision](/scope/16-freshness-and-versioning.md)).

Unchanged: **no hand-written API signature reference.** `pkg.go.dev` regenerates it per
commit and cannot go stale; re-typing signatures is the one form of duplication with
no upside ([decision](/scope/13-non-goals.md)).

This verdict is the largest single driver of project size — it turns four short pages
into a full documentation section per brick, which is why it becomes its own milestone
rather than riding along in the front door ([decision](/scope/17-milestones.md)).

**Amended — depth is reached progressively, not up front.** Per
[decision](/scope/20-documenting-the-gap.md), v1 ships the *template* for a brick section
(identity, maturity, exposed/needs, install, configuration, usage, integration, version stamp)
with every unknown left as an explicit placeholder. Sections then fill as the packages settle
and their documents come into order. So this verdict sets the **target shape** of per-brick
documentation; it does not require that shape to be complete in any milestone. A brick section
that is half placeholders and wholly true is a valid, expected state.
