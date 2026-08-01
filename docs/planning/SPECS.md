---
type: Technical Specification
title: "Kern wiki — Technical Specs"
description: "A Hugo site built from an OKF knowledge bundle, published to GitHub Pages, whose truthfulness rules are enforced by CI rather than by discipline."
tags: [planning, specs]
timestamp: 2026-08-01T00:26:20Z
status: final
---

# Kern wiki — Technical Specs

The one-way doors, decided. Everything cheap to reverse — file naming inside a section, internal
refactors of the tooling, page wording — is deliberately absent and belongs to implementation.

Full ledger: [specs decision ledger](/specs/index.md) — 18 decided, 5 not applicable.

## Stack

| Layer | Choice |
|---|---|
| Site generator | **Hugo**, extended edition, version-pinned in CI and locally ([decision](/specs/01-site-generator.md)) |
| Theme | **Hextra**, version-pinned Hugo Module ([decision](/specs/02-theme.md)) |
| Content format | **OKF v0.1** knowledge bundle, CommonMark + GFM markdown ([decision](/specs/23-okf-conformance.md)) |
| Repo tooling | **Go**, one binary in `tools/` ([decision](/specs/13-tooling-language.md)) |
| Hosting | **GitHub Pages**, deployed by GitHub Actions ([decision](/specs/11-hosting-and-deployment.md)) |

No Node, no Python, no Ruby. Hugo is a single binary, Hextra installs as a Hugo Module, and Go is
already on every contributor's machine — with two contributors and more expected, "how do I build
this" has one answer.

Hugo was chosen over Material for MkDocs because its multilingual support is in the core rather
than in `mkdocs-static-i18n`, which is frozen as-is over an unmaintained upstream — and the
bilingual site is a committed milestone. MDX-based generators (Docusaurus, Starlight) are excluded
by the generator-agnostic constraint carried in from scope.

## Content architecture

The repository **is** an OKF knowledge bundle; its root is the bundle root. That single choice
makes `/en/bricks/kern-orch.md` mean the same file to OKF, to GitHub and to a human reading the
tree ([decision](/specs/23-okf-conformance.md)).

```
kern-wiki/
├── index.md              # OKF bundle listing — okf_version only, no other frontmatter
├── log.md                # OKF history, ## YYYY-MM-DD newest first
├── .okfignore            # layouts/ static/ data/ tools/ templates/ .github/ README.md, config
├── hugo.toml
├── en/                   # Hugo contentDir for English
│   ├── _index.md         # home / overview
│   ├── ecosystem/        # philosophy, diagram, glossary, ownership map, what's missing
│   ├── bricks/           # one page per brick
│   ├── contracts/        # the registry — one page per kern.* contract
│   ├── integration/      # quickstart and cross-brick guides
│   ├── contributing/     # how to write here, process, brick-authoring
│   └── status/           # transverse status, freshness table, open questions
├── fr/                   # created at M5, same shape, front-door pages only
├── templates/            # brick and contract page templates, copyable, never published
├── tools/                # validate / gen / stale
├── layouts/              # site-shell overrides only
├── data/                 # closed vocabularies
└── .github/workflows/
```

- **A brick is one file**; a contract is one file. Adding either fills a slot and edits no
  navigation — the sidebar comes from the tree and section listings are generated. A brick that
  outgrows one page becomes a directory with an `_index.md`, changing no URL above it
  ([decision](/specs/04-content-tree.md)).
- **Every directory carries an `_index.md`**, which is simultaneously Hugo's section page and an
  OKF concept document.
- **No `index.md` inside `en/` or `fr/`.** The name is reserved by OKF *and* turns a Hugo directory
  into a leaf bundle that unpublishes its siblings; the bundle's `index.md` and `log.md` live at
  the repository root, outside the content directories.

## Data model

There is no database. Front matter is the schema ([decision](/specs/22-database-and-storage.md)),
composed of the OKF core plus typed project extensions
([decision](/specs/05-page-metadata.md)):

