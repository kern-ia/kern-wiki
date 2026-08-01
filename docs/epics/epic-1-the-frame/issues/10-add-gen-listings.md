---
type: Issue
title: "Add the gen subcommand with section listings and the bundle listing"
description: "Generate the section listings and the OKF bundle listing into committed markdown between markers, with regenerate-and-diff enforced in CI."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/15
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 10
slug: add-gen-listings
size: M
status: open
gh_issue: 15
depends_on: [05]
---

# Add the gen subcommand with section listings and the bundle listing

## Summary

Adding a brick must fill a slot, not edit navigation — which means the listings have to be derived.
This issue builds the generator and the CI enforcement around it, and lands the two simplest of the
five generated surfaces. The three registries follow in
[Issue 11](./11-add-generated-registries.md) on top of the same machinery.

## Scope

- `gen` implemented on Issue 05's skeleton: read the bundle, render a surface, write it back into
  committed markdown **between `<!-- BEGIN GENERATED -->` and `<!-- END GENERATED -->` markers**.
  Content outside the markers is never touched.
- **Section listings** — each `en/<section>/_index.md` lists its pages with title, description and
  `doc_state`.
- **The bundle listing** — the root `index.md`, replacing the hand-written listing from
  [Issue 01](./01-initialize-repo-and-okf-bundle-root.md).
- A `gen --check` mode: regenerate into memory and diff against what is committed, non-zero on any
  difference, printing the diff.
- A `gen --check` job in `.github/workflows/ci.yml`.
- Golden files for both surfaces under `tools/testdata/`, test-first.

## Out of scope

- **No freshness table, contracts index or exposed/needs matrix** —
  [Issue 11](./11-add-generated-registries.md).
- **No generation of contract pages or `log.md`** — a listing is derivable, a judgement is not.
  Both stay hand-written, permanently.
- **No French tree generation** — epic 5's generated stubs are a different surface with a different
  rule.
- No CI job that commits regenerated output; CI fails and the author reruns `gen`.

## Acceptance criteria / Definition of done

- [ ] `gen` writes only between the markers; text either side survives byte-identical.
- [ ] A page added to a section and not regenerated fails `gen --check` in CI, with a readable diff.
- [ ] The root `index.md` still carries `okf_version` and no other frontmatter after generation.
- [ ] Golden files cover both surfaces, including the empty-section case.
- [ ] Running `gen` twice produces no second change (idempotent).
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (gen packages), `tools/testdata/` (golden files),
`index.md`, `en/*/_index.md`, `.github/workflows/ci.yml`.

## Dependencies

Blocked by [Issue 05](./05-scaffold-tools-and-okf-conformance.md).
Blocks [Issue 11](./11-add-generated-registries.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
