---
type: Issue
title: "Scaffold the tools/ Go binary and the OKF conformance check"
description: "Create the single Go binary with its validate/gen/stale subcommand skeleton, the page-loading layer every check builds on, and the OKF conformance rules."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/10
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 05
slug: scaffold-tools-and-okf-conformance
size: M
status: open
gh_issue: 10
depends_on: [01, 03]
---

# Scaffold the tools/ Go binary and the OKF conformance check

## Summary

The wiki's truthfulness rules are enforced by CI rather than by discipline, and this is the binary
that does it. This issue builds the foundation — argument handling, bundle walking, frontmatter
parsing, `.okfignore` honouring, error reporting — and lands the first real rule set on top of it:
OKF conformance. Every later check issue adds a rule to this skeleton rather than a new program.

## Scope

- `tools/` as one Go module producing one binary with three subcommands, `validate`, `gen` and
  `stale`. `gen` and `stale` are stubs here; `stale` stays a stub until epic 4.
- The shared layer: walk the bundle, honour `.okfignore`, parse YAML frontmatter, and carry each
  page as a struct the rules read.
- **OKF conformance rules**, per the spec's three:
  - frontmatter is parseable and carries a non-empty `type` on every non-index document;
  - reserved filenames respected — `index.md` only at the bundle root, and never inside `en/`;
    the root `index.md` carries `okf_version` and no other frontmatter;
  - `log.md` headings are well-formed `## YYYY-MM-DD`, newest first.
- **Error reporting shape, decided once here and reused by every later rule**: a failure names the
  file, the rule, and what would satisfy it. Its audience is someone who just wrote a page.
- Test-first, strictly: every rule starts as a failing fixture under `tools/testdata/`, committed in
  the same PR, red before green.
- A `validate` job added to `.github/workflows/ci.yml`, plus `gofmt -l`, `golangci-lint` and
  `go test ./tools/...`.

## Out of scope

- **No frontmatter *value* validation** — closed vocabularies, stamps and truthfulness invariants
  are [Issue 06](./06-add-front-matter-validator.md).
- **No portability, link, heading, citation or terminology rules** — Issues 07–09.
- **No `gen` implementation** — [Issue 10](./10-add-gen-listings.md).
- **No `stale` implementation** — epic 4. Leave the subcommand registered and failing with "not
  implemented".
- No dependency beyond a YAML parser; the GitHub API client arrives with `stale`.

## Acceptance criteria / Definition of done

- [ ] `go test ./tools/...` passes, and every rule has at least one fixture it rejects and one it
      accepts.
- [ ] `gofmt -l` outputs nothing; `golangci-lint` passes with its default set, warnings fatal.
- [ ] `validate` run against the tree from Issue 01 exits 0.
- [ ] Each of the three OKF rules fails its fixture with a message naming file, rule and remedy.
- [ ] A file under a `.okfignore`d path is not validated.
- [ ] The `validate` job gates the PR; a tooling failure never gates the published site.
- [ ] Each rule's comment names the convention it enforces and links its section.

## Relevant files / areas

No existing code for this yet — the repository contains only `docs/`. Paths follow the decided
tree: `tools/` (Go module, `main.go` plus a package per concern), `tools/testdata/` (fixtures),
`.github/workflows/ci.yml` (extended).

## Dependencies

Blocked by [Issue 01](./01-initialize-repo-and-okf-bundle-root.md) and
[Issue 03](./03-add-pages-deploy-and-pr-build.md).
Blocks Issues [06](./06-add-front-matter-validator.md), [07](./07-add-portability-and-link-checks.md),
[10](./10-add-gen-listings.md) and [12](./12-add-stamp-coverage-pr-comment.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
