---
type: Decision
title: "Target audiences"
description: "Who is v1 for, and in what order are the audiences served?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 02
slug: target-audiences
status: decided
verdict: "All three audiences, phased external → contributors → maintainer"
decided_via: triage
depends_on: [problem-statement]
---

# Question

Three plausible audiences, already stated by the user as "all three, phased, order
doesn't matter much". So the real remaining question is the *phasing order*, since it
sets the milestone order and therefore the epic order downstream.

The three:

1. **External users** — Go developers who could use a brick (or the whole ecosystem)
   but have never heard of Kern.
2. **Contributors** — developers who want to fix, extend, or add a brick and currently
   have no CONTRIBUTING, no code of conduct, no brick-authoring guide.
3. **The maintainer** — you, needing a transverse map across five repos.

# Options

- **External → contributors → maintainer.** Public gap first (the org profile is the
  most visible hole), then the contribution surface, then the internal map.
- **Maintainer → external → contributors.** Scratch your own itch first; the internal
  map is the cheapest to write because the material already exists in repos.
- **Contributors → external → maintainer.** Optimize for attracting help earliest.

# Recommendation

**External → contributors → maintainer.** Not because external users matter most
(there are zero today), but because writing for a stranger is what forces the ecosystem
story to actually exist. The overview, the diagram, and the vocabulary produced in that
first pass are then *reused verbatim* by the contributor pages and the maintainer map —
whereas starting internal produces notes that need rewriting before anyone else can read
them. Each audience gets one milestone, so nothing is dropped, only ordered.

# Verdict

**All three audiences, phased external → contributors → maintainer**, accepted at triage
("les trois, pas besoin de priorité, juste phasée").

A fourth reader is implied by [decision](/scope/07-coverage-depth.md): the developer who
adopts *one* brick inside their own project without caring about the ecosystem. Treated
as a sub-case of audience 1, and it gets its own journey J6 in
[decision](/scope/11-core-journeys.md).

**Amended:** the contributor audience is not hypothetical — there are **two contributors today,
with more expected** ([decision](/scope/15-constraints.md)). That doesn't change the audience
list, but it changes its weight: contributors are a present, internal audience whose first need
is *how to write in this wiki*, not *how to get commit access*. Hence the conventions milestone
moving ahead of the bulk writing ([decision](/scope/17-milestones.md)).
