---
type: Issue
title: "Add the kern-ui brick page"
description: "Instantiate the brick template for kern-ui — filled where verifiable against the code, gap-blocked everywhere else."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/25
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 20
slug: add-kern-ui-brick-page
size: S
status: open
gh_issue: 25
depends_on: [04, 13, 18]
---

# Add the kern-ui brick page

## Summary

The live view, and the other half of the quickstart's premise. `Kern-UI`'s README is also the source
of the exposed/needs convention the brick template encodes, so this page is where that convention
meets its own origin — if the template's block and the README disagree, say so in the PR rather than
quietly picking one.

## Scope

- `en/bricks/kern-ui.md`, from `templates/brick.md`, every section filled or gap-blocked.
- The **exposed / needs** declaration, in the convention `Kern-UI`'s README states, with contract
  identifiers written with their versions.
- Install, configuration and usage, with the module path quoted verbatim as it exists today.
- What it shows live and what it does not, stated against the code rather than against intent.
- `# Citations` as paths at a version.

## Out of scope

- **No depth** — epic 3 fills the technical sections.
- **No quickstart** — the `kern-orch` + `kern-ui` pairing is [Issue 23](./23-write-verified-quickstart.md).
- **No changes to `Kern-UI`**, including no correction of its README; a disagreement becomes an
  issue on the brick, and the glossary records the repo's spelling as an alias.
- No licence claim.
- No screenshots — static images are not part of the markdown contract for v1.

## Acceptance criteria / Definition of done

- [ ] Every heading required for `type: Brick` is present, in order, none deleted.
- [ ] Every filled statement was checked against `Kern-UI`'s code at a named version, cited by path.
- [ ] The exposed/needs block follows the README's convention, and any divergence is called out in
      the PR description.
- [ ] Every unfilled section carries a gap block naming what is missing, with no guess.
- [ ] Commands are copy-pasteable, use today's module path, and are stamped only if run.
- [ ] The maturity marker matches reality, not intent.
- [ ] The page contradicts nothing in `Kern-UI`'s own README (criterion 5).
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/bricks/kern-ui.md`, from `templates/brick.md`.

Source: the `Kern-UI` repository at the tag or commit you cite, its README included.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md),
[Issue 13](./13-write-home-and-ecosystem-overview.md) and
[Issue 18](./18-add-kern-link-brick-page.md).
Blocks [Issue 23](./23-write-verified-quickstart.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs.
