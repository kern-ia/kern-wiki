---
type: Issue
title: "Add the French tree validator rules"
description: "Teach validate the four rules that make gaps acceptable and contradictions impossible: no French page without an English original, no French stamp, heading parity with the original, and a French glossary column that covers what the French tree uses."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/53
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 03
slug: add-french-tree-validator-rules
size: M
status: open
gh_issue: 53
depends_on: [01]
---

# Add the French tree validator rules

## Summary

*Gaps between the two languages are acceptable; contradictions are not* is the epic's whole
position, and a position held by discipline is a position held by whoever is in a hurry. This issue
turns it into checks, before the first translation lands rather than after.

Four rules, each deferred here on purpose by epic 1: the no-French-without-English rule the scope
states ([decision](/specs/09-bilingual-mechanism.md)), the inherited-stamp rule
([decision](/specs/05-page-metadata.md)), the heading comparison epic 1 issue 08 left to this epic,
and the glossary's French column epic 1 issue 09 left to this epic.

## Scope

Four validator rules in the existing `validate` subcommand, each arriving with a failing fixture:

- **No French page without an English original.** A file under `fr/` whose mirror path under `en/`
  does not exist is an error, naming both paths. This is the rule the scope states as a rule rather
  than a deferral.
- **No `verified` stamp under `fr/`.** A translation inherits its original's stamp; a second stamp
  asserts a verification that did not happen, and two stamps for one fact is drift by construction.
  The error message says to remove it, not to update it.
- **Heading parity with the original**: same `##` headings, same order, as the original at the mirror
  path. This is the translated-page half of epic 1's heading check — it runs a `fr/` page against its
  English original, not only against its `type`'s template. It is what makes *no FR-only content and
  no FR-only omissions within a translated page* mechanical
  ([decision](/conventions/13-translation-authoring.md)).
- **The glossary's French column covers the French tree.** Every row of `en/ecosystem/glossary.md`
  has a non-empty French cell, and a term used in the French tree that has no French form recorded is
  an error — a translator inventing a French term adds it to the glossary in the same PR
  ([decision](/conventions/10-terminology-and-naming.md)).
- Error messages name the file, the rule and what would satisfy it. The audience is a translator who
  just wrote a page.

## Out of scope

- **No drift detection** — "the original changed after the translation was last touched" needs git
  history and its own permissions; [issue 04](./04-add-translation-drift-lint.md) owns it.
- **No identifier-translation check.** *Identifiers are never translated* is a real rule, but
  distinguishing a translated brick name from ordinary French prose is not something a fixture can
  pin down; it stays a checklist item, and the conventions already say a rule with no fixture is
  weaker than one that has one.
- **No prose quality checks** — Vale and markdownlint are excluded by SPECS and this is not a way
  back in.
- **No changes to epic 1's existing rules**, beyond the extension point the heading check needs.
- **No translated content** — issues 05–08.

## Acceptance criteria / Definition of done

- [ ] Every rule starts as a failing fixture under `tools/testdata/`, committed in the same PR, red
      before green. A rule with no fixture is not merged.
- [ ] A `fr/` page with no `en/` original fails, naming both paths.
- [ ] A `fr/` page carrying `verified` fails, and the message says to remove the stamp.
- [ ] A `fr/` page whose `##` headings differ from its original in set or in order fails, naming the
      first divergence.
- [ ] A glossary row with an empty French cell fails; a French-tree term with no recorded French form
      fails.
- [ ] Each rule's comment names the convention it enforces and links its section.
- [ ] The rules run in CI on every pull request, on both trees, and a repository with no `fr/` content
      still passes — the checks must not go red between this PR and the first translation.
- [ ] `gofmt -l` is silent, `golangci-lint` passes with warnings fatal, `go test ./tools/...` passes.

## Relevant files / areas

No `tools/` binary exists in this repository yet — paths follow the decided layout
([specs](/specs/13-tooling-language.md)) and epic 1's output, and are not verified locations:
`tools/` (the `validate` subcommand from epic 1 issues 05–09), `tools/testdata/`,
`en/ecosystem/glossary.md`.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) — the `validate` subcommand, its front matter
validator, its heading checks and the glossary itself. Blocked by
[Issue 01](./01-add-fr-language-and-switch.md) for the tree these rules describe. Should land before
[Issue 05](./05-translate-home-and-ecosystem-overview.md), so the first translation is checked by
the rules rather than checked against them afterwards.

## PR size note

Target ~500 changed lines; four rules plus fixtures. If it approaches ~1000, split the glossary
column rule out — it is the one that shares nothing with the other three.
