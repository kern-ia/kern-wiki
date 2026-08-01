---
type: Issue
title: "Add the brick-authoring guide"
description: "Publish what makes a package a kern-* brick and what it must declare — including the exposed/needs block — so the wiki absorbs the fifth package without restructuring."
tags: [epic-2]
resource: https://github.com/kern-ia/kern-wiki/issues/34
timestamp: 2026-08-01T12:30:00Z
epic: 2
issue: 05
slug: add-brick-authoring-guide
size: M
status: open
gh_issue: 34
depends_on: [01, 04]
---

# Add the brick-authoring guide

## Summary

The wiki must absorb a new package without restructuring, and a fifth is already in progress. Epic 1
made that true of the *file layout* — a brick is one file, adding it edits no navigation. This issue
makes it true for *people*: what qualifies a package as a `kern-*` brick, what it has to declare,
and what to do on the day it arrives.

The load-bearing part is the **exposed / needs** declaration. It is what the contracts registry and
the exposed/needs matrix are generated from, so a new brick that skips it is invisible to the one
view that shows how the ecosystem fits together.

## Scope

- `en/contributing/brick-authoring.md`:
  - **What makes something a brick** — the criteria, stated so a reader can answer yes or no about a
    package that does not exist yet, rather than by analogy with the four that do.
  - **The exposed / needs declaration**: the `exposes:` and `needs:` front matter fields, contract
    identifiers written with their version (`kern.run.v1`), what "exposes" and "needs" mean at the
    seam, and what happens when a needed contract has no producer yet — a declared need pointing at
    something unbuilt is the honest state, not an error.
  - **Adding the brick to the wiki**, step by step: copy `templates/brick.md` to
    `en/bricks/<name>.md` on the canonical lowercase name, fill front matter, keep every section with
    a gap block, set `doc_state: placeholder` and no stamp, regenerate the listings, open the PR.
    A brick page whose sections are all gap blocks is a **valid, complete** first contribution.
  - **What a new brick's own repository should publish** so the wiki can document it truthfully: a
    README that names the package by its canonical name, its contracts with versions, and a
    resolvable module path. Stated as what the wiki needs, not as a mandate on repos the wiki does
    not own.
  - **What the wiki does not take from the brick** — architecture notes, dev logs, retros,
    changelogs and API reference stay in the repo and on `pkg.go.dev`, per the ownership map.
  - The link to [Issue 04](./04-add-canonical-naming-rule-and-followups.md)'s naming rule for the
    name itself.
- A pointer from `en/contributing/_index.md` and from the bricks section page.

## Out of scope

- **No new brick page.** The fifth package's name and role are still unknown and deliberately left
  open in [the scope](../../../planning/SCOPE.md); this guide is written so that whoever documents
  it needs no further instruction. Writing a page for it now would be invented content.
- **No changes to `templates/brick.md`** — if the template is missing something this guide has to
  explain, fix the template in epic 1's file and reference it here.
- **No changes to brick repositories**, and no issues opened against them.
- **No contract-entry instructions** — [Issue 06](./06-add-contract-entry-guide.md).
- **No `exposes`/`needs` validation code** — the field vocabulary and its checks are epic 1's.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] A contributor can add a new brick page end to end from this guide without asking how, and
      without the result differing from the four pages epic 1 wrote.
- [ ] The exposed/needs section names real contract identifiers with versions, taken from the
      contract pages that exist, not illustrative ones.
- [ ] The guide states explicitly that an all-gap-block brick page is a valid end state.
- [ ] The brick criteria are checkable against a package the reader has in front of them.
- [ ] Nothing in the guide asserts what any repository contains without that having been read and
      cited.
- [ ] `hugo` builds with warnings fatal; `validate` passes; 100-column wrap.

## Relevant files / areas

No existing content for this yet — path follows the decided tree, not verified against this
repository: `en/contributing/brick-authoring.md`, linked from `en/contributing/_index.md` and
`en/bricks/_index.md`.

Sources: `templates/brick.md` and `data/vocab.yaml` as epic 1 leaves them; the exposed/needs
convention as `Kern-UI`'s README states it — read it and name the commit;
[SPECS.md](../../../planning/SPECS.md) §Content architecture and §Data model.

## Dependencies

Blocked by [Issue 01](./01-add-contributing-and-how-to-write.md) and
[Issue 04](./04-add-canonical-naming-rule-and-followups.md).
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s templates (Issue 04), brick pages (Issues 18–21)
and the generated registries (Issue 11) — the guide describes all three.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
