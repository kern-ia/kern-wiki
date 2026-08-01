---
type: Issue
title: "Add the verification guide: stamping, citations and the self-review checklist"
description: "Publish what a version stamp asserts, how citations are written, and the five-question self-checklist that stands in for the human review gate this repository does not have."
tags: [epic-2]
resource: https://github.com/kern-ia/kern-wiki/issues/31
timestamp: 2026-08-01T12:30:00Z
epic: 2
issue: 02
slug: add-verification-and-review-checklist
size: M
status: open
gh_issue: 31
depends_on: [01]
---

# Add the verification guide: stamping, citations and the self-review checklist

## Summary

The epic's deliverable that turns the no-invented-content rule into a **review checklist**. It
carries more weight here than in most repositories: green CI is the only merge gate, no approval is
required anywhere, so criterion 1 has no human gate other than the one the author runs on
themselves. This page is that gate, written down.

It also documents the two things a contributor gets wrong first — stamping a page they only partly
re-read, and citing a repository home instead of the files they read.

## Scope

- `en/contributing/verifying.md`:
  - **What setting `verified: {version, date}` asserts**, of the whole page: every claim checked
    against that version by reading the sources in `# Citations`; anything uncheckable carrying a
    gap block rather than a hedge; no section skipped.
  - **There is no partial stamp.** A typo fix does not touch `verified` and does not need to.
  - **`doc_state: documented` requires a stamp and no gap blocks**; `partial` is the honest state
    for most pages for most of this project's life and is not a defect.
  - **Runnable content is stamped only after being run** — the quickstart, install commands,
    configuration examples.
  - **No automation ever writes a stamp**, the staleness job included.
  - **How to re-verify efficiently**: `git diff <commit that last set verified>..HEAD -- <path>`
    narrows the work, not the scope — a two-line diff can invalidate everything around it.
  - **If you don't re-verify, lower `doc_state`** rather than leave a stamp that no longer covers
    the page — with the stamp-coverage PR comment named as non-blocking and rewritten in place, so
    nobody re-verifies a page to silence a bot.
  - **Citations**: a citation is a path at a version, grouped by brick and version, paths not
    repository homes, what was actually *read* rather than what supports the claim in retrospect,
    non-repository sources dated. Include the worked example from CONVENTIONS.
  - *CI checks this* for the citation shape and for citation versions against `verified.version`.
  - **The self-checklist**, as the five questions from
    [CONVENTIONS.md](../../../planning/CONVENTIONS.md) §Review & merge, in a form a contributor can
    run against their own PR — plus the plain statement of the trade: a page asserting something
    untrue merges the moment the build is green, so if a false claim reaches the site and no check
    could have caught it, **the answer is a new check**.
- A pointer to this page from `en/contributing/_index.md` and from
  [Issue 01](./01-add-contributing-and-how-to-write.md)'s page.

## Out of scope

- **No changes to the checks themselves** — the stamp-coverage comment, the citation check and the
  staleness job are epic 1 and [Epic 4](/epic-4-project-map-freshness/EPIC_4.md) work. This page
  describes what already exists.
- **No stamping of existing pages**, and no re-verification pass over epic 1's content.
- **No new rules** — same constraint as Issue 01: CONVENTIONS is the source.
- No `CONTRIBUTING.md` anywhere, in this repository or in `kern-ia/.github`.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] A contributor can decide, from this page alone, whether their PR may touch `verified` and what
      `doc_state` to set.
- [ ] The citation example on the page is real — it cites files that exist at the versions named, or
      it is labelled as the illustrative example carried over from CONVENTIONS.
- [ ] The checklist's five questions are answerable without reading CONVENTIONS.
- [ ] The page states the non-blocking nature of the stamp-coverage comment explicitly.
- [ ] Nothing on the page restates a validator rule as advice; enforced rules are marked
      *CI checks this*.
- [ ] `hugo` builds with warnings fatal; `validate` passes; 100-column wrap.

## Relevant files / areas

No existing content for this yet — path follows the decided tree, not verified against this
repository: `en/contributing/verifying.md`, linked from `en/contributing/_index.md`.

Source: [CONVENTIONS.md](../../../planning/CONVENTIONS.md) §Citations discipline, §Stamping and when
a page is done, §Review & merge.

## Dependencies

Blocked by [Issue 01](./01-add-contributing-and-how-to-write.md) — the section and the page it links
from. Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s citation check and stamp-coverage comment
(Issues 09 and 12): describing a check that does not exist yet would be its own invented content.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
