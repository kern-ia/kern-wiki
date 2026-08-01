---
type: Decision
title: "Home of the cross-brick contracts"
description: "What is the wiki's role on the kern.* contracts, as they accumulate with each new package?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 09
slug: contract-registry-home
status: decided
verdict: "A growing contracts registry: document every contract as it arrives, per package what it exposes and needs; authority stays with the CI-enforced fixtures"
decided_via: discussion
depends_on: [source-of-truth, coverage-depth]
---

# Question

The bricks don't call each other's code — they exchange messages over contracts. Two classes
exist today, in very different states.

**Class A — enforced (orch → ui).** `kern.step-event/v1` and `/v2`, `kern.activity/v1`,
`kern.registry/v1`. JSON fixtures exist **twice**, in `Kern-Orch/contracts/` and
`Kern-UI/contracts/`, and the duplication is the safety mechanism: *"drift is caught by tests,
not by discipline […] each side asserts against them on every CI run."*

**Class B — provisional (orch → agent CLI).** One `{"node_id","prompt","state"}` request on
stdin, JSON-lines `token` / `result` / `error` on stdout, 4 MB line cap. **No JSON fixture, no
CI assertion, no owning repo** — prose in two READMEs, both marking it "awaiting reconciliation
with the real CLI", with five extensions already planned (`model`/`provider`, a
structured-output convention, `result.usage`, an explicit error-mapping rule, optional
`thinking`).

# Options

- **Document, don't own** — the wiki explains each contract; the CI-enforced JSON stays the
  reference for class A, and class B is documented with a provisional banner.
- **Wiki as canonical home** — the specs move to the wiki, repos link out. Trades a red build
  for a page nobody validates.
- **Extract a `kern-contracts` repo** — schemas in a shared repo both bricks depend on. A code
  decision, not a doc decision.
- **Stay silent on class B** until it's frozen.

# Verdict

**The user reframed the question: there is no one-shot choice to make, because the contracts
will keep accumulating.** A fifth package is already in progress and more are expected, each
arriving with its own surface. So the deliverable is not "a contracts page" but **a registry
and a habit**: document each contract as it appears, and for every package record what it
**exposes** and what it **needs**.

That pattern already exists in the codebase and becomes the wiki's template —
`Kern-UI/README.md` states it outright:

> Every `kern-*` brick publishes what it accepts and states what it needs. Nothing else is
> part of the contract: internal schemas, database files and package layouts may change
> without notice.

Adopted as the structure:

- **A contracts registry** — one entry per contract: purpose, producer, consumer, version(s),
  enforcement status (CI-asserted vs provisional), field semantics, migration notes.
  Designed so a new contract is a new entry, not a restructuring
  ([decision](/scope/12-mvp-cut.md)).
- **An exposed / needs block on every brick page** — what this package offers other bricks,
  and what it requires from them. This is the part that makes the registry usable rather than
  encyclopaedic, and it is what a new contributor reads first.
- **Class B is documented, with a provisional banner** — current shape, plus the gotchas anyone
  implementing it will hit (error-philosophy inversion, the 4 MB cap, `result.output` key
  collisions across nodes, no `model` field) and the five pending extensions listed as **open
  questions, not spec**.

**On authority — not contested, so the recommendation stands and is recorded explicitly:** the
wiki explains, the repos own. For class A, if the wiki and a CI-asserted fixture disagree, the
fixture wins. For class B nothing can win, which is itself worth documenting: the wiki noting
that class B lacks the guarantee class A has is useful output from this project, and the honest
fix (a fixture + assertions on both sides) is recorded as an M4 open question rather than
quietly absorbed by documentation.

The `kern-contracts` extraction stays an M4 open question, deferred to `define-specs` or a
brick epic.
