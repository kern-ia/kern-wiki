---
type: Decision
title: "Background work"
description: "Are there async jobs, queues or schedulers?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 21
slug: background-work
status: na
verdict: "N/A — no runtime; the only scheduled work is GitHub Actions cron, decided in 12 and 14"
decided_via: na
depends_on: [ci-checks, freshness-automation]
---

# Question

Does anything run outside a request, and does it need a queue or a scheduler?

# Verdict

**N/A.** There is no application runtime, so there is nothing to enqueue. The two recurring jobs
are GitHub Actions cron workflows, and both are decided in their own docs: the **weekly external
link check** ([decision](/specs/12-ci-checks.md)) and the **weekly staleness job**
([decision](/specs/14-freshness-automation.md)).

Both are idempotent, stateless, read-only against other repos, and produce at most one issue in
this repo — so retries, ordering and back-pressure, the reasons this checklist item exists, do not
arise.
