---
type: Decision
title: "Where the planning bundle lives"
description: "The repository root is already an OKF bundle root — so where does docs/planning/ sit, and is it published?"
tags: [decision, conventions]
timestamp: 2026-08-01T09:10:00Z
phase: conventions
decision: 1
slug: planning-bundle-location
status: decided
verdict: "`docs/` ships in the repo but is ignored by `.okfignore` and by Hugo; CONVENTIONS.md is a planning document, the M2 page its published rendering"
decided_via: triage
depends_on: []
---

# Question

The baseline says knowledge-style docs live as an OKF bundle under `docs/`, with a small top
level. This project inverts that: the repository root **is** the bundle root
([decision](/specs/23-okf-conformance.md)), and the top level is content trees (`en/`, `fr/`),
`tools/`, `layouts/`, `data/`, `templates/`.

That leaves this planning bundle — `docs/planning/`, already written — without a decided home.
It is itself an OKF bundle with its own `index.md` and `log.md`, which is precisely the pair the
root bundle reserves. Two bundle roots in one repository, one nested inside the other, is not
something OKF blesses; and `.okfignore` as drafted in SPECS does not list `docs/`, so the root
bundle's validator would currently walk into the planning bundle and judge its files.

# Options

- **Ship it, ignored** — `docs/` goes into `.okfignore` and into `hugo.toml`'s ignore list. The
  plan travels with the repo it describes, and neither validator nor Hugo sees it.
- **Ship it, published** — planning docs become a wiki section. Rejected on sight: the scope's
  non-goal *no re-hosting of repo internals* names dev logs and architecture notes, and a
  decision ledger is exactly that genre.
- **Keep it out of the wiki repo** — planning lives in a separate repo or locally. Honest about
  the two-bundles problem, but separates the rules from the repo that must obey them, and the
  downstream skills (`split-epics`, `create-issues`, `implement-issue`) expect
  `docs/planning/` beside the code they change.

# Recommendation

**Ship it, ignored**: `docs/` listed in `.okfignore` and excluded from Hugo's build.

The nesting objection is real but cheap to answer — an ignored directory is not part of the root
bundle, so there is exactly one published bundle and one private one that happens to share a
checkout. The alternative costs more: a planning bundle in another repo drifts from the
conventions it defines, and every downstream skill would need pointing at it.

Two consequences to record: `.okfignore` gains `docs/`, and CONVENTIONS.md is a **planning**
document, not the published contributor page. The M2 "how to write here" page
([scope](/scope/17-milestones.md)) is derived from it and written for contributors —
see [authoring rules ownership](/conventions/08-page-structure-and-templates.md).

# Verdict

**Ship it, ignored**, accepted at triage. `docs/` is added to `.okfignore` and to Hugo's ignore
list, so the repository has one published bundle and one private one sharing a checkout.
CONVENTIONS.md is a planning document; the M2 "how to write here" page is its published
rendering ([decision](/conventions/08-page-structure-and-templates.md)).
