---
type: Decision
title: "Problem & job-to-be-done"
description: "What pain does the Kern wiki solve, and for what job?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 01
slug: problem-statement
status: decided
verdict: "Front door + ecosystem glue — widened to include a usage manual"
decided_via: triage
depends_on: []
---

# Question

`kern-ia` is five public repos two weeks old: `kern-link` (unified Go LLM API),
`Kern-Anon` (PII detection/anonymization), `Kern-Orch` (graph agent orchestration),
`Kern-UI` (live run visualization), and an empty `.github`. Each repo documents itself
well *for someone already inside it*. Nothing documents Kern.

Concretely, today:

- The org profile is empty (`.github` holds only a `.gitkeep`), so github.com/kern-ia
  says nothing about what Kern is.
- No page explains why Kern is four autonomous bricks rather than one binary, or how
  they connect (`kern.step-event/v2` is the connective tissue and it is only visible
  inside two READMEs).
- Cross-cutting knowledge is either duplicated (the "CANONICAL BLOCK" mirrored verbatim
  between `Kern-Orch` and `Kern-UI`) or trapped in one repo (`Kern-Orch/docs/GLOSSAIRE.md`
  defines the ecosystem's vocabulary; `Kern-Orch/docs/ROADMAP.md` is per-brick).
- Nothing tells an outsider how to contribute, and nothing gives the maintainer a
  transverse view of five moving repos.

What job is this project actually hired for?

# Options

- **Front door + ecosystem glue** — the wiki owns only what no single repo can own
  (what Kern is, how bricks fit, vocabulary, contribution rules, transverse roadmap)
  and deep-links everything brick-specific. Small surface, low maintenance, but the
  reader crosses to GitHub for detail.
- **Central documentation** — the wiki absorbs and re-hosts per-brick documentation so
  everything is readable in one place. Best reading experience, worst drift: five repos
  moving weekly against one hand-maintained copy.
- **Internal knowledge hub only** — a maintainer's map (status, decisions, next steps).
  Cheapest, but leaves the public-facing gap that made the org look empty in the first
  place.

# Recommendation

**Front door + ecosystem glue.** The pain is not "the docs are bad" — per-repo docs are
unusually good. The pain is that *there is no Kern*, only four repos that happen to share
a prefix. The job is to make the ecosystem comprehensible and contributable from one
entry point **without becoming a second copy of anything**, because a solo maintainer
cannot keep a copy in sync with five repos.

# Verdict

**Front door + ecosystem glue**, accepted at triage.

Widened by two later verdicts: the wiki also *hosts* per-brick usage documentation
([decision](/scope/06-source-of-truth.md), [decision](/scope/07-coverage-depth.md)), so
the job is "make Kern comprehensible **and usable** from one place" — a front door and a
usage manual. Repos keep authoritative internals (architecture, dev logs, contracts,
`CHANGELOG`, API via `pkg.go.dev`).

Sharpened once more by [decision](/scope/20-documenting-the-gap.md): the ecosystem is still being
designed and packages are still arriving, so the job in its final form is **to build the frame
that documentation lands in** — templates, markers, a contracts registry, a placeholder
convention — and fill it as things settle, without ever asserting something that isn't true.
