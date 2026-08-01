---
type: Decision
title: "Performance & scale targets"
description: "What load and latency must the wiki handle?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 20
slug: performance-and-scale
status: na
verdict: "N/A — pre-rendered static pages on a CDN; no target worth architecting for"
decided_via: na
depends_on: [hosting-and-deployment]
---

# Question

Is there a load or latency budget that should shape the architecture?

# Verdict

**N/A.** Every page is pre-rendered and served from GitHub's CDN; search runs in the reader's
browser ([decision](/specs/10-search.md)). There is no origin to saturate and no query to
optimise. Stating a target would only invite gold-plating, which is the failure this checklist
item exists to prevent.

The only budget that could bind is GitHub Pages' soft limits — a 1 GB site and a 100 GB/month
bandwidth allowance — and a text wiki with Mermaid source instead of images
([decision](/specs/08-diagrams.md)) is orders of magnitude below both.

The one number this project does care about is human, not machine: **under 15 minutes from the
site to a running hello graph** ([decision](/scope/14-success-criteria.md)). It is a content and
navigation property, verified by running the quickstart, not by anything decided here.
