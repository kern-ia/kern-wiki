---
type: Decision
title: "Markdown portability contract"
description: "Exactly which markdown syntax is allowed in wiki pages, so every page renders on GitHub and in the site?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 03
slug: markdown-contract
status: decided
verdict: "CommonMark + GFM only, mandatory OKF frontmatter, mechanically enforced"
decided_via: triage
depends_on: [site-generator, theme, okf-conformance]
---

# Question

Scope's constraint is "plain, generator-agnostic markdown — no shortcodes, no generator-specific
syntax" ([decision](/scope/03-delivery-form.md)). That is a principle; it needs a line a
contributor and a CI check can both apply. Left vague, it decays the first time someone wants a
nice callout box.

This is the wiki's real public contract: it outlives Hugo, outlives Hextra, and it is what makes
"read the repo on GitHub" a permanent fallback rather than an aspiration.

# Options

- **CommonMark + GFM only** — the intersection that GitHub and Hugo's Goldmark both render:
  tables, task lists, strikethrough, autolinks, fenced code blocks with language tags,
  ` ```mermaid ` diagrams, and YAML front matter (which GitHub renders as a table).
- **CommonMark + GFM + a short allowlist of Hugo/Hextra shortcodes** — nicer pages, at the cost
  of raw `{{< callout >}}` text appearing on GitHub, which is the visible-brokenness the scope
  constraint exists to prevent.
- **No rule, review by taste** — the option the *consistency is the binding constraint* verdict
  ([decision](/scope/15-constraints.md)) rules out on its own.

# Recommendation

**CommonMark + GFM only, mechanically enforced.**

Allowed: ATX headings, GFM tables, fenced code blocks with a language tag, ` ```mermaid `
diagrams, task lists, blockquotes, bundle-relative `/en/…md` links
([decision](/specs/07-links-and-urls.md)), and YAML front matter conforming to the page schema
([decision](/specs/05-page-metadata.md)).

Front matter is **mandatory on every page**, not optional decoration: an OKF concept document
without parseable frontmatter carrying a non-empty `type` is not merely untidy, it makes the
bundle non-conformant ([decision](/specs/23-okf-conformance.md)).

Forbidden, and checked in CI ([decision](/specs/12-ci-checks.md)): any `{{< … >}}` or `{{% … %}}`
shortcode, MDX/JSX, raw HTML beyond `<br>` and `<!-- -->` comments (the generated-table markers
in [registries](/specs/06-registries-and-tables.md) use HTML comments), and generator-specific
directive syntax.

Two conventions that follow, and belong in M2's "how to write here" page:

- **Callouts are blockquotes** with a bold lead — `> **Provisional.** …`. Renders identically in
  both places; carries the maturity vocabulary ([decision](/scope/20-documenting-the-gap.md))
  without any markup.
- **Body headings follow OKF's conventional set where they apply** — `# Schema`, `# Examples`,
  `# Citations` — and a technical page ends with `# Citations` naming what was actually read to
  write it. That is the no-invented-content rule given a place to live rather than a slogan
  ([decision](/specs/23-okf-conformance.md)).
- **The page title lives in front matter, not in a `# H1`.** OKF's `title` is the display name,
  Hugo renders it, and a duplicated H1 would appear twice on the site and drift from the metadata
  the listings are generated from.

The rule is a floor, not a ceiling on quality: everything the wiki needs — diagrams, tables,
version stamps, maturity markers, placeholders — is expressible inside it. That is what makes it
enforceable rather than aspirational.

# Verdict

**CommonMark + GFM only, mechanically enforced**, accepted at triage. Shortcodes, MDX and raw HTML
beyond `<br>` and comments fail CI. Callouts are blockquotes, titles live in front matter, and
technical pages end with `# Citations`.
