---
type: Decision
title: "Documentation theme & site shell"
description: "Which Hugo theme provides navigation, search, the language switch and the docs layout?"
tags: [decision, specs]
timestamp: 2026-07-31T23:48:30Z
phase: specs
decision: 02
slug: theme
status: decided
verdict: "Hextra, installed as a version-pinned Hugo Module, with no theme shortcodes in content"
decided_via: discussion
depends_on: [site-generator]
---

# Question

The theme is not cosmetics here: it supplies the sidebar navigation, the search index, the
language switcher and the page furniture. Those are exactly the affordances the wiki's
information architecture assumes ([decision](/scope/12-mvp-cut.md)), and swapping a theme after
content exists means re-checking every page's rendering.

# Options

- **Hextra** — modern docs/blog theme, no JavaScript build step and **no Node.js**. Ships
  built-in offline full-text search (FlexSearch) with no configuration, Mermaid from fenced code
  blocks, Hugo multilingual support, dark mode, and a GitHub Pages workflow in its starter
  template. Installs as a Hugo Module. Cost: relatively young, one primary maintainer.
- **Docsy** — the CNCF-grade Hugo docs theme, used by Kubernetes and friends. Multilingual,
  versioning, mature. Cost: requires a Node/PostCSS pipeline, and its weight is aimed at
  multi-hundred-page sites with many maintainers.
- **Hugo Relearn** — very mature, excellent multilingual and print support, heavy on
  theme-specific shortcodes. Those shortcodes are the failure mode the markdown portability
  contract forbids ([decision](/specs/03-markdown-contract.md)) — the theme's best features are
  exactly the ones we would have to refuse.
- **Custom / minimal theme** — total control, and a permanent maintenance tax on a project whose
  binding constraint is contributor consistency, not design.

# Recommendation

**Hextra**, installed as a Hugo Module and pinned to a specific version.

It covers search, i18n switch, navigation and Mermaid without adding a second toolchain — the
same argument that picked Hugo, applied one level down. Critically, everything it needs from a
page is either front matter or plain markdown: nothing in the wiki's content has to be written
*for Hextra*, so the theme stays replaceable and the pages stay GitHub-readable.

Two guardrails, since a theme is a one-way door only if you let it be:

- **No Hextra shortcodes in content pages.** Callouts, cards and tabs are tempting and are
  theme lock-in. If a page needs a callout, it gets a blockquote
  ([decision](/specs/03-markdown-contract.md)).
- **Theme overrides live in `layouts/`**, versioned in the repo, and are limited to the site
  shell and generated-index layouts — never to per-page content.

Docsy is the safer choice on maintainer bus-factor alone; it is rejected because its Node
pipeline reintroduces the toolchain cost that decided
[the generator](/specs/01-site-generator.md), for features (versioned docs, large-org taxonomy)
that scope explicitly does not want — latest-only, no versioned trees
([decision](/scope/16-freshness-and-versioning.md)).

# Verdict

**Hextra, as a version-pinned Hugo Module**, chosen after discussion.

Flagged for deep-dive at triage, and the trade-space had narrowed by the time it was examined:
three decided verdicts already remove the theme's usual differentiators — no theme shortcodes in
content ([decision](/specs/03-markdown-contract.md)), our own link render hook
([decision](/specs/07-links-and-urls.md)), our own untranslated-page stub layout
([decision](/specs/09-bilingual-mechanism.md)). What the theme actually supplies is sidebar
navigation, per-language search, the language switch and dark mode.

The maintenance risk — a young theme with one primary maintainer — was weighed and accepted,
because it is bounded by a decision already taken: content carries **zero** theme-specific syntax,
so a theme swap touches `layouts/` and `hugo.toml` and not one content file. That makes the theme
a reversible choice rather than a one-way door, which is what justifies preferring the
batteries-included young theme over the heavier, better-staffed one.

Docsy was rejected for reintroducing a Node/PostCSS toolchain — the second toolchain that decided
[the generator](/specs/01-site-generator.md) — in exchange for features scope explicitly does not
want. Relearn was rejected because its shortcode library is its principal value and
[the markdown contract](/specs/03-markdown-contract.md) forbids using it.

The two guardrails in the recommendation stand as part of this verdict: no Hextra shortcodes in
content pages, and theme overrides confined to `layouts/` for the site shell and generated-index
layouts.
