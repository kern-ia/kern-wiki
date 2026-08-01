---
type: Decision
title: "Open-source governance files"
description: "Who owns CONTRIBUTING, code of conduct, security policy, licence and templates — the wiki or the .github repo?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 08
slug: governance-content
status: decided
verdict: "The .github repo is out of scope for now; the wiki documents the contribution process only"
decided_via: discussion
depends_on: [target-audiences, hosting-and-location]
---

# Question

The user's framing was "organizing the structure around an open source project", of which
the wiki is one part. Today `kern-ia/.github` contains only a `.gitkeep`, so the org has
no CONTRIBUTING, no code of conduct, no security policy, and no issue/PR templates. Only
`kern-link` advertises a licence (MIT); the others' licence status is unverified.

Does this project produce those files, and where do they live?

# Options

- **`.github` repo owns the files, the wiki explains the process** — GitHub inherits
  org-level community-health files across every repo that lacks its own, so one write
  serves all five.
- **The wiki owns everything** — one place, but GitHub will not surface a wiki page in the
  "Contributing" affordances on issues and PRs, so the files don't exist where
  contributors meet them.
- **Out of scope** — wiki only; governance files handled separately later.

# Recommendation

`.github` owns the files, the wiki explains the process, and this project produces both —
since they are the same job and pointless apart — plus a licence audit across the four
bricks.

# Verdict

**Out of scope for now, per the user.** The `kern-ia/.github` repo is currently more an
experiment than a settled thing: its contents were not deliberately chosen, they came
from automatic scaffolding, and the user is not in a position to validate them. Writing
org-wide governance files *through* a repo he can't yet vouch for would push unvalidated
rules onto all five bricks — worse than having none.

So: **this project does not touch `kern-ia/.github`.** Integration comes later, once that
repo is itself cleaned up and understood — a separate piece of work, not a milestone here.

What survives inside scope, because it needs no `.github` write:

- The wiki's own **contribution-process page** (how to set up, conventions, how the
  `kern.*` contracts work, where to open an issue) — the narrative half of the original
  recommendation, and enough to serve journey J4.
- The **brick-authoring guide** ("what makes something a `kern-*` brick").

What is explicitly *not* produced: `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`,
`SECURITY.md`, issue/PR templates, and the licence audit
([non-goals](/scope/13-non-goals.md), deferred).

Two consequences flagged rather than hidden:

- The **org profile README** lives at `.github/profile/README.md`, and the user confirmed the
  exception is refused: `.github` stays untouched, so `github.com/kern-ia` stays empty in v1.
  Dropped from the MVP ([decision](/scope/04-hosting-and-location.md),
  [decision](/scope/12-mvp-cut.md)) and recorded as a non-goal
  ([decision](/scope/13-non-goals.md)).
- Contributors will find a contribution page on the site but no `CONTRIBUTING.md` where
  GitHub shows one. Accepted; recorded as a risk
  ([decision](/scope/18-risks-and-assumptions.md)).
