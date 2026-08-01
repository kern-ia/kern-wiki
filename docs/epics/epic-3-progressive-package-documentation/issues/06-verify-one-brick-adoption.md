---
type: Issue
title: "Verify one-brick adoption on a clean machine and fix what it exposes"
description: "Adopt one brick into a fresh Go project using only its wiki page, then fix every gap the attempt exposes — the epic's adoption criterion, discharged by doing it."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/41
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 06
slug: verify-one-brick-adoption
size: M
status: open
gh_issue: 41
depends_on: [01, 02, 03, 04]
---

# Verify one-brick adoption on a clean machine and fix what it exposes

## Summary

The epic's acceptance criterion 7 is *a developer installs, configures and uses one brick in their
own Go project from its wiki section alone*. That is not a criterion anyone can review a diff
against — it is verified by doing it, the way epic 1 verified the quickstart by running it.

Take a clean machine and a fresh Go module, pick a brick, and adopt it using **nothing but its wiki
page**. Every time you have to open a repository, a README or `pkg.go.dev` to get unstuck, that is a
defect on the page, and this issue closes it.

## Scope

- **Do the run first**, on a clean machine, in a fresh module, with the brick repositories closed.
  Record every point where the page was insufficient, in the order they were hit.
- Repeat for a **second brick**, if the first run exposes little — one clean run is a weak sample.
- **Fix what the run exposed**, on the brick pages themselves: missing prerequisites, a step that
  assumed knowledge from another page, a configuration value with no stated default, an example that
  does not compile from a fresh module, an import path that is right in the repo and wrong here.
- Where a gap cannot be closed by writing — the information genuinely is not established — it
  becomes a **gap block naming what is missing**, and `doc_state` drops to match.
- **Re-stamp only what was re-verified.** A page whose stamp no longer covers it has its `doc_state`
  lowered rather than a stale stamp left in place.
- Record the outcome in the PR description: which brick, which machine, how long it took, and what
  had to be fixed.

## Out of scope

- **No new pages.** This issue corrects the four brick pages; anything it exposes that needs a page
  of its own becomes an issue, not a file in this PR.
- **No ecosystem quickstart work** — the `kern-orch` + `kern-ui` end-to-end run is epic 1's
  quickstart. This is the *narrow* reader: one brick, own project, no interest in Kern.
- **No changes to any brick.** A gap that is a defect in the brick rather than in the page becomes
  an issue on the brick, opened separately.
- **No CI-executed adoption check** — deferred with the same reasoning as the quickstart's; the
  version stamp is the interim mitigation.
- **No "all placeholders filled" target.** The epic has no completeness finish line; a page that is
  honest about what it does not cover passes this issue.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] The PR description names the brick(s), the machine, and how long the adoption took.
- [ ] Every point where the page was insufficient during the run is either fixed on the page or
      recorded as a gap block naming what is missing.
- [ ] No step in the fixed page depends on knowledge that is not on it or on a page it links.
- [ ] Every example touched by this issue compiles and runs from a fresh module as written.
- [ ] Any stamp changed is a re-verification, and any page not re-verified has its `doc_state`
      lowered rather than its stamp left standing.
- [ ] Defects that belong to a brick are listed in the PR description with the issue opened on that
      brick, and are not fixed here.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No `en/` tree exists in this repository yet — paths follow the decided tree and epic 1's output,
not verified locations: `en/bricks/kern-link.md`, `en/bricks/kern-orch.md`, `en/bricks/kern-ui.md`,
`en/bricks/kern-anon.md`.

Source for the run: only the published wiki. That constraint is the method.

## Dependencies

Blocked by [Issue 01](./01-document-kern-link.md), [Issue 02](./02-document-kern-orch.md),
[Issue 03](./03-document-kern-ui.md) and [Issue 04](./04-document-kern-anon.md) — there is nothing
to adopt from until the pages carry adoption depth.
Runs best after [Issue 05](./05-document-operational-traps.md), which is where an unattended run
would otherwise fail.

## PR size note

Target ~500 changed lines; most of this issue's cost is the run, not the diff. If the fixes turn out
to rewrite a page wholesale, that page's rewrite is its own PR — a content page is never split
across two PRs.
