---
type: Epic
title: "Project map & freshness"
description: "Give maintainers one transverse view across repos, and keep the wiki honest about what has gone stale."
tags: [epic]
resource: https://github.com/kern-ia/kern-wiki/issues/4
timestamp: 2026-08-01T02:20:00Z
epic: 4
slug: project-map-freshness
status: open
gh_issue: 4
milestone: 4
source: docs/planning/SCOPE.md#milestone-4-project-map--freshness
---

# Epic 4: Project map & freshness

## Goal

Maintainers have N roadmaps across repos that each move weekly, and no transverse view. Knowledge
that belongs to no single repo — the `Kern-Orch × kern-link` compatibility analysis is a document
about the *seam* between two bricks — has nowhere to live at all.

This epic gives maintainers one place to see where the project stands, and adds the automation that
keeps the rest of the wiki from quietly going stale.

Serves journey **J5** (see where the project stands).

## Scope

- **Transverse status** across the repos, plus a consolidated roadmap.
- **Open architectural questions**, each linked to the per-repo issues: the `kern-agent` bridge, the
  five pending agent-protocol extensions, a possible `kern-contracts` extraction, the module-path
  migration, and the `.github` cleanup.
- **CI link checker.**
- **Staleness check** — a scheduled job comparing each page's version stamp against the brick's
  latest release, and opening **one issue** listing what moved.

Three page states must stay distinguishable throughout the wiki: *not documented yet*, *verified
against version X*, *possibly stale*.

## Out of scope

- **No versioned documentation trees** — latest only. *Deferred.*
- **No executed-quickstart CI job** — this is the real fix for the quickstart breaking on a contract
  bump, and it is deliberately deferred past this epic; the version stamp is the interim mitigation.
  *Deferred.*
- **No blog or changelog aggregation.** *Deferred.*
- **No `.github` cleanup** — it is recorded here as an open question, not performed. *Deferred.*
- **No repo renames or module-path migration** — this epic *flags* the migration as an open
  architectural question; the breaking change stays owned by each repo. *Deferred.*
- **No changes to brick code** — findings become issues on the brick. *Rejected.*

## Acceptance criteria

9. **The transverse status page actually gets used to pick a next task.**

The staleness job opens a single consolidated issue rather than one per page, and the three page
states remain distinguishable.

## Dependencies

Depends on [Epic 1](/epic-1-the-frame/EPIC_1.md): the version stamps and the freshness table are
what the staleness job reads, and the "what's missing" page is where the open architectural
questions start.

Benefits from [Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md) having stamped technical
pages to check — but does not block on it, and the link checker and status page are useful from the
moment the frame exists.

## Context

- [Technical specs](../../planning/SPECS.md)
- [Conventions](../../planning/CONVENTIONS.md)

## Notes

**Project-wide constraints relevant here:**

- **Zero budget** — GitHub Pages and GitHub-native tooling only; the scheduled staleness job and the
  link checker are GitHub Actions.
- **No invented content** — the status page reports what the repos say, and marks the rest as not
  known.
- **Upstreams move weekly and are pre-1.0** — which is the reason this epic exists at all.

**This epic is the wiki's answer to its worst risk** — a page that is confidently wrong rather than
merely dead-linked. The ownership map and version stamps come from epic 1; the automation that
*acts* on them is here.

**Open unknown carried in:** the bricks each carry a licence, but only `kern-link` advertises MIT
and the licence audit is out of scope. If the status page lists licences, it lists them as unknown
where they are unknown.
