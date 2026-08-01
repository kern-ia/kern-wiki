---
type: Issue
title: "Document the fifth package once it lands"
description: "Add and fill the fifth brick's page when the package exists — the epic's slot for a brick whose name, role and contracts are unknown to this plan."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/42
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 07
slug: document-fifth-package
size: M
status: open
gh_issue: 42
depends_on: [01]
---

# Document the fifth package once it lands

## Summary

A fifth package is in progress, and its name, role and contracts are unknown to this plan — stated
in the epic as a certainty rather than an assumption. The wiki was built to absorb it without
restructuring: a brick is one file, adding it edits no navigation, and
[Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md)'s brick-authoring guide already says
how.

This issue is the tracking slot for actually doing it. It is **conditional on the package existing**
and having a readable repository. If neither is true when the rest of the epic finishes, close it
unstarted — an unfilled slot is the honest end state, and re-opening it costs nothing.

## Scope

Once the package exists and its repository can be read without a credential:

- `en/bricks/<name>.md`, created from `templates/brick.md` on the canonical lowercase kebab-case
  name, following the brick-authoring guide step by step — if the guide is insufficient, fix the
  guide in the same PR rather than working around it.
- The **exposed / needs** declaration, with contract identifiers written with their versions. A
  declared need pointing at something unbuilt is the honest state, not an error.
- Install, configuration, usage, worked examples and integration, filled to the depth
  [Issue 01](./01-document-kern-link.md) set, and gap-blocked everywhere the reading does not reach.
- Module path quoted verbatim as it exists today, whatever organization it sits under.
- The generated listings, registries and the exposed/needs matrix regenerated, and the ecosystem
  diagram updated if the package changes the picture.
- The glossary extended with any term this package introduces, in the same PR that first uses it.

## Out of scope

- **Nothing written before the package exists.** No page, no name, no placeholder file. A page for a
  package that has not landed is invented content in its purest form.
- **No new contract pages** unless the package brings a contract — and then the contract page
  follows epic 2's contract-entry guide, in its own PR.
- **No restructuring of the bricks section** to accommodate it. If it does not fit the template, the
  finding is that the template is wrong, and fixing it updates every instantiated page in that PR.
- **No changes to the package.**
- No French translation.

## Acceptance criteria / Definition of done

- [ ] The page was produced by following the brick-authoring guide, and any point where the guide
      was insufficient was fixed in the guide in this PR.
- [ ] Every heading required for `type: Brick` is present, in order, none deleted.
- [ ] Nothing on the page is derived from the package's name; every statement traces to a path at a
      version in `# Citations`.
- [ ] The module path is quoted as it exists today and the `go get` line works.
- [ ] `exposes` / `needs` are consistent with the contract pages, and the generated matrix and
      listings are regenerated in the same PR.
- [ ] `doc_state` and `maturity` reflect reality; `placeholder` carries no stamp.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.
- [ ] **Or**: the package has not landed, and the issue is closed unstarted with that stated.

## Relevant files / areas

No `en/` tree exists in this repository yet, and the package itself does not exist as far as this
plan knows — so there is no path to name beyond the pattern: `en/bricks/<name>.md`, from
`templates/brick.md`, plus the generated surfaces epic 1 built.

Source: the package's repository, at the version you cite, once there is one.

## Dependencies

Blocked by [Issue 01](./01-document-kern-link.md) — the depth pattern.
Blocked by [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md)'s brick-authoring guide
(Issue 05), which this issue is the first real exercise of.
Blocked, outside this repository, on the package landing.

## PR size note

Target ~500 changed lines; a new brick page plus regenerated listings sits comfortably under that.
If the package turns out to be large enough to need more, it becomes a directory with an
`_index.md`, in its own PR first.
