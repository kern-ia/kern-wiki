---
type: Decision
title: "Review, approval and merge"
description: "Two contributors: who reviews what, is self-merge allowed, and what the reviewer is actually accountable for."
tags: [decision, conventions]
timestamp: 2026-08-01T09:20:00Z
phase: conventions
decision: 6
slug: review-and-merge
status: decided
verdict: "green CI is the only merge gate — no approval required on any area; the reviewer checklist survives as a self-checklist, and everything it cannot hold moves into the validator"
decided_via: discussion
depends_on: [pr-size-and-unit, tdd-scope]
---

# Question

The baseline says CI must be green before merge and no force-pushes to `main`, but is silent on
approval: it assumes a team where someone else is always available. Here there are two
contributors, more expected ([scope](/scope/15-constraints.md)), and requiring an approval on
every PR means one person's absence stops the wiki.

The harder half: **what is a reviewer of a wiki page accountable for?** CI already proves the
site builds, the front matter validates, the links resolve and the generated blocks are current.
Everything CI cannot see is exactly criterion 1 — whether the page is *true*.

# Options

- **Review required on everything** — safest, and the M1 frame stalls whenever one of two people
  is away.
- **Review required by area** — tooling, templates and conventions require a second pair of eyes;
  ordinary content may be self-merged once CI is green.
- **Self-merge everywhere, CI is the gate** — fastest, and abandons the only check on
  truthfulness that exists.

# Recommendation

**Review required by area**, with an explicit checklist for the reviewer.

Requires a second approval:

- anything under `tools/`, `layouts/`, `.github/workflows/`, `data/` — the rules and the machinery
- anything under `templates/`, and any change to a page's **structure** — the frame the
  extensibility criterion depends on
- any change to CONVENTIONS.md or the published conventions page
- any page a contributor is stamping `documented` for the first time

Self-merge permitted once CI is green:

- filling or correcting prose inside an existing page's existing structure
- placeholder → placeholder edits, typo fixes, wording

The reviewer's checklist — the part CI cannot do:

1. **Is every claim verifiable against the code as it is today?** Anything not checked is a
   placeholder, not a hedge.
2. **Do the citations name what was actually read** — repo, path, version
   ([decision](/conventions/11-citations-discipline.md))?
3. **Does the maturity marker match reality**, not intent?
4. **Does the page contradict the owning repo's docs** on the same subject (criterion 5)?
5. **Does it read like the rest of the wiki** — template order, glossary terms, voice?

`main` is protected: no force-push, no direct push, CI green required. A single approval merges;
squash-merge so `main`'s history is one commit per subject, matching the one-subject PR rule.

The honest weakness: for the first months, "a second approval" means *the other contributor*, so
this is a convention held by two people who are also the people writing. Recorded as accepted —
the alternative is ceremony neither can staff.

# Verdict

**Green CI is the only merge gate.** No approval is required on any area, including `tools/`,
`templates/` and the conventions themselves. Self-merge is permitted everywhere the checks pass,
and `implement-epic` merges its own PRs without pausing.

The checklist above **survives as a self-checklist** — run by whoever opens the PR, and carried
into the M2 "how to write here" page as the review checklist a contributor applies to their own
work. It is what the CI cannot see:

1. every claim verifiable against the code as it is today;
2. citations naming what was actually read;
3. maturity marker matching reality rather than intent;
4. no contradiction with the owning repo's docs (criterion 5);
5. reads like the rest of the wiki.

`main` stays protected — no force-push, no direct push, CI green required — which is baseline and
unchanged.

**The trade this makes, stated plainly.** Criterion 1 (no false information) now has no human
gate: a page asserting something untrue merges the moment the build is green. Two consequences
follow, and they are not optional if this verdict is to hold:

- **Every convention that can become a check must become one.** A rule enforced only by a
  self-checklist is enforced by the same person who just broke it. This raises rather than lowers
  the stakes on the validator rules proposed in
  [placeholder phrasing](/conventions/09-placeholder-phrasing.md) and
  [stamping](/conventions/12-stamping-and-done.md) — they were the optional-looking half of M1's
  tooling and are now the only thing standing where review used to.
- **The weekly staleness issue and the freshness table become the after-the-fact review**
  ([decision](/specs/14-freshness-automation.md)) — the place a wrong page is caught, later,
  rather than at merge.

Revisit if a false claim reaches the site and the checks could not have caught it: the answer is
then a new check, and only if none is possible, an approval requirement on that area.
