---
type: Decision
title: "Milestones / phasing"
description: "How does the work phase into independently shippable chunks?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 17
slug: milestones
status: decided
verdict: "Five milestones: Frame → Conventions & contribution → Package docs → Project map & freshness → French edition"
decided_via: triage
depends_on: [mvp-cut, target-audiences, governance-content]
---

# Question

This becomes the `## Milestone N:` headings in `SCOPE.md`, which `split-epics` cuts into epics —
one milestone ≈ one epic, weeks-sized, independently shippable.

**Refreshed twice.** The three-milestone shape assumed link-only pages, `.github` in scope and
an English-only site. The five-milestone shape assumed v1 was finished content. Two new facts
reorder things: the project is **structure-first, filled progressively**
([decision](/scope/20-documenting-the-gap.md)), and there are **two contributors with more
expected** ([decision](/scope/15-constraints.md)).

# Options

- **Frame → package docs → contribution → map → French** — the previous order, with
  conventions arriving after the bulk of the writing.
- **Frame → conventions/contribution → package docs → map → French** — conventions before
  volume, so several people fill the frame the same way.
- **Per-brick milestones** — finest tracking; fragments the cross-cutting work (contracts,
  contribution, status, French) across everything.

# Recommendation

**Frame → conventions/contribution → package docs → map → French.** The reorder is the point:
with two contributors and packages still arriving, the conventions have to exist *before* the
bulk filling, or the second person fills the frame differently and the whole structure-first
argument collapses. In the previous ordering the contribution milestone came after the package
documentation — which would have meant writing the rules once the pages that needed them were
already written three ways.

**M1 — The frame.** The thirteen deliverables in [decision](/scope/12-mvp-cut.md): repo +
Pages, information architecture, page templates, the placeholder/maturity convention, overview,
ecosystem diagram with the gap, four templated brick pages (partly placeholdered), contracts
registry, quickstart, glossary, ownership map, freshness table, "what's missing". English.
Serves J1–J3. Everything after is filling and automating.

**M2 — Conventions & contribution surface** *(contributors; J4)*: how to write a page here
(templates, markers, stamps, the no-invented-content rule as an enforceable review checklist),
the contribution process, the brick-authoring guide — *what makes something a `kern-*` brick*,
including the exposed/needs declaration a new package must publish — and how to add a contract
entry when the next one lands. **No writes to `kern-ia/.github`**
([decision](/scope/08-governance-content.md)); that integration is separate, later work.

**M3 — Progressive package documentation** *(adopters; J6)*: fill each brick's section against
the template — install, configuration, usage patterns, worked examples, integration over the
`kern.*` contracts — replacing placeholders as knowledge settles, and covering the fifth package
once it lands. Includes the operational traps the compat analysis surfaced (env propagation
under `kern-orch serve`, **API keys only** for daemon mode rather than OAuth). The largest
milestone; expect `create-issues` to cut it roughly one brick at a time.

**M4 — Project map & freshness** *(maintainers; J5)*: transverse status across the repos,
consolidated roadmap, open architectural questions (the `kern-agent` bridge, the five pending
protocol extensions, a possible `kern-contracts` extraction, module-path migration, the
`.github` cleanup) linked to per-repo issues, CI link checker, staleness check
([decision](/scope/16-freshness-and-versioning.md)).

**M5 — French edition**: `fr/` tree and language switch, translating the **stable front-door
pages only** — overview, diagram, glossary, quickstart, and the conventions page if it has
settled. Deliberately **not** the M3 technical sections while the packages move
([decision](/scope/05-content-language.md)).

Ordering notes: M1 is a hard prerequisite for everything. M2 before M3 is the deliberate
change. M4 is independent of M2/M3 and can move earlier if the transverse view becomes urgent.
M5 is last so translation chases settled prose — a one-line swap if bilingual-at-launch matters.

# Verdict

**Five milestones, in the reordered sequence**, accepted at re-triage: M1 The frame → M2
Conventions & contribution surface → M3 Progressive package documentation → M4 Project map &
freshness → M5 French edition.

The reorder (conventions ahead of the bulk writing) is the substantive change, driven by there
being two contributors with more expected ([decision](/scope/15-constraints.md)). These five
headings become the epic boundaries `split-epics` cuts on.
