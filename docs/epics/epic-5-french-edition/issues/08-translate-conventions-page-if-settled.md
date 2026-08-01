---
type: Issue
title: "Translate the conventions page, if it has settled"
description: "Translate en/contributing/how-to-write.md only if the page has stopped moving — otherwise close this issue as deferred with the evidence, since the epic ships without it by design."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/58
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 08
slug: translate-conventions-page-if-settled
size: M
status: open
gh_issue: 58
depends_on: [01, 03, 06]
---

# Translate the conventions page, if it has settled

## Summary

The epic translates the conventions page **only if it has settled**. That condition is in the scope,
not an implementer's caution: translating a page that is still churning doubles the churn, and the
conventions page is the one front-door page epic 2 keeps editing as contributors hit its gaps.

So this issue has two legitimate outcomes, and closing it undone is one of them. What it must not
produce is a French conventions page that quietly falls behind the English one — which is the
outcome that looks like success on the day it merges.

## Scope

- **Decide, with evidence, whether the page has settled.** The test is git, not opinion: no
  substantive change to `en/contributing/how-to-write.md` for a sustained stretch before this issue
  is picked up — a `fix:` or `content:` commit within that window means it has not settled, a typo or
  formatting commit does not. Record the commits inspected in the pull request or in the closing
  comment.
- **If it has settled**: `fr/contributing/how-to-write.md` and `fr/contributing/_index.md` at their
  mirror paths, transposed — same headings, same order, no French-only rules and no dropped ones.
- Rule text is translated; **the artefacts a rule names are not** — front matter field names,
  `doc_state` and `maturity` values, commit type prefixes, branch naming, the gap block's and the
  provisional banner's leading text are quoted verbatim, because CI matches on them and a translated
  banner is a banner that fails its own check.
- The French page states, as its original does, that the planning bundle's conventions document is
  the source and this page is its rendering — with the pointer unchanged.
- No `verified` stamp; the original's is inherited.
- **If it has not settled**: close this issue as deferred, with the evidence, and leave the page
  English. The French tree serves the stub, which is the honest state and needs no work.

## Out of scope

- **No partial translation** to "get started" — a page is translated whole or absent.
- **No translation of the other epic 2 pages** — the verification guide, the contribution process,
  the naming rule, the brick-authoring and contract-entry guides all stay English and served as
  stubs. Only the conventions page is in this epic's scope, and only conditionally.
- **No translation of the planning bundle** under `docs/`, which is not published at all.
- **No editing of the English page to make it easier to translate.** If it needs a fix, that is a fix
  on its own merits.
- **No French-language CI rules** — the checks match the same literal strings in both trees.

## Acceptance criteria / Definition of done

Whichever outcome applies:

- [ ] The settled/not-settled judgement is recorded with the commits it rests on, in the PR or in the
      closing comment.

If translated:

- [ ] Both files exist at their mirror paths with `##` headings matching their originals in set and
      order, and no `verified` stamp.
- [ ] Every literal CI matches on — gap block lead, provisional banner, front matter values, commit
      types — is byte-identical to the English page.
- [ ] Every rule present in English is present in French, and none is added.
- [ ] The check suite is green, including the heading parity and drift rules.

If deferred:

- [ ] The issue is closed as deferred, the French tree serves the generated stub for the page, and no
      partial French file is committed.

## Relevant files / areas

No content exists in this repository yet — paths follow the decided layout
([specs](/specs/04-content-tree.md)) and epic 2's output, and are not verified locations:
`fr/contributing/how-to-write.md`, `fr/contributing/_index.md`,
`en/contributing/how-to-write.md`.

## Dependencies

Blocked by [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md) — specifically its
[issue 01](/epic-2-conventions-contribution-surface/issues/01-add-contributing-and-how-to-write.md),
and by that page having stopped moving. Blocked by
[Issue 01](./01-add-fr-language-and-switch.md), [Issue 03](./03-add-french-tree-validator-rules.md)
and [Issue 06](./06-translate-glossary.md). Does not block
[Issue 09](./09-verify-bilingual-criterion.md) — the epic ships without this page if it has not
settled.

## PR size note

Target ~500 changed lines; one dense page plus a section page, or zero lines if deferred.
