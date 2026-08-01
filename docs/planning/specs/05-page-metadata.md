---
type: Decision
title: "Page metadata schema"
description: "What structured metadata does every page carry, and what is it the source of truth for?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 05
slug: page-metadata
status: decided
verdict: "OKF core fields plus typed project extensions, as the single source of truth; staleness derived, never authored"
decided_via: triage
depends_on: [markdown-contract, content-tree, okf-conformance]
---

# Question

This project has no database; **the front matter is the data model** — and per the checklist, the
data model is the most expensive thing to change later. OKF fixes its base shape
([decision](/specs/23-okf-conformance.md)); what remains is the project profile on top of it,
which must carry four scope verdicts:

- three page states must stay distinguishable everywhere — *not documented yet* / *verified
  against version X* / *possibly stale* ([decision](/scope/16-freshness-and-versioning.md));
- every technical page carries a version stamp, written into the template from day one, because
  retrofitting stamps never happens (same decision, success criterion 8);
- maturity markers *works today* / *provisional* / *planned*
  ([decision](/scope/20-documenting-the-gap.md));
- each brick declares **exposed / needs** contracts ([decision](/scope/09-contract-registry-home.md)).

# Options

- **OKF core fields only** — `type`, `title`, `description`, `tags`, `timestamp`, `resource`.
  Conformant, and none of the four verdicts above is expressible, so stamps and maturity fall back
  to prose nothing can check.
- **OKF core + typed project extensions** — the stamp, maturity and contract wiring as additional
  frontmatter keys, which OKF explicitly permits ("producers MAY include any additional keys").
  Machine-checkable, and the M4 automation ([decision](/specs/14-freshness-automation.md)) becomes
  a metadata read rather than a text scrape.
- **Extensions plus a restated prose block** — prettiest on both surfaces, and two copies that
  drift. Rejected: a wrong version stamp is worse than an ugly one, and drift between two copies
  of the same fact is the failure mode this whole project is organised against.

# Recommendation

**OKF core plus typed project extensions, as the single source of truth**, validated in CI
([decision](/specs/12-ci-checks.md)).

Every page carries the OKF core:

```yaml
type: Brick               # Brick | Contract | Guide | Quickstart | Glossary | Reference | Section
title: "kern-orch"
description: "Graph-based agent orchestration with checkpoints."
tags: [orchestration, graph]
timestamp: 2026-07-31T09:00:00Z   # last meaningful change to this page
```

Pages bound to a real asset add OKF's `resource` — for a brick, its repository; for a contract,
the fixture in the repo that owns it:

```yaml
resource: https://github.com/yoann/kern-orch
```

Technical pages (`Brick`, `Contract`, and any page asserting something about code) add the
project extensions:

```yaml
doc_state: partial        # placeholder | partial | documented
maturity: works-today     # works-today | provisional | planned
verified:
  version: v0.2.0         # tag or commit — whatever was actually read
  date: 2026-07-31
```

Brick pages add the contract wiring, which is what makes the registry generable:

```yaml
brick: kern-orch
exposes: [kern.run.v1]
needs: [kern.agent-cli.v0]
```

Five rules that make the schema hold:

- **`resource` is the staleness job's input.** One repository URL per page, used by humans as a
  link and by [the M4 job](/specs/14-freshness-automation.md) as the thing to compare against —
  rather than a second, project-invented `repo:` key saying the same thing.
- **`doc_state: placeholder` forbids `verified`**, and a page with no `verified` block may not be
  marked `documented`. That is criterion 1 — no false information — expressed as a lint rule.
- **The third state is derived, never authored.** Nobody writes `stale`; the M4 job computes it by
  comparing `verified.version` against the brick's latest release. Authors record what they
  checked, machines decide what has rotted.
- **`maturity` describes the code, `doc_state` describes the page, `timestamp` describes the
  file.** Three different questions that a single "last updated" field would blur — and blurring
  "unwritten" with "doesn't exist yet" is precisely what makes readers distrust every page
  equally.
- **The project profile is stricter than OKF, deliberately.** OKF requires consumers to tolerate
  unknown keys and missing optional fields; our validator is a producer-side lint and rejects
  unknown keys, missing `description`, or an unstamped brick page. The bundle stays readable by
  any OKF consumer; contributors are held to more ([decision](/specs/23-okf-conformance.md)).

Vocabularies (`type`, `maturity`, `doc_state`, contract ids) are closed sets defined once in
`data/vocab.yaml` and enforced by the validator — so "which markers exist" has one answer for
contributors, the theme and CI alike.

# Verdict

**OKF core plus typed project extensions as the single source of truth**, accepted at triage.

`resource` carries the brick's repository and feeds the staleness job; `verified` records what a
human actually read; `maturity` describes the code and `doc_state` the page. A placeholder may not
carry a stamp, and no page may claim `documented` without one. Vocabularies are closed sets in
`data/vocab.yaml`, and the validator is deliberately stricter than OKF requires of consumers.
