---
type: Issue
title: "Add the generated registries: freshness table, contracts index, exposed/needs matrix"
description: "Generate the three cross-page registries from front matter, completing the five generated surfaces enforced by regenerate-and-diff."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/16
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 11
slug: add-generated-registries
size: M
status: open
gh_issue: 16
depends_on: [10]
---

# Add the generated registries: freshness table, contracts index, exposed/needs matrix

## Summary

The three surfaces that make the wiki legible across pages rather than page by page. All three are
derived from front matter — `verified`, `exposes`, `needs`, `maturity`, `doc_state` — so they cannot
disagree with the pages they summarize, and nobody maintains them by hand.

## Scope

- **Freshness table** — page → brick → version verified → date. **Placeholders are included**, and
  listed as *not documented yet* rather than as stale or as blank.
- **Contracts registry index** — every contract page with its enforcement status, producer and
  consumer.
- **Exposed/needs matrix** — bricks against contracts, from the `exposes` and `needs` fields, making
  an unconsumed contract or an unmet need visible.
- All three written between the generated markers into the pages that host them, and all three
  covered by `gen --check` in CI.
- Golden files, test-first, including: a brick with no stamp, a contract with no consumer, and a
  need with no producer — the cases that are the point of the matrix.

## Out of scope

- **No staleness derivation.** "Possibly stale" is derived weekly against the brick's latest
  release, and that job is epic 4. This issue reports what the pages claim, never a judgement about
  whether it has rotted.
- **No stamp writing, ever** — a stamp means a human read the code.
- **No pages** — the freshness table's host page is
  [Issue 24](./24-add-freshness-table-page.md); the contracts registry's host is the contracts
  section page. If a host page does not exist yet, generate into the section page and note it.
- No GitHub API calls; this reads front matter only.

## Acceptance criteria / Definition of done

- [ ] Each of the three surfaces regenerates deterministically and idempotently.
- [ ] A placeholder page appears in the freshness table as *not documented yet*, with no version and
      no date.
- [ ] A contract declared in `needs` with no page, and a contract page nothing `exposes`, both
      appear in the matrix as visible gaps rather than being silently dropped.
- [ ] `gen --check` fails when any of the three is stale in the working tree.
- [ ] Golden files cover the three degenerate cases named in Scope.
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (gen packages extending Issue 10),
`tools/testdata/`, `en/status/`, `en/contracts/_index.md`, `en/ecosystem/`.

## Dependencies

Blocked by [Issue 10](./10-add-gen-listings.md).
Blocks [Issue 24](./24-add-freshness-table-page.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
