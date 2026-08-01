---
type: Issue
title: "Add the translation drift lint"
description: "Flag a French page whose English original changed after the translation was last touched, using git dates, so an out-of-date translation is a check rather than a hope."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/54
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 04
slug: add-translation-drift-lint
size: S
status: open
gh_issue: 54
depends_on: [03]
---

# Add the translation drift lint

## Summary

The structural rules in [issue 03](./03-add-french-tree-validator-rules.md) catch a translation that
never matched its original. This one catches the translation that *stopped* matching — the English
page was corrected, the French page was not, and the wiki now says two different things about the
same subject in two languages. That is precisely the contradiction the epic forbids, and it arrives
by nobody doing anything wrong.

SPECS makes it a lint rather than a hope ([decision](/specs/09-bilingual-mechanism.md)). Git already
knows both dates; the only work is asking it.

## Scope

- **Compare last-modified commits**: for each `fr/` page, the commit that last touched it against
  the commit that last touched its `en/` original. The original being newer is the finding.
- The finding **names the diff to read** — the original's changes since the translation's commit —
  because that is the work, and a lint that says only "out of date" makes the translator re-read a
  whole page to find two changed sentences.
- **Non-blocking on the pull request path.** An English correction must not be blocked by its own
  translation being momentarily behind; the rule that matters — *the original changes first* — is
  satisfied by exactly that sequence ([decision](/conventions/13-translation-authoring.md)).
  Surface it the way stamp coverage is surfaced, as a comment rewritten in place.
- **Requires `fetch-depth: 0`** on the job that runs it, following the same operational shape as the
  stamp coverage check ([conventions](/conventions/12-stamping-and-done.md)). `GITHUB_TOKEN` only,
  `pull-requests: write` on that job alone, no PAT.
- Reuse the git-history reading from epic 1's stamp coverage check rather than adding a second way to
  ask git the same question.

## Out of scope

- **No auto-translation and no auto-editing.** Nothing here writes to a page, in either tree.
- **No blocking failure.** If this rule ever gates a merge, an English fix becomes hostage to a
  French one and people will stop fixing English pages.
- **No content-level comparison.** Whether the two pages *say* the same thing is
  [issue 09](./09-verify-bilingual-criterion.md) and human judgement; this rule compares dates.
- **No weekly job.** The two cron workflows are decided and this is not a third
  ([specs](/specs/21-background-work.md)); drift belongs where the change is being made.

## Acceptance criteria / Definition of done

- [ ] The rule starts as a failing fixture, committed in the same PR, red before green, with the git
      history it needs constructed by the test rather than assumed from the repository.
- [ ] A `fr/` page older than its original is reported, with the diff range to read.
- [ ] A `fr/` page newer than its original is silent — translating after a change is the correct
      sequence, not a finding.
- [ ] A page with no French counterpart produces no drift finding — absence is a gap, and gaps are
      acceptable.
- [ ] The check is non-blocking and its output is rewritten in place on each push rather than
      appended.
- [ ] The job declares `fetch-depth: 0`, uses `GITHUB_TOKEN` only, and takes `pull-requests: write`
      on no other job.
- [ ] `gofmt -l` is silent, `golangci-lint` passes with warnings fatal, `go test ./tools/...` passes.

## Relevant files / areas

No `tools/` binary exists in this repository yet — paths follow the decided layout
([specs](/specs/13-tooling-language.md)) and epic 1's output, and are not verified locations:
`tools/`, `tools/testdata/`, `.github/workflows/` (the pull request workflow, and the stamp coverage
job from epic 1 issue 12).

## Dependencies

Blocked by [Issue 03](./03-add-french-tree-validator-rules.md) — same rule set, same fixtures
directory, and the mirror-path resolution this reuses. Blocked by
[Epic 1](/epic-1-the-frame/EPIC_1.md) for the stamp coverage job whose git-history reading and
permissions shape this follows.

## PR size note

Target ~500 changed lines; this one should be well under it — one rule, its fixtures, and a job
setting. If it is growing, the growth is a second git-history implementation that should be a reuse
instead.
