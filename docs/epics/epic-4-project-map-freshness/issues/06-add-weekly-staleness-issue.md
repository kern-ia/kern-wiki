---
type: Issue
title: "Add the weekly staleness workflow and the one rolling issue"
description: "Render the stale report and upsert it into a single rolling stale-docs issue on a weekly schedule, rather than opening one issue per page or per run."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/48
epic: 4
issue: 06
slug: add-weekly-staleness-issue
size: M
status: open
gh_issue: 48
depends_on: [05]
---

# Add the weekly staleness workflow and the one rolling issue

## Summary

[Issue 05](./05-add-stale-version-comparison.md) works out what has rotted. This issue is how a
human finds out.

The shape is decided and is the point of the issue: **one rolling issue, edited in place**, not one
per page and not one per run. A weekly issue stream is a mute button waiting to happen, and the epic
names the single consolidated issue as an acceptance condition.

## Scope

- **Render the report** from [Issue 05](./05-add-stale-version-comparison.md) as an issue body,
  grouped so the three page states stay visually distinguishable:
  - **Possibly stale** — stamped, and the brick moved past the stamp. Each row names the page, the
    brick, the stamped version, and what it moved to (a release, or *N commits since*).
  - **Not documented yet** — placeholders, listed as such, never as stale.
  - **Errors** — unresolvable `resource` values, listed as failures needing a fix.
- **Upsert into one issue** labelled `stale-docs`: find the open one, edit its body; open it only if
  none exists. Reuse the upsert helper from
  [Issue 04](./04-add-weekly-external-link-check.md) if it landed first, or factor it so that issue
  can reuse it.
- Close the issue when everything is clean, and reopen-and-edit rather than open a second one when
  it is not.
- Body ends with a line stating **the job never wrote a stamp and never will** — the reader is
  looking at a list of pages a human must go and re-verify.
- `.github/workflows/stale.yml` — weekly schedule plus `workflow_dispatch`, `GITHUB_TOKEN` only,
  `issues: write` on that job and read elsewhere, pinned actions, no PAT.
- The label is created in this PR if it does not exist.

## Out of scope

- **No comparison logic** — [Issue 05](./05-add-stale-version-comparison.md) owns it; this issue
  renders and publishes its output.
- **No stamp coverage section** — [Issue 07](./07-add-stamp-coverage-in-weekly-issue.md) adds it to
  the same issue body, deliberately after this lands.
- **No page edits, no stamp writes, no `--fix`.** If the workflow can write to a content file at
  all, the design is wrong.
- **No per-page issues and no per-run issues.**
- **No issues opened on brick repositories.**
- **No notifications beyond the issue** — no email, no webhook, no third-party service.

## Acceptance criteria / Definition of done

- [ ] Rendering is unit-tested against golden files; grouping into the three states is
      fixture-covered.
- [ ] The GitHub client is faked at the boundary; no test opens a real issue.
- [ ] Running twice with the same report leaves exactly one open `stale-docs` issue, with the second
      run editing the first — asserted by a test, not by observation.
- [ ] Running with a clean report closes the issue; a later dirty run edits and reopens the same
      one.
- [ ] Placeholders never appear in the stale group, and errors never appear as staleness.
- [ ] The workflow declares `issues: write` on that job only, uses `GITHUB_TOKEN`, pins its actions,
      and runs on a weekly schedule plus `workflow_dispatch`.
- [ ] The issue body states that no automation writes a stamp.
- [ ] The workflow has been dispatched manually once and the resulting issue linked in the PR
      description.
- [ ] `gofmt -l` is silent, `golangci-lint` passes, `go test ./tools/...` passes.

## Relevant files / areas

No `tools/` binary or workflows exist in this repository yet — paths follow the decided layout and
are not verified locations: `tools/` (the `stale` subcommand from
[Issue 05](./05-add-stale-version-comparison.md)), `tools/testdata/`, `.github/workflows/stale.yml`.

## Dependencies

Blocked by [Issue 05](./05-add-stale-version-comparison.md). Shares the rolling-issue upsert with
[Issue 04](./04-add-weekly-external-link-check.md) — whichever lands first writes the helper. Blocks
[Issue 07](./07-add-stamp-coverage-in-weekly-issue.md).

## PR size note

Target ~500 changed lines; rendering, upsert, golden files and one workflow.
