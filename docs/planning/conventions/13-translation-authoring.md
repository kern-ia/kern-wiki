---
type: Decision
title: "Translation authoring rules"
description: "M5 writes French, but the rules that keep FR from diverging must exist while EN is being written."
tags: [decision, conventions]
timestamp: 2026-08-01T09:34:00Z
phase: conventions
decision: 13
slug: translation-authoring
status: decided
verdict: "translation is transposition — same path, headings and order, identifiers untranslated, stamps inherited never re-earned; English writers keep headings descriptive from M1"
decided_via: triage
depends_on: [terminology-and-naming, stamping-and-done]
---

# Question

SPECS decided the *mechanism* — mirror paths, generated stubs, inherited stamps, lints for
missing originals ([decision](/specs/09-bilingual-mechanism.md)). It did not decide how a
translator writes: whether the French page may restructure, add an example, or translate a
technical term. Criterion 10 is that every French page says the *same thing* as its original, and
the scope accepts gaps between languages but not contradictions.

The rules are needed now, not at M5: English pages written between M1 and M4 are what M5
translates, and untranslatable choices made now cost more later.

# Options

- **Translation is transposition** — same paths, same headings, same order, same claims; only the
  prose language changes.
- **Translation is adaptation** — a French reader may need different examples or ordering.
  Produces two wikis that drift, and no mechanical way to see it happening.
- **Defer to M5** — and discover at M5 that the English pages assumed an English reader
  (idioms, wordplay in headings, screenshots with English UI).

# Recommendation

**Translation is transposition**, plus a small number of rules that make English translatable:

For the translator:

- **Same path, same headings, same order.** The heading-order check the validator runs on typed
  pages ([decision](/conventions/08-page-structure-and-templates.md)) applies to `fr/` against
  its original, not just against the template.
- **No FR-only content and no FR-only omissions within a translated page.** A page is translated
  whole or not present — the generated stub covers "not present"
  ([decision](/specs/09-bilingual-mechanism.md)). This is what makes "gaps yes, contradictions
  no" mechanically true.
- **Identifiers are never translated**: brick names, contract names, field names, commands, code
  blocks and their comments stay as they are. Only prose is translated.
- **Technical vocabulary follows the glossary's French column** — the glossary becomes bilingual
  at M5, and it is the only place a term's French form is decided
  ([decision](/conventions/10-terminology-and-naming.md)). A translator inventing a French term
  adds it to the glossary in the same PR.
- **Stamps are inherited, never re-earned** — the translator did not read the code, so the French
  page carries the original's `verified` block unchanged
  ([decision](/conventions/12-stamping-and-done.md)). Re-stamping a translation would assert a
  verification that did not happen.
- **The original changes first.** A correction discovered while translating is fixed in `en/`
  and then translated — never fixed only in French.

For English writers, from M1:

- **Headings are descriptive, not clever.** No puns, no idioms, no metaphors in headings — they
  translate badly and the diff between languages becomes unverifiable.
- **Screenshots and diagram labels are avoided where a table or Mermaid node would do**; Mermaid
  labels are text and translate, an image does not.

# Verdict

**Translation is transposition**, accepted at triage, with both halves of the rule set: the
translator keeps path, headings and order, translates no identifier, follows the glossary's
French column, inherits the original's stamp rather than re-earning it, and fixes discovered
errors in `en/` first. A page is translated whole or absent — the generated stub covers absent,
which is what makes "gaps yes, contradictions no" mechanically true.

The two English-side rules apply **from M1**, not M5: descriptive headings rather than clever
ones, and Mermaid labels in preference to images.
