---
type: Issue
title: "Add the fr/ language configuration and the language switch"
description: "Declare French as a second Hugo language with its own contentDir and search index, and turn on the always-present language switch — the configuration half of the bilingual site, with no page translated yet."
tags: [epic-5]
resource: https://github.com/kern-ia/kern-wiki/issues/51
timestamp: 2026-08-01T17:45:00Z
epic: 5
issue: 01
slug: add-fr-language-and-switch
size: S
status: open
gh_issue: 51
depends_on: []
---

# Add the fr/ language configuration and the language switch

## Summary

Epic 1 configured `en` as a language rather than as the site, precisely so that this issue is adding
a block instead of restructuring a tree
([epic 1 issue 02](/epic-1-the-frame/issues/02-add-hugo-site-and-link-render-hook.md)). This is the
issue that cashes that in: French becomes a declared language with its own `contentDir`, its own
search index, and a language switch that is present on every page.

No page is translated here. The point of separating this from the translations is that everything
downstream — the stub layout, the lints, the four translated pages — needs a working `fr` language
to exist against, and a bilingual build that breaks should break in a pull request that changed
configuration, not in one that changed prose.

## Scope

- **A second language block in `hugo.toml`**: `fr`, with `contentDir = "fr"`, a language name and
  weight, mirroring the `en` block's shape. URLs stay `/{lang}/{section}/{page}/` with the language
  present for both languages ([decision](/specs/07-links-and-urls.md)) — `en` does not become
  implicit now that it has a sibling.
- **The `fr/` directory exists** with whatever minimum Hugo needs to treat it as a content root. No
  content pages: this issue creates the tree, not the edition.
- **The language switch is always present**, on every page of both trees, and always lands on the
  same subject ([decision](/specs/09-bilingual-mechanism.md)). Where the counterpart does not exist,
  it still switches — [issue 02](./02-add-untranslated-stub-layout.md) supplies what the reader
  lands on.
- **One search index per language** — Hextra's FlexSearch, already enabled in epic 1, extended to
  the second language rather than reconfigured ([decision](/specs/10-search.md)).
- **Translation linking is by mirrored path**, with no `translationKey` on any page. The escape
  hatch stays unused while paths mirror; adding it pre-emptively would be a second mechanism to keep
  in sync.
- Whatever the switch needs in `layouts/` stays site-shell only — the theme override budget is
  `layouts/` and `hugo.toml`, and content carries zero theme-specific syntax.

## Out of scope

- **No translated page.** Issues 05–08 own the content, and mixing configuration with prose makes
  the first French page's review about Hugo instead of about French.
- **No stub layout** — [issue 02](./02-add-untranslated-stub-layout.md).
- **No French tree lints** — [issue 03](./03-add-french-tree-validator-rules.md).
- **No change to any `en/` page.** Adding a language moves no file; if this issue touches `en/`
  content, the epic 1 tree was wrong and that is a separate fix.
- **No third language, and no language-agnostic abstraction for a third.** Two are decided; a
  general mechanism for an undecided third is invented content in configuration form.

## Acceptance criteria / Definition of done

- [ ] `hugo --gc --minify` builds both languages with warnings fatal.
- [ ] Every page in `en/` renders a language switch, and following it produces a `/fr/…` URL at the
      mirror path.
- [ ] `en/` URLs are unchanged from before this PR — the language was already in the path.
- [ ] Two search indexes are produced, one per language, and searching in one does not return the
      other's results.
- [ ] No content page is added, modified or moved by this PR.
- [ ] The site remains readable on GitHub: nothing this PR adds puts a shortcode or raw HTML into a
      content file.

## Relevant files / areas

No site exists in this repository yet — only `docs/`. Paths follow the decided layout
([specs](/specs/04-content-tree.md)) and epic 1's output, and are not verified locations:
`hugo.toml`, `fr/`, `layouts/`.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) — the Hugo site, the Hextra theme, the `en`
language block and the search configuration. Blocks every other issue in this epic.

## PR size note

Target ~500 changed lines; this one should be well under it — a configuration block, a directory and
a switch. If it is growing past that, the growth is the stub layout leaking in from
[issue 02](./02-add-untranslated-stub-layout.md).
