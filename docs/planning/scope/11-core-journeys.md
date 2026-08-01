---
type: Decision
title: "Core user journeys"
description: "Which end-to-end flows must work for v1 to mean anything?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 11
slug: core-journeys
status: decided
verdict: "Six journeys — J1–J5 as recommended, plus J6 (adopt one brick) added by the coverage-depth verdict"
decided_via: triage
depends_on: [target-audiences, coverage-depth]
---

# Question

Which flows are the wiki accountable for? These become acceptance-criteria seeds for
epics, so they must be walkable and checkable, not aspirational.

# Options

- **Three journeys** (discover, run, pick a brick) — external audience only; contributor
  and maintainer milestones then arrive without journeys of their own.
- **Five journeys**, one or two per audience — covers all three audiences from
  [decision](/scope/02-target-audiences.md) without inventing flows nobody walks.
- **Journey-per-page inventory** — enumerate a flow for every page. Precise, and it
  collapses into a page list rather than a set of outcomes.

# Recommendation

**Five journeys:**

- **J1 — Understand Kern in 60 seconds.** Arrives at the org or the site, reads the
  overview + one ecosystem diagram, and can say what Kern is and name the four bricks.
- **J2 — Run the ecosystem end to end.** Follows one copy-pasteable quickstart and gets
  `kern-orch` executing a hello graph with `kern-ui` showing it live in a browser —
  the pairing both READMEs already document in fragments.
- **J3 — Pick the right brick.** Arrives with a need ("unified LLM API in Go", "strip
  PII in-process") and lands on the correct repo at the correct entry point.
- **J4 — Make a first contribution.** Finds how to set up, what the conventions are, how
  the `kern.*` contracts work, and where to open the issue — without asking anyone.
- **J5 — See where the project stands.** (Maintainer.) One transverse page giving each
  brick's status and what's next, instead of five ROADMAP files.

J1–J3 land in milestone 1, J4 in milestone 2, J5 in milestone 3.

# Verdict

**Accepted at triage, with one journey added by a later verdict.**

J1–J5 stand as recommended. [decision](/scope/07-coverage-depth.md) — per-brick technical
usage documentation — creates a sixth flow that none of the five covered, because J3 stops
at "lands on the right repo":

- **J6 — Adopt one brick.** A developer who does not care about the Kern ecosystem installs
  a single brick into their own Go project, configures it, and gets it working **from the
  wiki alone** (e.g. "strip PII from user input in-process", "talk to three LLM providers
  behind one interface"). This is the journey the whole package-documentation milestone
  exists to serve, and the one that makes the wiki self-contained rather than a signpost.

Phasing: J1–J3 in M1, J6 in M2, J4 in M3, J5 in M4
([decision](/scope/17-milestones.md)).
