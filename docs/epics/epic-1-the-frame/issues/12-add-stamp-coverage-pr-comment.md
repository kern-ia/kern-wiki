---
type: Issue
title: "Add the stamp coverage pull request comment"
description: "Compare each changed page against the commit that last set its verified stamp, and report what entered the page since, as a non-blocking sticky comment."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/17
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 12
slug: add-stamp-coverage-pr-comment
size: M
status: open
gh_issue: 17
depends_on: [06]
---

# Add the stamp coverage pull request comment

## Summary

Staleness asks *the brick moved — did the page?* and is epic 4's weekly job. This is the other axis:
*the page moved — did the verification?* Git knows the commit that last set `verified` on a file, so
`git diff <that-commit>..HEAD -- <path>` is exactly what entered the page since it was checked. The
comment surfaces that; the judgement stays human, which is why it never blocks.

## Scope

- A `validate` mode (or a sibling subcommand) that, for each content page changed in the PR, finds
  the commit that last modified its `verified` field and reports the diff that landed since.
- Output as a **sticky pull request comment, rewritten in place on each push** — a typo fix must not
  cost a re-verification, and must not accumulate comments either.
- **Non-blocking**: it never fails the job.
- The comment states the remedy plainly: re-verify, or **lower `doc_state`** rather than leave a
  stamp that no longer covers the page.
- A job in `.github/workflows/ci.yml` with `actions/checkout` at `fetch-depth: 0` and
  `pull-requests: write` — the first permission beyond read in this repository, scoped to this job
  alone, `GITHUB_TOKEN` only.
- Unit tests with the git history faked at the boundary; mock only true externals.

## Out of scope

- **No blocking behaviour**, and no failing exit code, under any condition including its own errors.
- **No stamp writing or lowering** — it reports, a human edits.
- **No weekly issue** — the same signal also appears in epic 4's weekly issue; this issue writes the
  PR half only.
- No PAT, no additional repository secret.

## Acceptance criteria / Definition of done

- [ ] A PR editing a stamped page shows a comment listing the diff since its stamp commit.
- [ ] A second push rewrites the same comment rather than adding one.
- [ ] A PR touching no stamped page produces no comment (or removes a stale one).
- [ ] The job succeeds even when the comment cannot be posted, and says so in its log.
- [ ] `pull-requests: write` appears on this job and no other.
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (a package reading git history),
`tools/testdata/`, `.github/workflows/ci.yml`.

## Dependencies

Blocked by [Issue 06](./06-add-front-matter-validator.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
