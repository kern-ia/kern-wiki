---
type: Issue
title: "Pick a next task from the status page and fix what it exposes"
description: "Discharge the epic's acceptance criterion by actually using the status section to choose a next task, then fixing whatever made that harder than it should have been."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/50
epic: 4
issue: 08
slug: verify-status-page-picks-next-task
size: S
status: open
gh_issue: 50
depends_on: [01, 02, 03]
---

# Pick a next task from the status page and fix what it exposes

## Summary

The epic has one stated acceptance criterion: **the transverse status page actually gets used to
pick a next task.** A criterion phrased as a use is discharged by using it, not by asserting it
holds.

This issue is deliberately separate and last, for the same reason epic 3 separates its adoption
check: it is the criterion most likely to be quietly assumed satisfied once the pages exist and look
plausible.

## Scope

- **Do it for real.** Open the status section cold, without opening any brick repository first, and
  pick what to work on next across the ecosystem using only what is on those pages.
- **Record the run in the PR description**: what you were trying to decide, what you looked at, in
  what order, where you had to leave the wiki to answer something, and what you picked.
- **Fix what the run exposed**, in this PR, bounded to the three status pages:
  - a column or field that turned out to be the one you needed and was not there;
  - an entry that was ambiguous about whether it was tracked, blocked, or merely old;
  - a link that should have existed between the status page, the roadmap and the open questions and
    did not;
  - ordering or grouping that made the page unusable at a glance.
- **Where a gap cannot be fixed by editing these pages, record it** — as a gap block if it is
  missing knowledge, or as an entry in the open questions register if it is a question. A finding
  that is neither fixed nor recorded did not happen.
- Update `verified` on any page you materially changed, or lower `doc_state` if you did not
  re-verify the whole page.

## Out of scope

- **No new page.** If the answer is "this needs a fourth status page", that is a finding to record,
  not a page to write here.
- **No new generated surface**, and no changes to `tools/`. A missing column is a content fix.
- **No brick documentation changes** — if the run exposes that a brick page is thin, that is an epic
  3 issue, opened separately, not fixed here.
- **No changes to any brick repository**, and no issues opened on them.
- **No rewriting of the pages wholesale.** The point is the delta the use exposed.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] The PR description records the run: the question, the path through the pages, and the task
      picked. A description that only lists the edits does not discharge the criterion.
- [ ] Every point at which you had to leave the wiki to answer something is named, and each is
      either fixed here or recorded as a gap block or an open question.
- [ ] Every edit traces to something the run exposed — no speculative improvements.
- [ ] Anything added to the pages is cited at a version, and nothing was inferred.
- [ ] Stamps are re-set only where the whole page still qualifies, and lowered rather than left
      stale where it does not.
- [ ] Findings belonging to another epic are named in the PR description as follow-ups rather than
      fixed here.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet — paths follow the decided content tree, not verified locations:
`en/status/status.md`, `en/status/roadmap.md`, `en/status/open-questions.md`,
`en/status/_index.md`, and `en/status/freshness.md` from epic 1.

## Dependencies

Blocked by [Issue 01](./01-add-transverse-status-page.md),
[Issue 02](./02-add-consolidated-roadmap-page.md) and
[Issue 03](./03-add-open-architectural-questions.md) — all three pages must exist before the section
can be used cold. Independent of the automation issues; the staleness job does not need to be
running for a human to pick a task.

## PR size note

Target ~500 changed lines; expected to be a small diff across three pages. Most of the cost is the
run, not the writing.
