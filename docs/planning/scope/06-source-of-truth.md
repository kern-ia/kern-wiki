---
type: Decision
title: "Source of truth vs the repos"
description: "Does the wiki copy repo documentation, link to it, or generate from it?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 06
slug: source-of-truth
status: decided
verdict: "Self-contained wiki: it hosts its own content, duplication with repos accepted and bounded by an ownership map"
decided_via: discussion
depends_on: [delivery-form, hosting-and-location]
---

# Question

Every brick already carries real documentation: `kern-link/docs/{architecture,auth,usage}.md`,
`Kern-Anon/docs/index/*` (17 files), `Kern-Orch/docs/{ARCHITECTURE,GLOSSAIRE,ROADMAP}.md`
plus 19 index docs, `Kern-UI/docs/*`. All five repos move weekly. What is the wiki's
relationship to that material?

This is the decision that determines whether the wiki survives its first month.

# Options

- **Link, never copy** — the wiki owns only content that has no repo home and deep-links
  everything else. Cannot drift on content it doesn't hold; can drift on *links*.
- **Self-contained** — the wiki holds real content, readable without leaving the site.
  Best reading experience; accepts duplication against five moving upstreams.
- **Generate at build time** — CI pulls repo docs and renders them into the site. No
  content drift, real machinery to build and debug, and pulled pages read oddly out of
  the repo context they were written for.

# Recommendation

Link, never copy — treated as a hard rule, on the grounds that a solo maintainer cannot
keep a copy in sync with five weekly-moving repos, and that "zero duplicated prose" is
then a checkable success criterion.

# Verdict

**Overruled by the user: the wiki is self-contained.** Sending a reader from a GitHub
Pages site out to a markdown file in another repo is a bad experience ("un peu barbare"),
and the wiki is only worth having if it is actually readable on its own. Some duplication
with repo docs is accepted as the price.

The recommendation's underlying worry is real, so the verdict bounds duplication instead
of denying it — an **ownership map**, written on the wiki and applied per topic:

| Subject | Authoritative home |
|---|---|
| How to install / configure / use a brick, integration between bricks, examples | **Wiki** |
| Ecosystem overview, vocabulary, contribution rules, transverse status | **Wiki** |
| API signatures | `pkg.go.dev` (never re-typed by hand) |
| Internal architecture, design/dev logs (`docs/index/*`), retros | **Repo** |
| `kern.*` contract JSON fixtures | **Repo**, CI-enforced ([decision](/scope/09-contract-registry-home.md)) |
| Release history (`CHANGELOG.md`) | **Repo** |

Two rules follow, and they are what keep this from rotting:

1. **No page duplicates a subject the map assigns elsewhere.** Where both sides
   inevitably say something about the same thing, the wiki states the *usage* view and
   links the repo for the internals — duplication of subject, not of claims.
2. **Every technical page is stamped** with the brick version/commit and date it was
   verified against, so staleness is visible rather than silent
   ([decision](/scope/16-freshness-and-versioning.md)).

Build-time generation stays rejected for now: the usage documentation the wiki hosts does
not exist in the repos to be pulled — it has to be written.
