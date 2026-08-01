---
type: Decision
title: "Site generator & build runtime"
description: "Which static site generator builds the wiki, and what toolchain does that impose on contributors?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 01
slug: site-generator
status: decided
verdict: "Hugo, extended edition, version-pinned in CI and locally"
decided_via: triage
depends_on: []
---

# Question

Scope fixed the delivery form — generator-agnostic markdown in `kern-ia/kern-wiki`, published
with GitHub Pages ([decision](/scope/03-delivery-form.md)) — and deferred the generator here.
Three scope verdicts set the bar:

- a **bilingual EN/FR tree with a language switch** ([decision](/scope/05-content-language.md));
- enough **navigation and search** to carry per-brick technical documentation
  ([decision](/scope/07-coverage-depth.md));
- **zero budget**, GitHub-native tooling only ([decision](/scope/15-constraints.md)).

The generator also chooses the toolchain every contributor installs. With two contributors today
and more expected, all of them Go developers, that is not a neutral cost.

# Options

- **Hugo** — single Go binary, no runtime. Multilingual is a **core feature**, not a plugin:
  per-language content directories, translation linking, language switcher data. Renders
  ` ```mermaid ` fences. Builds in milliseconds. Themes install as Hugo Modules (which uses the
  Go toolchain the team already has). Cost: Go templating is the least pleasant of the four if
  the site ever needs custom layouts.
- **Material for MkDocs** — the best documentation UX of the set, built-in search, huge feature
  surface. But i18n is a third-party plugin, `mkdocs-static-i18n`, whose own README now states it
  is **frozen as-is because MkDocs core upstream is unmaintained and uncertain**. Betting a
  five-milestone bilingual project on a frozen plugin over an uncertain core is the wrong risk to
  take. Also imports a Python toolchain (venv, pinned requirements) for a Go team.
- **Docusaurus** — first-class i18n and versioning, React-based. Content is **MDX**, which is
  precisely what the generator-agnostic constraint forbids: MDX files with components stop
  rendering on GitHub. Imports Node plus a `node_modules` tree.
- **Astro Starlight** — excellent i18n, Pagefind search, clean docs defaults. Imports Node; its
  callouts/asides use directive syntax that does not render on GitHub.
- **Jekyll** — GitHub Pages builds it natively without a workflow. Ruby toolchain, weak
  multilingual story (plugin-based, and the native Pages builder allows no plugins), no built-in
  search.

# Recommendation

**Hugo (extended edition).**

It is the only candidate whose multilingual support is in the core rather than in a plugin, which
matters because the bilingual site is a committed milestone (M5) and the plugin-based alternative
is explicitly frozen. It is a single binary in the team's own language, so "how do I build the
site locally" is a one-line answer — decisive under a *consistency-is-the-binding-constraint*
scope ([decision](/scope/15-constraints.md)). It renders Mermaid from plain fenced code blocks
and resolves relative `.md` links (see [links](/specs/07-links-and-urls.md)), so the
generator-agnostic constraint costs nothing rather than being fought for.

Extended edition specifically: the recommended theme ([decision](/specs/02-theme.md)) compiles
SCSS and requires it. Pin the Hugo version in the workflow and in a `.hugo_version`-style note in
the README so local and CI builds cannot drift.

Rejecting Material for MkDocs is the close call and worth naming: it is the better documentation
tool *today*, and it loses on the one axis this project cannot compromise — a bilingual site
whose i18n layer is frozen and whose core is unmaintained.

# Verdict

**Hugo, extended edition**, accepted at triage. Version pinned in the deploy workflow and stated
in the README so local and CI builds cannot drift. Material for MkDocs is rejected on the frozen
i18n plugin over an unmaintained core; MDX-based generators are rejected by the
generator-agnostic constraint.
