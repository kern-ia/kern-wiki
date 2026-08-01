---
type: Issue
title: "Initialize the repository skeleton and the OKF bundle root"
description: "Create the repository's directory skeleton, the OKF bundle root files and the empty en/ section tree, so every later PR has a slot to fill."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/6
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 01
slug: initialize-repo-and-okf-bundle-root
size: M
status: open
gh_issue: 6
depends_on: []
---

# Initialize the repository skeleton and the OKF bundle root

## Summary

`kern-ia/kern-wiki` currently holds nothing but the planning bundle under `docs/`. This issue lays
down the shape every other issue in the epic writes into: the repository root **is** the OKF bundle
root, with an `en/` content tree whose six sections already exist as empty-but-honest section pages,
so adding `fr/` at epic 5 moves no file and adding a brick at epic 3 fills a slot.

## Scope

- `index.md` at the repository root — the OKF bundle listing, carrying `okf_version: "0.1"` and
  **no other frontmatter**. Its listing body is hand-written for now; it becomes a generated block
  in [Issue 10](./10-add-gen-listings.md).
- `log.md` at the repository root — OKF history, `## YYYY-MM-DD` headings newest first, with the
  first entry recording the repository's creation.
- `.okfignore` listing `layouts/`, `static/`, `data/`, `tools/`, `templates/`, `.github/`,
  `README.md`, `docs/` and the Hugo config.
- `README.md` — what this repository is, and **how to add a page**: which section, copy a template,
  the frontmatter that is required, how it gets published. Short; the contributor-facing version is
  epic 2's, not this one's.
- `en/_index.md` plus an `_index.md` for each of the six sections — `ecosystem/`, `bricks/`,
  `contracts/`, `integration/`, `contributing/`, `status/`. Each is simultaneously a Hugo section
  page and an OKF concept document, so each carries full frontmatter and, having nothing true to say
  yet, a gap block.
- Empty `templates/`, `tools/`, `layouts/`, `data/` and `.github/workflows/` directories (kept with
  their real first file where one exists, otherwise a `.gitkeep`).
- `.gitignore` covering Hugo's build output (`public/`, `resources/`, `.hugo_build.lock`).

## Out of scope

- **No `hugo.toml`, no theme, no build** — [Issue 02](./02-add-hugo-site-and-link-render-hook.md).
- **No workflows** — [Issue 03](./03-add-pages-deploy-and-pr-build.md).
- **No page templates and no `data/vocab.yaml`** —
  [Issue 04](./04-add-page-templates-and-vocabulary.md).
- **No `index.md` anywhere inside `en/`** — the name is reserved by OKF and turns a Hugo directory
  into a leaf bundle that unpublishes its siblings.
- No real content on the section pages beyond the gap block; the home page itself is
  [Issue 13](./13-write-home-and-ecosystem-overview.md).

## Acceptance criteria / Definition of done

- [ ] The root `index.md` carries `okf_version: "0.1"` and nothing else in its frontmatter.
- [ ] `log.md` parses as OKF history: `## YYYY-MM-DD` headings, newest first.
- [ ] Every `_index.md` under `en/` has parseable frontmatter with a non-empty `type`, and carries
      the gap block verbatim: `> **Not documented yet.**` followed by one line naming what is
      missing.
- [ ] `docs/` appears in `.okfignore` — one published bundle, one private one, sharing a checkout.
- [ ] No file named `index.md` exists under `en/`.
- [ ] Markdown is hard-wrapped at 100 columns; tables and fenced blocks exempt.
- [ ] `README.md` states how to add a page, in second person, with no marketing register.

## Relevant files / areas

No existing code for this yet — the repository contains only `docs/`. The paths below are the tree
decided in [specs](../../../planning/SPECS.md#content-architecture), not verified against anything
that exists:

```
index.md  log.md  .okfignore  README.md  .gitignore
en/_index.md
en/{ecosystem,bricks,contracts,integration,contributing,status}/_index.md
templates/  tools/  layouts/  data/  .github/workflows/
```

## Dependencies

None. Blocks every other issue in [Epic 1](/epic-1-the-frame/EPIC_1.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
