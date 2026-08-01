---
type: Decision
title: "Go module-path migration"
description: "Should this project migrate module paths from julienlegoux/* to kern-ia/*?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 19
slug: module-path-migration
status: na
verdict: "Not applicable — belongs to each brick repo"
decided_via: na
depends_on: [naming-and-identity]
---

# Question

`kern-link/go.mod` declares `github.com/julienlegoux/kern-link` and its badges point at
the personal account, while the repo now lives under `kern-ia`. The same is likely true of
the other three bricks. Writing install instructions forces the issue into view, so it
must be visible in the ledger rather than silently ignored.

# Options

Not applicable — see reason.

# Recommendation

**N/A for this project.** Changing a Go module path is a breaking change for importers and
touches imports across every file, plus CI, badges, and `pkg.go.dev` — it is brick work
requiring per-repo release decisions, and it cannot be done correctly from a documentation
repo. This project instead: documents the *current* paths so instructions are true today,
opens one issue per affected repo, and surfaces the migration on the M3 open-questions
page ([decision](/scope/10-naming-and-identity.md),
[risk](/scope/18-risks-and-assumptions.md)).

Reclassify this to `open` at triage if you want the migration inside this project's
scope — it would add a fourth milestone touching four repos.

# Verdict

Recorded as N/A at enumeration: out of a documentation project's reach, tracked as a
risk and as per-repo issues instead.
