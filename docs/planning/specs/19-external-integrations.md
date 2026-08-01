---
type: Decision
title: "External integrations"
description: "Which third-party services does the wiki depend on, and what is the fallback posture for each?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 19
slug: external-integrations
status: na
verdict: "N/A as a standalone decision — the only integrations are GitHub itself and outbound links, both decided elsewhere"
decided_via: na
depends_on: [freshness-automation, secrets-and-access]
---

# Question

Which third-party services can take the wiki down or make it wrong?

# Verdict

**N/A as a standalone decision.** The zero-budget, GitHub-native constraint
([decision](/scope/15-constraints.md)) leaves nothing to integrate with. The three touchpoints
that exist are each decided in their own doc, and each already carries its fallback posture:

- **GitHub Pages + Actions** — the platform, not an integration
  ([decision](/specs/11-hosting-and-deployment.md)). If Actions is down, the published site keeps
  serving; only new deploys wait.
- **The GitHub API**, read weekly by the staleness job
  ([decision](/specs/14-freshness-automation.md)). Degrade, never hard-fail: the job's failure
  affects an issue nobody is blocked on, and the site is untouched.
- **Outbound links** to `pkg.go.dev` and the brick repos, which are content rather than runtime
  dependencies. Rot is caught by the weekly external link check
  ([decision](/specs/12-ci-checks.md)); it makes a page wrong, not the site broken.

Search is deliberately offline and client-side ([decision](/specs/10-search.md)) and analytics
deliberately absent ([decision](/specs/16-observability-and-analytics.md)), which is what keeps
this list at three.
