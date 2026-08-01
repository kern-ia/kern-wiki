---
type: Decision
title: "Repo location & hosting"
description: "Which repo holds the wiki, and where does it publish?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 04
slug: hosting-and-location
status: decided
verdict: "Dedicated repo kern-ia/kern-wiki, published with GitHub Pages; custom domain deferred"
decided_via: triage
depends_on: [delivery-form]
---

# Question

Local working directory is `D:\Project\wiki-kern`, not yet a git repo. Where does it
live in the org, and at what URL does it publish? Existing repo names are inconsistent
(`kern-link` lowercase, `Kern-Anon`/`Kern-Orch`/`Kern-UI` capitalized).

# Options

- **Dedicated repo `kern-ia/kern-wiki`, Pages at `kern-ia.github.io/kern-wiki`** —
  fits the `kern-*` family, its own issues/milestones (which the downstream
  `split-epics` → `create-issues` pipeline needs), free hosting. URL has a path prefix.
- **Dedicated repo `kern-ia/kern-ia.github.io`, Pages at the org root URL** — cleanest
  URL with no custom domain, but the repo name breaks the `kern-*` family and reads as
  infrastructure rather than a brick.
- **Inside the `.github` repo** — no new repo. Wrong tool: `.github` exists for org-wide
  community health files and templates, its history would mix governance with content,
  and Pages from `.github` is awkward.
- **Custom domain (e.g. `kern.dev`)** — nicest, costs money and a DNS setup, and
  nothing depends on it for v1.

# Recommendation

**Dedicated repo `kern-ia/kern-wiki`, published with GitHub Pages** (branch or Actions
workflow — a specs detail). It gives the project its own milestone/issue space, which
this planning pipeline requires, and it names itself as part of the family. A custom
domain is a later, purely additive step: adding a `CNAME` later changes no content and
breaks no internal link, so buying a domain now would be premature.

Separately: the org profile README (`kern-ia/.github/profile/README.md`) becomes a
short pointer to the site rather than a duplicate of it.

# Verdict

**Dedicated repo `kern-ia/kern-wiki`, published with GitHub Pages**, custom domain
deferred. Accepted at triage.

Amended: the org profile README (`kern-ia/.github/profile/README.md`) is **not a deliverable**.
The user confirmed `.github` stays untouched ([decision](/scope/08-governance-content.md)), so
`github.com/kern-ia` remains silent in v1 — the site is the only front door, reached by link
rather than by landing on the org.
