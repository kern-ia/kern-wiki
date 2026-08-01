---
type: Issue
title: "Add the contribution process page"
description: "Publish how a change lands: local setup, branch and commit conventions, what CI runs, self-merge on green, and where to open an issue."
tags: [epic-2]
resource: https://github.com/kern-ia/kern-wiki/issues/32
timestamp: 2026-08-01T12:30:00Z
epic: 2
issue: 03
slug: add-contribution-process-page
size: M
status: open
gh_issue: 32
depends_on: [01]
---

# Add the contribution process page

## Summary

The mechanical half of journey **J4** (make a first contribution): a contributor knows *what* to
write after [Issue 01](./01-add-contributing-and-how-to-write.md) and *when it is true enough* after
[Issue 02](./02-add-verification-and-review-checklist.md) — this page is how the change actually
gets from their machine to the site.

It carries the epic's accepted risk on its face: GitHub will not surface a `CONTRIBUTING.md` for
this project, because `kern-ia/.github` is out of scope. This page is what the wiki offers instead,
so it must be findable from the home page and the README rather than only from the section listing.

## Scope

- `en/contributing/process.md`:
  - **Setup** — the pinned Hugo extended version and how to install it, `hugo server` for a local
    preview, Go for `tools/`, and the fact that there is no Node, Python or Ruby anywhere in the
    build. Commands must be run before they are written down.
  - **Making a change** — one branch per issue, `issue-<n>-<slug>`, short-lived; a PR closes exactly
    one issue with `Closes #<n>`; a content page is never split across two PRs, because its
    correctness is internal coherence and a reviewer can only judge that whole.
  - **Commit convention** — the re-aimed type table (`feat:`, `fix:`, `content:`, `chore:`,
    `refactor:`, `test:`) with `content:` explained: the repository's most common commit, a
    placeholder becoming prose, is neither a feature nor a fix. Imperative subject, no trailing
    period, optional disambiguating scope. A commit that changes a `verified` stamp names the
    version read in its body.
  - **What CI runs on your PR**, as a table of check → what it guarantees → what a failure means you
    should change: the Hugo build with warnings fatal, OKF conformance, the front matter validator,
    portability, generated blocks, internal links, the Go checks, and the non-blocking stamp
    coverage comment. Plus: every PR uploads the built site as an artifact — **there is no preview
    URL**, which is a decided trade, not an oversight.
  - **How it lands** — green CI is the only gate, no approval is required on any area, self-merge is
    permitted wherever the checks pass; `main` is protected against force-push and direct push.
  - **Where to open an issue** — the routing rule, resolved against the ownership map: a wrong or
    missing *page* is an issue on `kern-wiki`; a wrong or missing *brick behaviour* is an issue on
    the brick's own repository. Name the two explicitly so the default is not "open it here".
  - The note that a regenerated block or a `gofmt` diff is a `git` operation, not a hand edit.
- Pointers to this page from `en/contributing/_index.md`, from the home page, and from the
  repository `README.md`.

## Out of scope

- **No `CONTRIBUTING.md`** — not in `kern-ia/.github` (out of scope for the epic, and the reason
  this page exists), and not at this repository's root either: the epic serves J4 entirely from wiki
  pages, and adding one here would create a second place for the process to rot. If the accepted
  risk turns out to bite, that is a scope change, not a quiet addition in this PR.
- **No issue or PR templates**, no code of conduct, no security policy.
- **No CI changes** — this page describes the workflows epic 1 built; if a check behaves differently
  from what is written here, the fix is in the workflow or in an epic 1 issue, not a hedge on this
  page.
- **No branch-protection changes** on `main`.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] Every command on the page was run on a clean checkout before being written down, and the Hugo
      version named matches the pin in CI exactly.
- [ ] The CI table lists every check that actually runs on a PR today — no check invented, none
      omitted.
- [ ] The page states plainly that no approval is required and that self-merge on green is expected.
- [ ] The issue-routing rule resolves the wiki-versus-brick question without the reader consulting
      anyone.
- [ ] The absent `CONTRIBUTING.md` is addressed on the page rather than left as a surprise.
- [ ] The page is reachable from the home page and the README, not only from the section listing.
- [ ] `hugo` builds with warnings fatal; `validate` passes; 100-column wrap.

## Relevant files / areas

No existing content for this yet — path follows the decided tree, not verified against this
repository: `en/contributing/process.md`, plus link edits in `en/_index.md`,
`en/contributing/_index.md` and `README.md`.

Sources: [CONVENTIONS.md](../../../planning/CONVENTIONS.md) §Git & PRs and §Review & merge, and
[SPECS.md](../../../planning/SPECS.md) §Testing & enforcement and §Deployment & operations — checked
against the workflows as epic 1 actually left them, which is the authority when they disagree.

## Dependencies

Blocked by [Issue 01](./01-add-contributing-and-how-to-write.md).
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s workflows and checks (Issues 03 and 05–12) — the
page documents them, so it cannot be written truthfully before they run.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
