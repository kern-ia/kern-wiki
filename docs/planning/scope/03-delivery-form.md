---
type: Decision
title: "Delivery form"
description: "What does the reader actually receive: a GitHub Wiki, a website, or markdown in a repo?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 03
slug: delivery-form
status: decided
verdict: "Generator-agnostic markdown in a repo, published as a GitHub Pages site"
decided_via: triage
depends_on: [target-audiences]
---

# Question

The user said "wiki". That word covers three very different products. This decides the
*form*, not the tooling — which static-site generator (if any) is a `define-specs`
decision.

# Options

- **GitHub Wiki tab** — the literal feature. Zero setup, editable in the browser. But:
  content lives in a separate hidden git repo, changes cannot go through pull-request
  review, no CI (so no link checking), weak deep-linking, poor discoverability, and
  contributors cannot use the normal fork→PR flow. Actively hostile to audience 2.
- **Markdown in a normal repo, read on GitHub** — plain `.md` files, reviewed via PR,
  no build, no site. Zero infrastructure. Reads acceptably on GitHub, renders Mermaid
  natively, but no search, no navigation, no landing page.
- **Markdown in a normal repo + generated site on GitHub Pages** — same files, plus a
  build step producing a searchable, navigable site. PR-reviewable, CI-checkable,
  linkable from the org profile. Cost: one generator to pick and a Pages workflow.

# Recommendation

**Markdown in a normal repo + generated site on GitHub Pages**, with one constraint that
makes it strictly better than the middle option: **write plain, generator-agnostic
markdown** — no shortcodes, no generator-specific syntax — so every page stays fully
readable on GitHub even if the site build breaks or the generator is swapped. That makes
option 2 a permanent fallback rather than a competing choice, and defers the
generator pick to `define-specs` without blocking content work.

Reject the GitHub Wiki tab despite the project's name: it cannot serve contributors
(no PR review, no CI), and it is the one form you cannot migrate away from cheaply.
"Wiki" stays as the project's name; the delivery is a documentation site.

# Verdict

**Generator-agnostic markdown in a repo, published as a GitHub Pages site**, accepted at
triage. The GitHub Wiki tab is rejected. "Wiki" stays the project's name; the delivery is
a site.

Two later verdicts raise the bar on the generator pick, which stays a `define-specs`
decision: it must support a **bilingual tree with a language switch**
([decision](/scope/05-content-language.md)) and enough navigation to carry per-brick
usage documentation ([decision](/scope/07-coverage-depth.md)).
