---
type: Decision
title: "MVP feature cut"
description: "What exactly ships in v1 of the wiki?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 12
slug: mvp-cut
status: decided
verdict: "The frame — 13 deliverables, templates and the placeholder convention included; partly-placeholdered pages are the intended state"
decided_via: triage
depends_on: [coverage-depth, core-journeys]
---

# Question

**Refreshed twice.** The first cut assumed link-only brick pages and an org profile README.
The second assumed v1 was a set of finished pages. Both premises are gone: the user's framing is
**"créer vraiment la structure autour de ce que va être cette wiki"** — build the frame, then
fill it as the documents come into order — with placeholders where knowledge is missing and
**no invented content** ([decision](/scope/20-documenting-the-gap.md)).

So: what is the smallest v1 that is a real, usable frame rather than an empty promise?

# Options

- **Skeleton** — repo, Pages build, nav. Ships in an afternoon; nobody can tell what it will
  become or how to fill it.
- **The frame** — the information architecture, the page templates, the placeholder/maturity
  convention, plus every page that can be written **truthfully today** instantiated from those
  templates. A reader gets real answers where they exist and honest gaps elsewhere; a
  contributor gets a slot to fill.
- **The frame + full content** — everything the coverage verdict implies, at once. Contradicts
  structure-first, and requires knowledge of a target architecture that isn't settled.

# Recommendation

**The frame.** Thirteen deliverables, small individually — the value is in their consistency,
not their volume:

1. `kern-ia/kern-wiki` initialized: plain generator-agnostic markdown, `en/` tree so adding
   `fr/` later moves no files, repo README explaining what the repo is and how to add a page.
2. GitHub Pages publishing on push to the default branch.
3. **Information architecture** — the section skeleton (ecosystem · bricks · contracts ·
   integration · contributing · status), designed so a new brick or contract is a filled slot,
   not a navigation redesign. The fifth package, already in progress, is the test of this.
4. **Page templates** — a brick template (identity, maturity, **exposed / needs**, install,
   configuration, usage, integration, version stamp) and a contract template (purpose,
   producer, consumer, versions, enforcement status, fields, migration). The exposed/needs
   block follows `Kern-UI/README.md`'s existing convention
   ([decision](/scope/09-contract-registry-home.md)).
5. **The placeholder & maturity convention**, written as a page contributors are pointed at:
   markers *works today* / *provisional* / *planned*, explicit "not documented yet" blocks
   stating what's missing, and the hard rule — **no plausible-sounding invented content, ever**.
   This is the single most load-bearing deliverable in v1: every later page depends on it, and
   with several contributors it is what keeps the wiki coherent.
6. **Home / overview** — what Kern is, the brick philosophy (autonomous, agnostic, coupled only
   through contracts), and plainly what runs today vs what is planned.
7. **Ecosystem diagram** — Mermaid, renders on GitHub *and* in the site, with the `kern-agent`
   gap drawn dashed and room for packages still to come. Four happily connected bricks would be
   the most misleading artefact on the site.
8. **Four brick pages instantiated from the template** — filled where truthful today, explicitly
   placeholdered elsewhere. Partially-empty pages are the expected v1 state.
9. **Contracts registry** — entries for the four known contracts (three CI-enforced, one
   provisional), each stating its enforcement status.
10. **End-to-end quickstart** — J2: `kern-orch` running a hello graph with `kern-ui` live in a
    browser. Works today because the default runner is the deterministic `Stub`, so the page
    **must state that the agent nodes are stubs, not model calls**. Verified by running it, and
    stamped with the contract version and date.
11. **Glossary** — consolidated and translated from `Kern-Orch/docs/GLOSSAIRE.md` (graph, node,
    state, edge, sub-graph, checkpoint, freeze, brick, contract).
12. **Ownership map** — what the wiki owns vs the repos vs `pkg.go.dev`. The guardrail the
    [source-of-truth verdict](/scope/06-source-of-truth.md) rests on.
13. **Freshness table** — page → brick → version verified → date, and which pages are
    placeholders. Distinguishing "not written yet" from "written but possibly stale" is the
    point ([decision](/scope/16-freshness-and-versioning.md)).

Also in v1, near-free and high value: the **"what's missing" page** (the `kern-agent` bridge and
the pending protocol extensions) — it is where a contributor finds the most valuable open work.

**Dropped:** the org profile README. It lives in `kern-ia/.github`, which the user has kept out
of scope ([decision](/scope/08-governance-content.md)) — so `github.com/kern-ia` stays silent in
v1, accepted as a known cost.

Two honest notes on this cut. The quickstart is still the item most likely to be
underestimated: the only deliverable that can fail for reasons outside this repo. And item 5 is
the one to resist cutting when time gets short — without the convention, items 8–13 become
thirteen pages written three different ways.

# Verdict

**The frame**, accepted at re-triage: the thirteen deliverables above, with the
placeholder/maturity convention (item 5) treated as the one that must not be cut under time
pressure, and the "what's missing" page included. Partly-placeholdered pages are the intended
v1 state, not a shortfall.

The org profile README stays dropped ([decision](/scope/08-governance-content.md)).
