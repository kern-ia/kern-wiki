---
type: Decision
title: "Content tree & repository layout"
description: "How is the repo laid out — where content, per-language trees, templates, data and tooling live?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 04
slug: content-tree
status: decided
verdict: "Language trees at the repository root (`en/`, `fr/`) as per-language contentDir; six fixed sections; `_index.md` in every directory"
decided_via: triage
depends_on: [site-generator, markdown-contract, okf-conformance]
---

# Question

Scope requires an `en/` tree from day one so that adding `fr/` later **moves no files**
([decision](/scope/12-mvp-cut.md)), and an information architecture where a new brick or contract
**fills a slot rather than triggering a redesign** ([decision](/scope/15-constraints.md)). The
fifth package is the stated test ([decision](/scope/14-success-criteria.md)).

Directory layout is normally cheap to change. Here it is not: every path is a published URL and
an inbound link ([decision](/specs/07-links-and-urls.md)) — and, since the wiki is an OKF bundle,
every path is also a concept ID ([decision](/specs/23-okf-conformance.md)).

# Options

- **Language as a directory, per-language `contentDir`** — Hugo is configured with
  `[languages.en] contentDir = 'en'`. Trees are independent, a translation is a file at the mirror
  path, and the FR tree can be legitimately incomplete — which M5 requires, since only front-door
  pages get translated ([decision](/scope/05-content-language.md)).
- **Language as a filename suffix** — `overview.md` / `overview.fr.md`, side by side. Fewer
  directories; every folder becomes a bilingual mix, "which pages are translated" stops being
  answerable by looking at a tree, and OKF concept IDs acquire a language suffix.
- **Language as a branch or a separate repo** — rejected on sight: two review surfaces for one
  wiki.

Nested inside that: whether the language trees live under `content/` (Hugo's default home) or at
the repository root. OKF settles it — the bundle root must be the repo root for `/`-links to mean
one thing ([decision](/specs/23-okf-conformance.md)), so the trees sit at the root and Hugo is
pointed at them.

# Recommendation

**Language as a directory at the repository root, per-language `contentDir`**, with the section
set fixed by scope:

```
kern-wiki/
├── index.md                # OKF bundle listing (okf_version only)   /specs/23
├── log.md                  # OKF history
├── .okfignore              # everything below that is not knowledge
├── hugo.toml
├── en/                     # contentDir for English
│   ├── _index.md           # home / overview                          (J1)
│   ├── ecosystem/          # philosophy, diagram, glossary, ownership map, what's missing
│   ├── bricks/             # one page per brick, from the brick template  (J3, J6)
│   ├── contracts/          # the registry: one page per kern.* contract
│   ├── integration/        # quickstart and cross-brick guides           (J2)
│   ├── contributing/       # how to write here, process, brick-authoring (J4)
│   └── status/             # transverse status, freshness table, open questions (J5)
├── fr/                     # created at M5, same shape, front-door pages only
├── templates/              # the brick and contract page templates, copyable
├── tools/                  # repo tooling                               /specs/13
├── layouts/                # site-shell overrides only                  /specs/02
├── data/                   # closed vocabularies                        /specs/05
├── static/
└── .github/workflows/
```

Four rules that make the "new brick fills a slot" criterion real:

- **A brick is one file**, `en/bricks/<name>.md`, instantiated from `templates/brick.md`. Adding a
  brick adds one file and zero navigation edits — the sidebar comes from the tree, and the
  section listing is generated ([decision](/specs/06-registries-and-tables.md)).
- **A contract is one file**, `en/contracts/<name>.md`. Same property.
- **Every directory has an `_index.md`**, which is both Hugo's section page and an OKF concept
  document (`type: Section`) carrying the directory's listing. There is deliberately **no**
  `index.md` inside `en/` or `fr/` — that filename is reserved by OKF and would turn the
  directory into a Hugo leaf bundle, silently unpublishing its pages
  ([decision](/specs/23-okf-conformance.md)).
- **Sections are fixed; depth beyond a section is not.** A brick that outgrows one page becomes
  `en/bricks/<name>/` with an `_index.md`, which changes no URL above it.

`templates/` and `tools/` sit outside the content trees and are listed in `.okfignore`: templates
are for humans to copy, and a template page rendered on the live site would be exactly the kind of
empty, plausible-looking page the no-invented-content rule forbids
([decision](/scope/13-non-goals.md)).

# Verdict

**Language trees at the repository root, per-language `contentDir`, six fixed sections**, accepted
at triage. A brick is one file, a contract is one file, and every directory carries an `_index.md`
that is both Hugo's section page and an OKF concept document. No `index.md` inside `en/` or `fr/`.
