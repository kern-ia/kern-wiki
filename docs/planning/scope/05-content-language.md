---
type: Decision
title: "Content language"
description: "Is the wiki written in English, French, or both?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 05
slug: content-language
status: decided
verdict: "Documents authored in English; the published site is bilingual EN/FR"
decided_via: triage
depends_on: [target-audiences]
---

# Question

The project's language usage is currently mixed: all four repo READMEs are in English,
the org tagline is French ("Kern - L'IA qui s'emploie."), and several internal docs are
French (`Kern-Orch/docs/GLOSSAIRE.md`, `Kern-UI/docs/a-trancher.md`,
`docs/brainstorming_28_07_2026.html`). The maintainer is French-speaking.

# Options

- **English only** — matches the READMEs, matches the Go/OSS ecosystem, one copy to
  maintain. French-speaking readers are all technical and read English docs daily.
- **French only** — natural for the maintainer, and consistent with the brand tagline.
  Shrinks the potential contributor pool to a fraction of it.
- **Bilingual** — widest reach, and doubles the maintenance surface for a solo
  maintainer. In practice one language rots.

# Recommendation

English only for all published wiki content, keeping the French tagline as brand.
Bilingual as an explicit non-goal for v1, with nothing in the structure preventing a
French tree later.

# Verdict

**Split decision, chosen by the user:** the *documents* are authored in **English**, and
the *published GitHub Pages site* is **bilingual EN/FR**.

So English is the source language — every page is written and reviewed in English first,
and no French page exists without an English original. French is a translation layer on
the site, not a parallel authoring track.

Two consequences, both recorded downstream rather than argued here:

- The site must carry a language switch and a per-language tree, which raises the bar on
  the generator pick in `define-specs`
  ([decision](/scope/03-delivery-form.md)).
- Translating pages that describe still-moving packages would double the churn. Hence the
  scoping rule adopted in [decision](/scope/17-milestones.md): French covers the **stable
  front-door pages** (overview, ecosystem diagram, glossary, quickstart) and explicitly
  **not** the per-brick technical documentation while the packages are unstable
  ([decision](/scope/07-coverage-depth.md)). The French edition gets its own milestone so
  it cannot silently block the English one.

The consolidated glossary is a special case worth noting: its source material
(`Kern-Orch/docs/GLOSSAIRE.md`) is French, so here English is the *translation* and French
the original — the one page where the FR version is guaranteed to be the more natural read.
