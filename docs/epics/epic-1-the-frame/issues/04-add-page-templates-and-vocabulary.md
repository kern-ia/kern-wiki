---
type: Issue
title: "Add the brick and contract page templates and the closed vocabulary"
description: "Write the copyable brick and contract templates and data/vocab.yaml, which together define every page type, its required headings and its allowed field values."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/9
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 04
slug: add-page-templates-and-vocabulary
size: M
status: open
gh_issue: 9
depends_on: [01]
---

# Add the brick and contract page templates and the closed vocabulary

## Summary

Deliverables 4 and 5 of the epic — the page templates, and the placeholder & maturity convention
they carry. This is the deliverable the scope names as the one not to cut: without it the rest gets
written three different ways. It is also the machine-readable half of it — `data/vocab.yaml` is what
[Issue 06](./06-add-front-matter-validator.md) and
[Issue 08](./08-add-page-structure-checks.md) enforce, so the templates and the checks cannot drift.

## Scope

- `templates/brick.md` — identity, maturity, **exposed / needs**, install, configuration, usage,
  integration, version stamp. The exposed/needs block follows the convention `Kern-UI`'s README
  already states. Copyable, never published.
- `templates/contract.md` — purpose, producer, consumer, versions, enforcement status, fields,
  migration.
- Both templates pre-filled with gap blocks in every content section, the provisional banner shown
  in a comment with its usage rule, and a `# Citations` section — so a page copied from a template
  is already valid and already honest.
- `data/vocab.yaml` — the closed vocabularies and, per `type`, its required `##` heading list in
  order:
  - `type`: the page types in use (`Brick`, `Contract`, `Concept`, `Guide`, `Registry`, … — settle
    the exact set in this PR, it is the closed set everything else validates against).
  - `maturity`: `works-today` | `provisional` | `planned`.
  - `doc_state`: `placeholder` | `partial` | `documented`.
- `templates/README.md` (or a section in the root README) stating the three-field rule verbatim:
  `maturity` describes the code, `doc_state` describes the page, `timestamp` describes the file.
- The gap block and the provisional banner written once, verbatim, so both are greppable and
  countable:
  > **Not documented yet.** *(one line naming what is missing.)*

  > **This describes a provisional interface.** It is expected to change, and changes are not
  > announced.

## Out of scope

- **No validator code** — the vocabulary is data here; enforcing it is
  [Issue 06](./06-add-front-matter-validator.md) and [Issue 08](./08-add-page-structure-checks.md).
- **No instantiated pages** — the brick and contract pages are Issues 18–22.
- **No contributor-facing writing guide** — that is epic 2's rendering of these conventions. This
  issue writes the templates; epic 2 explains them.
- No `templates/` output in the published site.

## Acceptance criteria / Definition of done

- [ ] Both templates carry every heading listed in the epic's scope, in that order.
- [ ] Every content section in both templates carries a gap block; neither template asserts
      anything about any brick or contract.
- [ ] `data/vocab.yaml` parses, and its `type` keys each carry an ordered required-heading list.
- [ ] The heading lists in `vocab.yaml` match the templates exactly — a mismatch here is what
      Issue 08 will later fail on.
- [ ] `templates/` is excluded from the Hugo build and from `.okfignore`'s published surface.
- [ ] The gap block and banner strings are byte-identical to the ones in
      [conventions](../../../planning/CONVENTIONS.md#placeholders--maturity).

## Relevant files / areas

No existing code for this yet — paths follow the decided tree, not verified against this
repository: `templates/brick.md`, `templates/contract.md`, `data/vocab.yaml`.

Source for the exposed/needs convention: `Kern-UI`'s README, read at whatever commit you read it —
name it in the PR.

## Dependencies

Blocked by [Issue 01](./01-initialize-repo-and-okf-bundle-root.md).
Blocks [Issue 06](./06-add-front-matter-validator.md),
[Issue 08](./08-add-page-structure-checks.md) and all content issues (13–24).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
