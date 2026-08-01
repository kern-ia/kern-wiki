---
type: Issue
title: "Add the kern-anon brick page"
description: "Instantiate the brick template for kern-anon — filled where verifiable against the code, gap-blocked everywhere else."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/26
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 21
slug: add-kern-anon-brick-page
size: S
status: open
gh_issue: 26
depends_on: [04, 13, 18]
---

# Add the kern-anon brick page

## Summary

The fourth brick page of deliverable 8. `kern-anon` is the brick this plan knows least about, so
this page is the epic's clearest test of the placeholder convention: a page that is mostly gap
blocks and still useful is the intended outcome, not a failure.

## Scope

- `en/bricks/kern-anon.md`, from `templates/brick.md`, every section filled or gap-blocked.
- The **exposed / needs** declaration, with contract identifiers written with their versions.
- Install, configuration and usage, with the module path quoted verbatim as it exists today.
- `doc_state` set honestly — `placeholder` if that is what it is, which carries no stamp.
- `# Citations` as paths at a version, for whatever was read.

## Out of scope

- **No depth** — epic 3 fills the technical sections. Under-filling here is correct.
- **No inference from the name.** *Anon* suggests anonymization; what the brick does is whatever the
  code does. Nothing is described from its name.
- **No changes to `kern-anon`.**
- No licence claim.

## Acceptance criteria / Definition of done

- [ ] Every heading required for `type: Brick` is present, in order, none deleted — including the
      ones that are entirely gap blocks.
- [ ] Nothing on the page is derived from the brick's name; every statement was read somewhere
      citable.
- [ ] `doc_state: placeholder` carries no `verified` stamp; `documented` is not claimed without one.
- [ ] Every gap block names what is missing and, if known, what would settle it — with no guess.
- [ ] The maturity marker matches reality, not intent.
- [ ] The page contradicts nothing in the repository's own docs (criterion 5).
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/bricks/kern-anon.md`, from `templates/brick.md`.

Source: the `Kern-Anon` repository at the tag or commit you cite. If the repository is not readable
with `GITHUB_TOKEN`-level access, it is not documented rather than reached for with a credential —
record that as the page's gap and say so in the PR.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md),
[Issue 13](./13-write-home-and-ecosystem-overview.md) and
[Issue 18](./18-add-kern-link-brick-page.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs.
