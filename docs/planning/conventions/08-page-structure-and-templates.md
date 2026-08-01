---
type: Decision
title: "Page structure, templates and where the authoring rules live"
description: "How binding are the M1 templates, and is CONVENTIONS.md or the published contributing page the source of truth?"
tags: [decision, conventions]
timestamp: 2026-08-01T09:24:00Z
phase: conventions
decision: 8
slug: page-structure-and-templates
status: decided
verdict: "templates binding on section set and order (validator-checked), free below `###`; CONVENTIONS.md is the source and the M2 page its rendering; enforced rules are never re-specified in prose"
decided_via: triage
depends_on: [planning-bundle-location, tdd-scope]
---

# Question

M1 delivers a brick template and a contract template; M2 delivers a "how to write here" page.
SPECS decided *where* templates live (`templates/`, never published) but not **how binding** they
are — whether a page may add, drop or reorder sections. Extensibility (criterion 2) says adding a
brick is filling a slot; uniformity (criterion 6) says pages match without asking. Both fail if
the template is a suggestion.

Second, sharper question: after this skill writes CONVENTIONS.md, the project will have *two*
documents stating authoring rules — this one, and M2's published page. Two sources of truth for
the rule set whose entire purpose is consistency is a self-inflicted wound.

# Options

- **Templates advisory** — write what the page needs. Fastest, and produces the three-different-ways
  outcome the scope names as the thing not to cut.
- **Templates binding on section set and order, free within sections** — required headings must
  be present in order; extra `##` sections are not permitted, extra `###` inside them are.
- **Templates binding down to `###`** — total uniformity, and no room for a brick that genuinely
  has three configuration modes.

On ownership: CONVENTIONS.md is *planning* (audience: whoever builds this repo, plus the
downstream skills); the M2 page is *product* (audience: a contributor who found the wiki).

# Recommendation

**Binding on section set and order, free within sections**, machine-checked:

- Each `type` in the closed vocabulary (`Brick`, `Contract`, …) has a required heading list in
  `data/vocab.yaml`; the validator asserts presence and order and rejects unknown `##` headings
  on typed pages. This is a validator rule, so per
  [test-first scope](/conventions/03-tdd-scope.md) it ships with a failing fixture.
- **A section with nothing true to say is not deleted** — it carries the placeholder block. A
  missing section and an unwritten one must not look the same; that distinction is criterion 1.
- `###` and below are free.
- Changing a template is a reviewed change ([decision](/conventions/06-review-and-merge.md)) and
  the PR that changes it updates every instantiated page in the same PR, or opens issues for
  them. A template that drifts from its instances is worse than none.

**On ownership: CONVENTIONS.md is the source; the M2 page is a rendering of it for
contributors.** The M2 page states the rules a contributor needs, in the wiki's own voice, and
links nothing back into `docs/planning/` (which is unpublished,
[decision](/conventions/01-planning-bundle-location.md)). Where they overlap, CONVENTIONS.md
wins and the M2 page is corrected — and a rule that exists *only* in the M2 page is a bug to fix
here. Neither document restates the validator: **anything mechanically enforced is documented as
"CI checks this", not re-specified in prose**, so there is one place a rule can rot.

# Verdict

**Binding on section set and order, free within sections**, accepted at triage. Required heading
lists live per `type` in `data/vocab.yaml`; the validator asserts presence, order and the absence
of unknown `##` headings on typed pages, shipping with fixtures. A section with nothing true to
say keeps its heading and carries the gap block rather than being deleted. Changing a template
updates every instance in the same PR or opens issues for them.

**CONVENTIONS.md is the source; the M2 page is its rendering for contributors** — where they
overlap, this document wins, and a rule existing only in the M2 page is a bug to fix here.
Neither restates the validator: anything mechanically enforced is documented as "CI checks this".
