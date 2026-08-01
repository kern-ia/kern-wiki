---
type: Decision
title: "Freshness automation (staleness job)"
description: "How does the M4 staleness check learn that a brick moved past a page's version stamp?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 14
slug: freshness-automation
status: decided
verdict: "Weekly job comparing each page's stamp against the latest release, with a commit-count fallback, writing one rolling issue; never auto-stamps"
decided_via: triage
depends_on: [page-metadata, tooling-language, secrets-and-access]
---

# Question

Scope decided the mechanism in outline: a scheduled job comparing each page's version stamp
against the brick's latest release, opening **one** issue listing what moved
([decision](/scope/16-freshness-and-versioning.md)). It lands in M4, but its input — the stamp
format — is fixed at M1 ([decision](/specs/05-page-metadata.md)), so the shape has to be decided
before the templates are written.

The bricks are pre-1.0, move weekly, and live in repos with inconsistent naming and inconsistent
release discipline (`github.com/julienlegoux/kern-link`, `github.com/yoann/kern-orch`). "Latest
release" may not exist for every brick.

# Options

- **Compare against latest release tag** — cheap, meaningful, and silent for a brick that has
  never cut a release.
- **Compare against the default branch head commit** — always available, and fires on every
  README typo. Noise that trains people to ignore the issue.
- **Compare against latest release, falling back to commit count since the stamped ref** — real
  releases where they exist; elsewhere, "37 commits since you last checked", which is a signal a
  human can weigh.
- **Executed documentation** — run the quickstart against real bricks. The only thing that
  catches *wrong* rather than *old*; explicitly deferred by scope.

# Recommendation

**Latest release, with commit-count fallback**, run weekly, writing to **one rolling issue**.

- **Reads metadata only** — the GitHub API's releases and compare endpoints, resolving each page's
  OKF `resource` URL to a repository ([decision](/specs/05-page-metadata.md)). No checkouts, no Go
  builds of other repos, no minutes worth worrying about.
- **One issue, updated in place** (`stale-docs` label, edited body) rather than a new issue per
  run. A weekly issue stream is a mute button waiting to happen.
- **Output distinguishes the three states** by construction: placeholders are listed separately
  as *not documented yet* rather than as stale, because `doc_state: placeholder` pages carry no
  stamp to compare ([decision](/scope/16-freshness-and-versioning.md)).
- **No auto-editing of pages.** The job never touches `verified.date` — a stamp means *a human
  read the code at that version*, and a bot refreshing it would turn the wiki's central honesty
  mechanism into a lie.
- **Unknown repos fail loudly**: a page stamped against a `resource` the job cannot resolve is
  reported as an error, not skipped. Silent skipping is how a stamp stops meaning anything.

The ordering weakness scope already named — automation in M4, after M3 writes the pages it
governs — is unchanged and accepted. The mitigation is that stamps and the freshness table exist
by hand from M1, so M4 automates an existing practice.

# Verdict

**Weekly, latest release with commit-count fallback, one rolling issue**, accepted at triage.
Metadata only, resolved through each page's OKF `resource`. Placeholders are reported as *not
documented yet* rather than as stale, unresolvable resources are errors rather than skips, and the
job never edits a page — a stamp means a human read the code, and a bot refreshing it would turn
the wiki's central honesty mechanism into a lie.

Lands in M4 as scope ordered it, automating a stamping practice that exists by hand from M1.
