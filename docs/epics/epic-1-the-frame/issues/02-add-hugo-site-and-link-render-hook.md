---
type: Issue
title: "Add the Hugo site with the Hextra theme and the link render hook"
description: "Configure Hugo and the pinned Hextra module, and add the render hook that resolves OKF bundle-relative links to site permalinks."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/7
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 02
slug: add-hugo-site-and-link-render-hook
size: M
status: open
gh_issue: 7
depends_on: [01]
---

# Add the Hugo site with the Hextra theme and the link render hook

## Summary

Turn the markdown tree from [Issue 01](./01-initialize-repo-and-okf-bundle-root.md) into a site that
builds. The one bespoke piece is the link render hook: content links are written once, in OKF's
bundle-relative form, and must resolve on GitHub *and* in the published site — GitHub resolves them
against the repository root, the hook resolves them to permalinks.

## Scope

- `hugo.toml` — extended-edition Hugo, version pinned; `baseURL` set to the full project-pages URL
  `https://kern-ia.github.io/kern-wiki/`; per-language `contentDir` with `en` configured now;
  URLs of the form `/{lang}/{section}/{page}/` with the language present.
- Hextra installed as a **version-pinned Hugo Module** (`go.mod`, `go.sum`, module imports in
  config). No theme-specific syntax reaches any content file.
- `layouts/_markup/render-link.html` — resolves `/en/bricks/kern-orch.md`-style targets to
  permalinks, and fails the build (rather than silently emitting a dead link) on a target that does
  not resolve.
- Hextra's built-in FlexSearch enabled, one index per language, with placeholder pages indexed.
- Hugo's ignore list excluding `docs/`, `templates/` and `tools/` from the build.
- A pinned Hugo version recorded in one place that both CI and a contributor's machine read.

## Out of scope

- **No `fr/` language configuration** — epic 5. Configure `en` in a way that adding a second
  language is adding a block, not restructuring.
- **No CI** — [Issue 03](./03-add-pages-deploy-and-pr-build.md) consumes this.
- **No layout work beyond the site shell and the render hook.** The render hook is the project's
  only bespoke Hugo templating; anything else is a signal the theme is being fought.
- No custom domain, no analytics, no cookie banner.

## Acceptance criteria / Definition of done

- [ ] `hugo --gc --minify` builds the tree from Issue 01 with **warnings fatal**, exit 0.
- [ ] The Hugo version and the Hextra module version are both pinned, not floating.
- [ ] A bundle-relative link in a content page renders as a working site permalink, and the same
      link resolves on GitHub's own markdown view.
- [ ] A bundle-relative link to a non-existent target fails the build.
- [ ] Search returns a page whose `doc_state` is `placeholder`.
- [ ] `docs/`, `templates/` and `tools/` produce no published output.
- [ ] `gofmt -l` reports nothing (the Hugo Module `go.mod` is the only Go artifact here).

## Relevant files / areas

No existing code for this yet — paths follow the tree decided in
[specs](../../../planning/SPECS.md#content-architecture), not verified against this repository:
`hugo.toml`, `go.mod`, `go.sum`, `layouts/_markup/render-link.html`, `layouts/` shell overrides.

One implementation detail is deliberately unverified and must not be assumed: Hugo's leaf-bundle
classifier versus `ignoreFiles`. The decided layout avoids needing it — if you find yourself
reaching for it, say so in the PR.

## Dependencies

Blocked by [Issue 01](./01-initialize-repo-and-okf-bundle-root.md).
Blocks [Issue 03](./03-add-pages-deploy-and-pr-build.md) and all content issues.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
