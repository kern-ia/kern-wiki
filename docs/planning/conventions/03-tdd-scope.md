---
type: Decision
title: "Where test-first applies"
description: "Strict red-green is baseline-mandatory for assertable behavior — in a wiki repo, that is the tooling and nothing else."
tags: [decision, conventions]
timestamp: 2026-08-01T09:14:00Z
phase: conventions
decision: 3
slug: tdd-scope
status: decided
verdict: "strict red-green for `tools/`, every validator rule shipping with a failing fixture; content carries no unit tests — the CI check suite is its test suite"
decided_via: triage
depends_on: []
---

# Question

The baseline mandates strict red-green test-first wherever correctness is an assertable
behavior, and carves out only *visual fidelity to a design*. Neither half describes most of this
repository: a brick page's correctness is **whether it matches the code it describes**, which no
unit test can assert.

The baseline's carve-out language doesn't transfer either — a wiki page is not a UI port. The
dividing line needs restating for a documentation repo.

# Options

- **Test-first for `tools/`, CI checks as the content's tests** — the validator, generator and
  staleness job get strict red-green; content is answerable to the six CI checks
  ([decision](/specs/12-ci-checks.md)) and to review.
- **Test-first for `tools/` only, no rule for content** — same, minus the statement that the CI
  checks play the role tests play elsewhere. Leaves the impression content is unchecked.
- **Relax test-first for tooling too** — it is "just scripts". Directly contradicts SPECS, which
  requires the validator be unit-tested because *an untested validator converts an absent
  guarantee into a false one*.

# Recommendation

**Test-first for `tools/`, strictly; the CI check suite is the content's test suite.** Concretely:

- Every rule the validator enforces starts as a **failing fixture** — a small markdown file
  under `tools/testdata/` that the rule must reject — committed in the same PR, red before
  green. A rule with no fixture is not merged.
- The generator's five surfaces ([decision](/specs/06-registries-and-tables.md)) are tested by
  golden files; the staleness job's version comparison is unit-tested with the GitHub client
  faked at the boundary, per the baseline's *mock only true externals*.
- **Content carries no unit tests.** Its equivalents are the CI checks and the review checklist
  ([decision](/conventions/06-review-and-merge.md)). Adding a rule to the wiki is therefore a
  `tools/` change with a fixture, not a paragraph in a style guide — the project's stated
  principle, *drift is caught by tests, not by discipline*, applied to itself.

The consequence worth naming: **a convention nobody can write a fixture for is a review-checklist
item, and is understood to be weaker than one that has one.** That is the honest line between the
two, and it belongs in the M2 page as well.

# Verdict

**Test-first for `tools/`, strictly; the CI check suite is the content's test suite**, accepted
at triage. Every validator rule starts as a failing fixture under `tools/testdata/`, committed in
the same PR — a rule with no fixture is not merged. Golden files for the generator, a faked
GitHub client for the staleness job. Content carries no unit tests.

Recorded as the consequence: **a convention nobody can write a fixture for is a review-checklist
item, and is weaker than one that has one** — a line that belongs in the M2 page too.
