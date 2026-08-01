---
type: Decision
title: "Formatters & linters"
description: "Baseline says a formatter is law — but the main artifact here is prose, and SPECS excluded prose linters."
tags: [decision, conventions]
timestamp: 2026-08-01T09:12:00Z
phase: conventions
decision: 2
slug: formatters-and-linters
status: decided
verdict: "gofmt + golangci-lint fatal over `tools/`; no prose formatter or linter; markdown hard-wrapped at 100 columns, held by review"
decided_via: triage
depends_on: []
---

# Question

The baseline's rule — *a formatter is law: run it in CI, never debate style in review* — assumes
a repository of code. Here roughly 95% of the diff will be markdown prose, for which SPECS
deliberately excluded both markdownlint and Vale: *"the risk here is asserting something untrue,
not comma placement"* ([decision](/specs/12-ci-checks.md)).

So the baseline rule applies in full to `tools/` and not at all to content — but "not at all"
would leave nothing catching a 400-character line or a table that renders differently on GitHub
than in the site.

# Options

- **Go formatted and linted, markdown unformatted** — `gofmt`/`goimports` and `go vet` +
  `golangci-lint` gate `tools/`; markdown answers only to the validator and to review.
- **Add markdownlint after all** — reopens a settled specs decision to catch trivia.
- **Add a formatter but not a linter for markdown** (e.g. `prettier --parser markdown`) — would
  normalize tables and wrapping mechanically. Costs a Node toolchain in a repo whose stack
  decision was *no Node, no Python, no Ruby*.

# Recommendation

**Go formatted and linted; markdown deliberately unformatted**, with two mechanical rules that
cost no new tool:

- `gofmt` (via `gofmt -l` in CI, failing on any output) and `golangci-lint` with its default
  set, warnings fatal, over `tools/`.
- Markdown: **hard-wrap at 100 columns**, one sentence per line not required. This is the only
  whitespace rule, it is what the planning bundle already does, and it makes prose diffs
  reviewable line by line — which matters more here than anywhere, because review is the only
  check on truthfulness.
- Tables and fenced blocks are exempt from the wrap.

Enforcement of the wrap is by review, not by CI — adding a line-length check is a two-line
addition to the existing Go validator if review turns out not to hold it.

# Verdict

**Go formatted and linted, markdown deliberately unformatted**, accepted at triage. `gofmt -l`
failing on any output and `golangci-lint` with its default set, warnings fatal, over `tools/`.
No prose formatter and no prose linter — SPECS' exclusion of Vale and markdownlint stands.
Markdown hard-wraps at 100 columns (tables and fenced blocks exempt), held by review, promotable
to a validator rule if review doesn't hold it.
