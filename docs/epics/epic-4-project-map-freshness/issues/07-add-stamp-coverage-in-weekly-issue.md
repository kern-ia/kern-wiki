---
type: Issue
title: "Add stamp coverage to the weekly staleness issue"
description: "Report the second freshness axis in the same rolling issue — pages that moved since they were last verified, derived from git history rather than from the GitHub API."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/49
epic: 4
issue: 07
slug: add-stamp-coverage-in-weekly-issue
size: S
status: open
gh_issue: 49
depends_on: [06]
---

# Add stamp coverage to the weekly staleness issue

## Summary

Freshness has two axes, and they are not redundant
([decision](/conventions/12-stamping-and-done.md)):

| Axis | Question | Where it surfaces |
|---|---|---|
| Staleness | the brick moved — did the page? | weekly rolling issue |
| Stamp coverage | the page moved — did the verification? | sticky PR comment, **and the same weekly issue** |

Epic 1 issue 12 built the PR-comment half. This issue builds the other half of that sentence: the
weekly view, so a page edited eleven times since its last verification is visible to whoever reads
the weekly issue rather than only to whoever opened one PR months ago.

It is small because both halves already exist — the git-history derivation from epic 1 and the issue
upsert from [Issue 06](./06-add-weekly-staleness-issue.md).

## Scope

- Reuse epic 1's stamp-coverage derivation: git knows the commit that last set `verified` on a file,
  so `git diff <that-commit>..HEAD -- <path>` is exactly what entered the page since it was checked.
  Do not reimplement it.
- Add a **stamp coverage** section to the rolling `stale-docs` issue body, listing each stamped page
  that has changed since its stamp, with the number of commits and the diff size since.
- Keep it visually separate from the staleness section — the two axes answer different questions and
  a reader must not conflate "the brick moved" with "the page moved".
- `actions/checkout` with `fetch-depth: 0` on the staleness workflow, since it now reads history.
- Prose in the section stating the remedy: re-verify, or **lower `doc_state`** rather than leave a
  stamp that no longer covers the page.

## Out of scope

- **No new workflow** — this extends the one from
  [Issue 06](./06-add-weekly-staleness-issue.md).
- **No changes to the PR comment** — epic 1 issue 12 owns it, it is non-blocking, and it stays that
  way.
- **No blocking behaviour.** A page out of coverage does not fail CI. A typo fix must not cost a
  re-verification.
- **No stamp writes and no `doc_state` edits** by the job.
- **No re-verification of any page** in this PR — that is the work the section asks a human to do.

## Acceptance criteria / Definition of done

- [ ] Fixtures cover: a stamped page unchanged since its stamp (absent from the section), a stamped
      page changed since (present, with a commit count), and an unstamped page (absent, and not
      reported as an error).
- [ ] The derivation is epic 1's, reused — no second implementation of the git-history walk.
- [ ] The stamp coverage section is distinct from the staleness section in the issue body, and each
      states which question it answers.
- [ ] The workflow checks out with `fetch-depth: 0`, and its permissions are unchanged beyond what
      [Issue 06](./06-add-weekly-staleness-issue.md) already declared.
- [ ] Nothing in this PR writes a stamp or lowers a `doc_state`.
- [ ] The section names the remedy, including lowering `doc_state` as the honest option.
- [ ] `gofmt -l` is silent, `golangci-lint` passes, `go test ./tools/...` passes.

## Relevant files / areas

No `tools/` binary or workflows exist in this repository yet — paths follow the decided layout and
are not verified locations: `tools/` (the stamp-coverage derivation from epic 1 issue 12, the
`stale` subcommand from [Issue 05](./05-add-stale-version-comparison.md)), `tools/testdata/`,
`.github/workflows/stale.yml`.

## Dependencies

Blocked by [Issue 06](./06-add-weekly-staleness-issue.md) for the issue body and workflow, and by
[Epic 1](/epic-1-the-frame/EPIC_1.md) issue 12 for the derivation it reuses.

## PR size note

Target ~500 changed lines; well under it — one report section and a checkout depth change.
