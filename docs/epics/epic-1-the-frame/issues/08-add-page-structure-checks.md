---
type: Issue
title: "Add the page structure checks: headings, provisional banner, gap blocks"
description: "Enforce the required heading list per page type, and the two-way equivalences between maturity and the banner, and between doc_state and the gap block."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/13
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 08
slug: add-page-structure-checks
size: M
status: open
gh_issue: 13
depends_on: [04, 06]
---

# Add the page structure checks: headings, provisional banner, gap blocks

## Summary

The placeholder & maturity convention is the deliverable the scope says not to cut. This issue is
what stops it being cuttable: the markers become equivalences a machine checks in both directions,
so a page cannot be provisional without warning the reader, and cannot carry a gap block while
claiming to be documented.

## Scope

Rules added to `validate`:

- **Required headings per `type`** — presence and order, from `data/vocab.yaml`; and no unknown `##`
  heading on a typed page. Free below `###`.
- **`maturity: provisional` ⟺ the banner** — that exact blockquote present, both directions. A page
  carrying the banner without the marker is equally an error.
- **`doc_state: placeholder` ⟺ a gap block present**, both directions.
- **`maturity: planned` implies a gap block in every content section** — a planned page is made of
  gap blocks; if it can say something true, it is not planned.
- **A section is never deleted** — this is the heading check's other half: a section with nothing
  true to say keeps its heading and carries a gap block, so a missing section and an unwritten one
  cannot look the same.
- The gap block's lead is matched **verbatim** (`> **Not documented yet.**`) so it stays greppable
  and countable, and a hedged variant fails.
- Fixtures first, one per rule.

## Out of scope

- **No prose-truthfulness checks** — forbidden hedges (*may*, *should*, *probably*) describing our
  own knowledge stay a review item; there is no rule for them in v1.
- **No citation rules** — [Issue 09](./09-add-citation-and-terminology-checks.md).
- **No translated-page heading comparison** — the `fr/` page against its original is epic 5. Write
  the heading comparison so a second tree is a caller, not a rewrite.
- No changes to `data/vocab.yaml`'s heading lists; if a template is wrong, fix it in a PR of its own.

## Acceptance criteria / Definition of done

- [ ] A page missing a required heading, and one with the headings out of order, both fail.
- [ ] Each equivalence has a fixture failing in *each* direction — four fixtures minimum.
- [ ] A `planned` page with one section lacking a gap block fails.
- [ ] A gap block with a guessed continuation ("…probably exponential backoff") is not rejected by
      this check, and the PR says so explicitly — that one is a review item, not a rule.
- [ ] The templates from Issue 04 pass every rule unmodified.
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (rule package), `tools/testdata/`, reading
`data/vocab.yaml` and `templates/`.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md) and
[Issue 06](./06-add-front-matter-validator.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
