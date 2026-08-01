---
type: Decision
title: "PR size and the unit of change"
description: "The baseline's ~500-line PR target is calibrated for code; a single brick page from the template may exceed it truthfully."
tags: [decision, conventions]
timestamp: 2026-08-01T09:18:00Z
phase: conventions
decision: 5
slug: pr-size-and-unit
status: decided
verdict: "no PR-size rule in the conventions — sizing and grouping belong to split-epics and create-issues; conventions state only that a content page is not split across PRs"
decided_via: discussion
depends_on: []
---

# Question

The baseline targets roughly 500 changed lines per PR and never approaches 1000, matching how
`create-issues` sizes issues. That number encodes reviewer fatigue over *code*. Prose has a
different density: a brick page instantiated from the M1 template — identity, maturity,
exposed/needs, install, configuration, usage, integration, citations — plausibly lands at 250–400
lines, and the four brick pages of M1 arrive together. Meanwhile a 40-line prose diff can contain
a claim that is confidently wrong, which is the failure mode this project actually fears.

Lines are the wrong unit for the artifact that dominates this repo.

# Options

- **Keep 500/1000 everywhere** — would split a single page across PRs, so a reviewer never sees
  a page whole. For a page whose job is internal coherence, that is a real loss.
- **Size by subject for content, by lines for tooling** — one page (or one coherent section
  edit) per PR, uncapped; `tools/` keeps the baseline's 500/1000.
- **No size rule at all** — with two contributors and self-review pressure, the M1 frame arrives
  as one 3000-line PR nobody reads.

# Recommendation

**Size by subject for content, by lines for tooling.**

- **Content PR = one subject**: one page, or one section's worth of a coherent change (e.g.
  "instantiate the four brick pages from the template, all placeholdered" is one subject; "fill
  kern-orch's configuration section" is another). No line cap, but **no second subject** — a PR
  that both adds a page and adjusts the template is two PRs.
- **`tools/` PR**: the baseline's ~500 lines, never approaching 1000, unchanged.
- **Generated blocks don't count** toward any size judgement — they are regenerate-and-diff
  output ([decision](/specs/06-registries-and-tables.md)), reviewed by the fact that CI
  reproduced them, not by reading.
- A PR closes exactly one issue via `Closes #<n>`, and branches stay `issue-<n>-<slug>` — both
  baseline, both unchanged.

Read the trade honestly: this removes the mechanical guard against a huge PR. What replaces it is
the one-subject rule, which is the guard that matters for prose — a reviewer can check a claim
against the code only if the PR is *about* one thing.

# Verdict

**None of the above: the conventions carry no PR-size rule at all.** Sizing and grouping work is
the job of `split-epics` and `create-issues`, which already decide what one PR contains; a line
target restated here would be a second source of truth for a number those skills own, and the
baseline's 500/1000 is guidance *to them*, not to this repository.

What the conventions keep is the one fact those skills cannot derive from a line count, because
it is a property of the artifact rather than of the sizing policy:

- **A content page is not split across PRs.** Its correctness is internal coherence — template
  order, one maturity claim, citations matching the stamp — which a reviewer can only judge
  whole. Splitting *within* a page is the one grouping choice that is wrong regardless of size.
- Correspondingly, `create-issues` sizes content issues by subject rather than by lines. Recorded
  as input to that skill, not as a rule enforced here.

The baseline's PR-size bullet is therefore **not applied** to this project's content, and applies
to `tools/` only as the general guidance it already is.

> **Promotion candidate.** The rationale is not project-specific: PR size and grouping belong to
> `create-issues` in every project, so a conventions document restating them will always
> duplicate. Suggest amending `assets/baseline.md` to state the ownership boundary instead of a
> number — via the improve-skill loop, not in this run.