```yaml
type: Brick                      # closed set, data/vocab.yaml
title: "kern-orch"
description: "Graph-based agent orchestration with checkpoints."
tags: [orchestration, graph]
timestamp: 2026-07-31T09:00:00Z  # last meaningful change to this page
resource: https://github.com/yoann/kern-orch
doc_state: partial               # placeholder | partial | documented
maturity: works-today            # works-today | provisional | planned
verified:
  version: v0.2.0
  date: 2026-07-31
brick: kern-orch
exposes: [kern.run.v1]
needs: [kern.agent-cli.v0]
```

Four invariants, enforced rather than trusted:

- **`maturity` describes the code, `doc_state` describes the page, `timestamp` describes the
  file.** Scope's three page states stay distinguishable because these are three fields, not one.
- **A placeholder carries no stamp, and nothing claims `documented` without one** — criterion 1
  (no false information) as a lint rule.
- **"Possibly stale" is derived, never authored.** Humans record what they checked; the staleness
  job decides what has rotted.
- **`resource` is the single repository reference** — a link for readers, the comparison target for
  the staleness job.

Aggregate views are generated into committed markdown between `<!-- BEGIN GENERATED -->` markers,
with regenerate-and-diff enforced in CI ([decision](/specs/06-registries-and-tables.md)): the
freshness table, the contracts registry index, the exposed/needs matrix, every section listing and
the bundle listing. Contract pages and `log.md` stay hand-written — a listing is derivable, a
judgement is not.

## Authoring contract

The wiki's durable public contract, outliving Hugo and Hextra
([decision](/specs/03-markdown-contract.md)):

- **Allowed** — ATX headings, GFM tables, fenced code blocks with a language tag, ` ```mermaid `
  diagrams, task lists, blockquotes, bundle-relative links, mandatory OKF front matter.
- **Forbidden and CI-checked** — any `{{< … >}}` or `{{% … %}}` shortcode, MDX/JSX, raw HTML beyond
  `<br>` and comments, generator-specific directives.
- **Callouts are blockquotes** with a bold lead; the page title lives in front matter, not in an
  `# H1`; technical pages end with `# Citations` naming what was actually read.

**Diagrams** are Mermaid in fenced code blocks, exclusively — the only form that renders both on
GitHub and in the site. Line style encodes maturity: dashed for planned or missing, the
`kern-agent` bridge being the reference case, with a legend node carrying the convention inside the
diagram ([decision](/specs/08-diagrams.md)).

**Links** use one form, `/en/bricks/kern-orch.md` — OKF's recommended bundle-relative form, which
GitHub resolves against the repository root and a custom render hook in
`layouts/_markup/render-link.html` resolves to permalinks. That hook is the project's only bespoke
Hugo templating. URLs are `/{lang}/{section}/{page}/` with the language present for both languages;
`baseURL` is the full project-pages URL; filenames are lowercase kebab-case on the canonical
`kern-*` names ([decision](/specs/07-links-and-urls.md)).

**Moves** keep their old paths as Hugo `aliases`, permanently; a rename without one fails the
validator ([decision](/specs/15-content-moves.md)).

## Bilingual

English is authored, French is translated, and the French tree is permanently partial by design.
The mechanism makes that legible instead of broken ([decision](/specs/09-bilingual-mechanism.md)):

- Per-language `contentDir`; a translation is the file at the mirror path.
- The language switch is always present and always lands on the same subject.
- An untranslated page serves a **generated French stub** pointing at the English original — never
  a silent English page, and never a committed stub asserting nothing.
- Translations inherit their original's version stamp rather than carrying a second one.
- Missing English originals and out-of-date translations are lints, not hopes.

Search is Hextra's built-in FlexSearch: offline, client-side, **one index per language**, with
placeholders indexed so unwritten areas stay findable ([decision](/specs/10-search.md)).

## Deployment & operations

- **GitHub Actions → `actions/deploy-pages` on push to `main`.** No build output in git, no
  versioned trees, no custom domain — `kern-ia.github.io/kern-wiki/`
  ([decision](/specs/11-hosting-and-deployment.md)).
