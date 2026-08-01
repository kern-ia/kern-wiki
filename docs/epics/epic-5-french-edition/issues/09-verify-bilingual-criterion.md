---
type: Issue
title: "Read the site in French end to end and fix what it exposes"
description: "Discharge the epic's acceptance criterion by browsing the published French tree as a reader — every French page has an English original and says the same thing — and fixing what that surfaces."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/59
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 09
slug: verify-bilingual-criterion
size: S
status: open
gh_issue: 59
depends_on: [02, 05, 06, 07]
---

# Read the site in French end to end and fix what it exposes

## Summary

The epic has one acceptance criterion — **every French page has an English original and says the
same thing** — and half of it is now a lint. The other half is not: whether two pages *say the same
thing* is a judgement, and the checks that passed on each translation PR read one page at a time.

This issue is the pass that reads the French tree as a reader does, following the switch, hitting
stubs, and checking claims against their originals. Its output is the fixes it finds. If it finds
nothing, that is a result worth recording rather than a sign the issue was unnecessary.

## Scope

- **Browse the published French site end to end**: home, ecosystem overview and diagram, glossary,
  quickstart, and the conventions page if [issue 08](./08-translate-conventions-page-if-settled.md)
  translated it. Follow the language switch in both directions from each.
- **Land on stubs on purpose** — a per-brick page, a contract page, a status page — and confirm each
  one reads as an honest gap in French, names the page it stands in for, and links through to a
  working English original.
- **Compare claim by claim**, not paragraph by paragraph, on each translated page. A French sentence
  that hedges where its original states, or states where its original hedges, is a contradiction even
  when both are grammatical.
- **Search in French** and confirm the results are French-tree results, and that a term with a French
  form in the glossary finds the page that uses it.
- **Fix what this exposes**, small and in place: a mistranslated claim, a link that did not get
  rewritten to its mirror, a heading that drifted, a term that does not match the glossary column.
  Anything wrong in the English original is fixed in `en/` first and then in `fr/`.
- Record the pass — what was read, what was found — so the next person knows the criterion was
  discharged by reading rather than by assertion.

## Out of scope

- **No new translations.** A page found untranslated is a stub doing its job, not a defect.
- **No new checks.** If this pass finds a class of error a fixture could catch, open an issue for the
  rule rather than adding it here — the conventions want the rule and its fixture in one PR of their
  own.
- **No structural change** to the tree, the switch or the stub layout.
- **No re-verification of code claims.** Stamps are inherited; a translator reading the French
  quickstart does not re-earn its stamp, and this pass does not either.
- **No prose polish** on the English tree beyond what a real contradiction forces.

## Acceptance criteria / Definition of done

- [ ] Every page in the French tree was opened, and every one either is a translation whose original
      exists or is a generated stub linking a working original.
- [ ] The language switch was followed in both directions from every translated page and landed on
      the same subject each time.
- [ ] At least one stub was reached from the French navigation and read as an honest gap, in French.
- [ ] French search returns French-tree results, and a glossary term finds the page that uses it.
- [ ] Every contradiction found is fixed, English side first where the English page was wrong.
- [ ] What was read and what was found is recorded, including a nil result.
- [ ] The check suite is green and `hugo --gc --minify` passes with warnings fatal.

## Relevant files / areas

The published site at `kern-ia.github.io/kern-wiki/`, both trees. Fixes land in `fr/` and, where the
original was wrong, in `en/`. No `tools/` change is expected from this issue.

## Dependencies

Blocked by [Issue 02](./02-add-untranslated-stub-layout.md),
[Issue 05](./05-translate-home-and-ecosystem-overview.md),
[Issue 06](./06-translate-glossary.md) and [Issue 07](./07-translate-quickstart.md) — the tree has
to be readable before it can be read. Not blocked by
[Issue 08](./08-translate-conventions-page-if-settled.md): if that page was deferred, this pass reads
its stub instead. Last issue in [Epic 5](/epic-5-french-edition/EPIC_5.md).

## PR size note

Target ~500 changed lines, and expect far fewer — the deliverable is the fixes, and a large diff here
means the translation PRs merged with problems the checks could have caught.
