---
type: Issue
title: "Add the kern-link brick page"
description: "Instantiate the brick template for kern-link — filled where verifiable against the code, gap-blocked everywhere else."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/23
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 18
slug: add-kern-link-brick-page
size: S
status: open
gh_issue: 23
depends_on: [04, 13]
---

# Add the kern-link brick page

## Summary

One of the four brick pages of deliverable 8, and the first instantiation of the brick template.
Whatever shape this page takes, the other three follow it — so if a template slot turns out to be
wrong, fix it in `templates/` here rather than diverging.

## Scope

- `en/bricks/kern-link.md`, copied from `templates/brick.md`, with every section either filled from
  what was read in the repository or carrying a gap block.
- Identity, maturity marker, and the **exposed / needs** declaration in the convention `Kern-UI`'s
  README states.
- Install, configuration and usage — with the **module path quoted verbatim as it exists today**
  (`github.com/julienlegoux/kern-link`), never normalized to a `kern-ia` path. A `go get` line that
  does not work is a false claim.
- `resource` pointing at the repository; `verified: {version, date}` only if the page genuinely
  qualifies for a stamp.
- `# Citations` naming what was read, as paths at a version.

## Out of scope

- **No depth.** Filling the per-brick technical sections properly is
  [Epic 3](/epic-3-progressive-package-documentation/EPIC_3.md); this issue instantiates the
  template and fills only what is verifiable now.
- **No licence claim.** `kern-link` advertises MIT, but the licence audit is out of scope and the
  other bricks are unknown — treat consistency across bricks as unestablished and do not assert a
  licence comparison.
- **No changes to `kern-link`.** Findings become issues on the brick, not commits here — and not in
  this PR.
- **No API reference** — `pkg.go.dev` regenerates it.
- No template edits beyond ones this instantiation proves necessary; if you change the template,
  every already-instantiated page changes in the same PR.

## Acceptance criteria / Definition of done

- [ ] Every heading required for `type: Brick` is present, in order, none deleted.
- [ ] Every filled statement was checked against `kern-link`'s code at a named version, and that
      version appears in both `# Citations` and `verified.version` if the page is stamped.
- [ ] Every unfilled section carries a gap block naming what is missing, with no guess.
- [ ] The install command is copy-pasteable and uses the module path as it exists today.
- [ ] Installation and configuration examples are stamped only if they were actually run.
- [ ] The maturity marker matches reality, not intent; the provisional banner appears if and only if
      `maturity: provisional`.
- [ ] The page contradicts nothing in `kern-link`'s own README (criterion 5).
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/bricks/kern-link.md`, from `templates/brick.md`.

Source: `github.com/julienlegoux/kern-link` at the tag or commit you cite.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md) and
[Issue 13](./13-write-home-and-ecosystem-overview.md).
Its template findings inform Issues [19](./19-add-kern-orch-brick-page.md),
[20](./20-add-kern-ui-brick-page.md) and [21](./21-add-kern-anon-brick-page.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs.
