---
type: Issue
title: "Add the four contract pages"
description: "Instantiate the contract template for the four known kern.* contracts, each stating its enforcement status."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/27
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 22
slug: add-contract-pages
size: M
status: open
gh_issue: 27
depends_on: [04, 13]
---

# Add the four contract pages

## Summary

Deliverable 9 — the contracts registry. The contracts are what make the bricks an ecosystem rather
than four repositories, and the field that matters most on each page is the **enforcement status**:
a contract nothing checks is a different object from one both sides validate against, and a reader
choosing a brick needs to know which they are looking at.

## Scope

- One page per known `kern.*` contract under `en/contracts/`, each from `templates/contract.md`:
  purpose, producer, consumer, versions, **enforcement status**, fields, migration.
- Identifiers written **always with their version** — `kern.run.v1`, never `kern.run`.
- The provisional banner, verbatim, on any contract whose interface is provisional — the
  orch↔agent-CLI seam being the known case.
- Fields documented from the code that defines them, never from their names; anything unread carries
  a gap block.
- The four pages consistent with the `exposes` / `needs` fields on the brick pages, which is what
  [Issue 11](./11-add-generated-registries.md)'s matrix will render.

## Out of scope

- **No registry index page written by hand** — the contracts index is a generated surface
  ([Issue 11](./11-add-generated-registries.md)). Contract pages stay hand-written; a listing is
  derivable, a judgement is not.
- **No relocation of the `kern.*` fixtures** — rejected in scope.
- **No freezing of the provisional agent-CLI protocol by documentation.** Describe what it is today
  and mark it provisional; the pending extensions are open questions on
  [Issue 17](./17-add-whats-missing-page.md)'s page.
- **No `kern-contracts` extraction discussion** — that is an epic 4 open question.
- **No changes to any brick.**

## Acceptance criteria / Definition of done

- [ ] Four pages exist, one per known contract, each with every `type: Contract` heading in order.
- [ ] Every page states its enforcement status explicitly — including "nothing enforces this", where
      that is the truth.
- [ ] Every identifier on every page carries its version.
- [ ] Producer and consumer named on each page match the `exposes` / `needs` fields on the brick
      pages; a mismatch is resolved in this PR or recorded as a gap on both sides.
- [ ] The provisional banner appears verbatim if and only if `maturity: provisional`.
- [ ] Fields are documented from the defining code, cited by path at a version.
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Paths: `en/contracts/<contract>.md` × 4, from
`templates/contract.md`.

Sources: the `kern.*` fixtures and the code defining each contract, in the brick repositories, at
the versions you cite.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md) and
[Issue 13](./13-write-home-and-ecosystem-overview.md).
Blocks [Issue 23](./23-write-verified-quickstart.md), which stamps a contract version.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR — four contract
pages is the unit here, and splitting it means splitting by contract, never splitting a page.
