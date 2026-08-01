---
type: Issue
title: "Add the front matter validator"
description: "Enforce the closed vocabularies and the four truthfulness invariants — no stamp on a placeholder, no documented page without one, resource present, alias on rename."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/11
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 06
slug: add-front-matter-validator
size: M
status: open
gh_issue: 11
depends_on: [04, 05]
---

# Add the front matter validator

## Summary

Front matter is the schema — there is no database — so this is where acceptance criterion 1 (*no
false information*) becomes a lint rule rather than an intention. The validator reads
`data/vocab.yaml` from [Issue 04](./04-add-page-templates-and-vocabulary.md), so the rules and the
templates cannot drift apart.

## Scope

Rules added to `validate`:

- **Closed vocabularies** — `type`, `maturity` and `doc_state` must each hold a value listed in
  `data/vocab.yaml`. An unknown value is an error naming the allowed set.
- **`doc_state: placeholder` ⇏ `verified`** — a placeholder carries no stamp, in both directions:
  a stamped placeholder is an error.
- **`doc_state: documented` requires a stamp** — nothing claims documented without
  `verified: {version, date}`.
- **Every technical page is stamped** — the page types `vocab.yaml` marks as technical must carry
  `verified`, or a `doc_state` that admits its absence.
- **`resource` present where required** — one repository reference per page that documents a repo;
  it is both the reader's link and the staleness job's comparison target.
- **Alias on rename** — a content file whose path changed relative to the merge base and that
  carries no matching Hugo `aliases` entry is an error.
- **`timestamp` present and parseable** as ISO 8601 on every non-index document.
- Fixtures first, one per rule, red before green.

## Out of scope

- **No heading, banner or gap-block rules** — [Issue 08](./08-add-page-structure-checks.md); those
  read the page body, these read only the frontmatter.
- **No citation-version cross-check** — [Issue 09](./09-add-citation-and-terminology-checks.md).
- **No stamp *coverage* against git history** — [Issue 12](./12-add-stamp-coverage-pr-comment.md).
  This issue checks the stamp's shape and its compatibility with `doc_state`, not whether the
  verification still covers the page.
- No new vocabulary values; if a rule needs one, it goes in `vocab.yaml`, not in Go.

## Acceptance criteria / Definition of done

- [ ] Every rule above has a rejecting fixture under `tools/testdata/` and an accepting one, both
      committed in this PR.
- [ ] The vocabularies are read from `data/vocab.yaml` at runtime, not duplicated in Go.
- [ ] Each failure names the file, the rule, and what would satisfy it.
- [ ] The rename check works from a shallow-free checkout (`fetch-depth: 0` where history is read).
- [ ] `validate` against the pages existing at merge time exits 0.
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (a rules package extending Issue 05's skeleton),
`tools/testdata/`, reading `data/vocab.yaml`.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md) and
[Issue 05](./05-scaffold-tools-and-okf-conformance.md).
Blocks [Issue 08](./08-add-page-structure-checks.md) and
[Issue 09](./09-add-citation-and-terminology-checks.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