- **Every PR builds the full site** with warnings fatal and uploads it as an artifact. Accepted as
  the weaker option: no preview URL, in exchange for not importing a third-party host into a
  zero-budget GitHub-native project.
- **`GITHUB_TOKEN` only**, least-privilege per job, no PAT and no other repository secrets. A brick
  repo that turns out to be private is not documented rather than reached for with a credential
  ([decision](/specs/17-secrets-and-access.md)). Dependabot watches the Actions.
- **No analytics** — no tracking, no cookie banner, no consent regime. Health signals are the
  deploy failing, the weekly link check, and the staleness issue
  ([decision](/specs/16-observability-and-analytics.md)).

## Testing & enforcement

The Kern repos' own principle — *drift is caught by tests, not by discipline* — applied to
documentation ([decision](/specs/12-ci-checks.md)). On every pull request:

| Check | Guarantees |
|---|---|
| `hugo --gc --minify`, warnings fatal | the site builds; translations and render hooks resolve |
| OKF conformance | parseable front matter with a non-empty `type`; reserved filenames respected; `log.md` headings well-formed |
| Front matter validator | closed vocabularies, `placeholder` ⇏ `verified`, every technical page stamped, `resource` present where required, alias on rename |
| Portability check | no shortcodes, no MDX, no disallowed raw HTML |
| Generated blocks | regenerate-and-diff on all five surfaces |
| Internal links | every bundle-relative target exists, both trees, both surfaces |

Weekly, off the PR path: **external link checking** and the **staleness job**.

All of it lands in **M1, not M4** — the rules are introduced by M1, and shipping them unenforced is
how three people fill the frame three different ways before M2's conventions page can stop them.
Vale and markdownlint are deliberately excluded from v1: the risk here is asserting something
untrue, not comma placement.

The tooling is one Go binary with `validate` / `gen` / `stale` subcommands, standard library plus a
YAML parser and a GitHub API client, unit-tested — the validator encodes criterion 1, so an
untested one would convert an absent guarantee into a false one. Tooling failures gate merges,
never the published site ([decision](/specs/13-tooling-language.md)). OKF's three conformance rules
are reimplemented here rather than adding Python for the reference checker.

**Staleness job** (M4): weekly, metadata only, comparing each page's `verified.version` against the
brick's latest release with a commit-count fallback, writing **one rolling issue**. Placeholders are
listed as *not documented yet* rather than as stale; an unresolvable `resource` is an error, not a
skip; and the job never edits a stamp — a stamp means a human read the code, and a bot refreshing
it would turn the wiki's central honesty mechanism into a lie
([decision](/specs/14-freshness-automation.md)).

## Not applicable, explicitly

- **Auth** — public static site; write access is GitHub repository permissions plus PR review
  ([decision](/specs/18-auth.md)).
- **External integrations** — only GitHub itself and outbound links; each fallback posture is
  decided in place ([decision](/specs/19-external-integrations.md)).
- **Performance & scale** — pre-rendered pages on a CDN; the only budget that matters is the human
  15-minutes-to-a-hello-graph ([decision](/specs/20-performance-and-scale.md)).
- **Background work** — no runtime; the two cron workflows are the whole of it
  ([decision](/specs/21-background-work.md)).
- **Database & migrations** — git is the store, the OKF bundle is the schema
  ([decision](/specs/22-database-and-storage.md)).

## Accepted risks

Two choices are knowingly the weaker option, recorded so they are not rediscovered as mistakes:

- **No PR preview URL** — reviewers download an artifact. Revisit if outside contributions arrive
  at volume; it changes no content.
- **Hextra's bus factor** — one primary maintainer. Bounded by the version pin and by content
  carrying zero theme-specific syntax: a theme swap touches `layouts/` and `hugo.toml`, not one
  content file.

One implementation detail is deliberately unverified and must not be assumed: Hugo's leaf-bundle
classifier versus `ignoreFiles`, the fallback route to per-directory `index.md` files. The decided
layout avoids needing it ([decision](/specs/23-okf-conformance.md)).
