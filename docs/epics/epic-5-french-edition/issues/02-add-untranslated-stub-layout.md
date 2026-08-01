---
type: Issue
title: "Add the generated French stub for untranslated pages"
description: "Serve a build-time French stub pointing at the English original wherever a translation is absent, so the French tree is legibly partial instead of silently English."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/52
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 02
slug: add-untranslated-stub-layout
size: M
status: open
gh_issue: 52
depends_on: [01]
---

# Add the generated French stub for untranslated pages

## Summary

The French tree is permanently and intentionally partial — front-door pages only, while the per-brick
sections stay English. This issue is what makes that state legible rather than broken: a French URL
with no translation serves a short French stub saying so and linking the English original
([decision](/specs/09-bilingual-mechanism.md)).

The two rejected alternatives are worth restating, because both are cheaper to implement. A silent
fallback to English makes the site look complete and lie about it — against the project's one
non-negotiable. A committed stub file per untranslated page is an OKF concept document asserting
nothing, fifty of them, drifting the moment a real translation lands.

## Scope

- **A layout, not committed files.** The stub is rendered at build time from `layouts/`, so it can
  never drift from reality and nobody hand-writes it. This is the one place a build-time template is
  right, because the artefact is a signpost rather than content.
- The stub states, in French, that the page is not translated yet, and **links through to the English
  original** at the mirror path. It names the page it stands in for — a signpost that does not say
  where it points is a wall.
- **The French navigation shows the page**, so a reader browsing in French sees the whole shape of
  the wiki and hits an explanation rather than an absence.
- The stub is **not** indexed as if it were content, and carries no `verified` stamp, no maturity
  banner and no gap block — it is not a page making claims. It must not be counted as a documented
  page by anything downstream.
- Works for both regular pages and section pages, so a section whose `_index.md` is untranslated
  behaves the same as a leaf page rather than producing an empty French section.

## Out of scope

- **No silent English fallback**, in any form, including "just for section pages".
- **No committed `fr/` stub file.** If this PR adds a markdown file under `fr/` whose content is
  "pas encore traduit", the approach went wrong.
- **No translated content** — issues 05–08.
- **No stub in the other direction.** English is the source language; an `en/` page with no French
  counterpart is the normal state and needs no signpost.
- **No "help translate this" call to action.** The contribution surface is epic 2's, and a link into
  a process page from a generated stub is a second place for that process to rot.

## Acceptance criteria / Definition of done

- [ ] A French URL with no counterpart file serves the stub, in French, with a working link to the
      English original at the mirror path.
- [ ] No `.md` file under `fr/` is added by this PR.
- [ ] The language switch on an English page lands on the stub rather than 404ing or staying put.
- [ ] Once a real translation exists at that path, the stub is not rendered for it — verified with at
      least one temporary fixture page, or with the first real translation if it lands first.
- [ ] `hugo --gc --minify` builds with warnings fatal, both languages.
- [ ] The stub carries no version stamp and no gap block, and does not appear as a documented page in
      the freshness table or any generated listing.

## Relevant files / areas

No site exists in this repository yet — paths follow the decided layout
([specs](/specs/04-content-tree.md)) and epic 1's output, and are not verified locations:
`layouts/`, `hugo.toml`.

## Dependencies

Blocked by [Issue 01](./01-add-fr-language-and-switch.md) — there is nothing to stub until `fr` is a
declared language. Should land before [Issue 05](./05-translate-home-and-ecosystem-overview.md), so
the first real translation lands into a French tree that already reads correctly.

## PR size note

Target ~500 changed lines; a layout plus its fixtures. If it approaches ~1000, the extra is probably
theme-shell work that belongs in [Issue 01](./01-add-fr-language-and-switch.md) or nowhere.
