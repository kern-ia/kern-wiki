---
type: Issue
title: "Add the stale subcommand: release comparison with commit-count fallback"
description: "Resolve each page's resource to a repository and compare its verified.version against the latest release, falling back to commits since the stamped ref, producing a structured report."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/47
epic: 4
issue: 05
slug: add-stale-version-comparison
size: M
status: open
gh_issue: 47
depends_on: []
---

# Add the stale subcommand: release comparison with commit-count fallback

## Summary

The wiki's worst risk is a page that is confidently wrong rather than merely dead-linked. Stamps and
the freshness table exist by hand from epic 1; this is the code that reads them and works out what
has rotted.

This issue is the computation only — resolve, compare, report. Publishing the result as a GitHub
issue is [Issue 06](./06-add-weekly-staleness-issue.md). Splitting there keeps the comparison
logic testable without a workflow in the loop, and it is the half where being wrong is expensive.

## Scope

- **The `stale` subcommand**, the third of the binary's three
  ([decision](/specs/13-tooling-language.md)), producing a structured report on stdout.
- **Resolve each page's OKF `resource` to a repository.** An unresolvable `resource` on a stamped
  page is an **error, not a skip** — silent skipping is how a stamp stops meaning anything.
- **Compare `verified.version` against the brick's latest release.** Where the repository has cut no
  release, **fall back to the commit count since the stamped ref**: "37 commits since you last
  checked" is a signal a human can weigh.
- **Placeholders are reported separately as *not documented yet*, never as stale** — a
  `doc_state: placeholder` page carries no stamp to compare, and the epic requires the three page
  states stay distinguishable.
- **Metadata only** — the GitHub API's releases and compare endpoints. No checkouts, no builds of
  other repositories.
- A GitHub API client, faked at the boundary in tests. This and a YAML parser are the only
  dependencies SPECS budgets for.
- **The job never writes a stamp.** Not `verified.version`, not `verified.date`, not on any page.
  Make it structurally impossible rather than merely absent: this subcommand opens no file for
  writing.

## Out of scope

- **No GitHub issue creation, no workflow, no scheduling** — [Issue 06](./06-add-weekly-staleness-issue.md).
- **No stamp-coverage-against-git-history computation** — [Issue 07](./07-add-stamp-coverage-in-weekly-issue.md).
- **No edits to any page**, under any flag. There is no `--fix`.
- **No executed documentation.** Running the quickstart against real bricks is the thing that
  catches *wrong* rather than *old*, and scope defers it explicitly.
- **No content changes** in this PR.

## Acceptance criteria / Definition of done

- [ ] Every rule starts as a failing fixture under `tools/testdata/`, committed in the same PR, red
      before green.
- [ ] The GitHub client is faked at the boundary; no test makes a real network request. Only true
      externals are mocked.
- [ ] A page whose `resource` cannot be resolved to a repository is reported as an error and exits
      non-zero — covered by a fixture asserting it is not skipped.
- [ ] A brick with releases is compared against the latest release; a brick with none falls back to
      a commit count since the stamped ref. Both paths have fixtures.
- [ ] `doc_state: placeholder` pages appear in a separate *not documented yet* group and never in
      the stale group — fixture-covered in both directions.
- [ ] No code path in the subcommand opens a content file for writing; a test asserts the content
      tree is byte-identical after a run.
- [ ] Rate limiting and API errors are propagated with context naming the page and the repository,
      never swallowed.
- [ ] Any new dependency carries a one-line justification in the PR description.
- [ ] `gofmt -l` is silent, `golangci-lint` passes with warnings fatal, `go test ./tools/...`
      passes.

## Relevant files / areas

No `tools/` binary exists in this repository yet — paths follow the decided layout and epic 1's
output, and are not verified locations: `tools/` (front matter parsing from epic 1 issue 06 is
reused, not reimplemented), `tools/testdata/`.

Reads the front matter fields decided in [specs](/specs/05-page-metadata.md): `resource`,
`verified.version`, `verified.date`, `doc_state`.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) — the `tools/` binary, its front matter parsing,
and the stamps this reads. Blocks [Issue 06](./06-add-weekly-staleness-issue.md).

## PR size note

Target ~500 changed lines; Go plus fixtures. If the GitHub client and the comparison logic together
approach ~1000, land the client and its fake first as its own PR.
