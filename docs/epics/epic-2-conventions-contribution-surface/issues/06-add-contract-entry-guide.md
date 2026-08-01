---
type: Issue
title: "Add the contract-entry guide"
description: "Publish how to add an entry to the contracts registry when the next kern.* contract arrives, including the enforced-versus-provisional distinction."
tags: [epic-2]
resource: https://github.com/kern-ia/kern-wiki/issues/35
timestamp: 2026-08-01T12:30:00Z
epic: 2
issue: 06
slug: add-contract-entry-guide
size: S
status: open
gh_issue: 35
depends_on: [01]
---

# Add the contract-entry guide

## Summary

The contracts registry is the wiki's growing surface: contracts keep accumulating as packages
arrive, and the registry only stays coherent if each new entry is added the same way as the last.
This is the shortest guide in the epic and the one most likely to be needed by someone in a hurry.

The distinction it must get across is the one the scope drew: some contracts are **enforced** —
asserted by CI on both sides, `kern-orch` → `kern-ui` being the reference case — and some are
**provisional and unenforced**, the orch ↔ agent-CLI seam with five extensions pending. A registry
that flattens the two tells readers something false about what they can rely on.

## Scope

- `en/contributing/adding-a-contract.md`:
  - **When something is a contract entry** rather than an implementation detail of one brick.
  - **The identifier form** — `kern.<name>.v<n>`, always written with its version, because a
    contract without its version is not a contract. A new major version is a **new entry**, not an
    edit to the old one.
  - **Adding the page**: copy `templates/contract.md` to `en/contracts/<identifier>.md`, fill
    purpose, producer, consumer, versions, enforcement status, fields and migration; gap blocks for
    what is not yet known; regenerate the registry index and the exposed/needs matrix.
  - **Enforcement status**, spelled out: what qualifies as *enforced* (a check that actually fails
    on both sides, named), what *provisional* means and that it requires the provisional banner
    verbatim, and that "we intend to enforce it" is not an enforcement status.
  - **Updating the producing and consuming brick pages' `exposes:` / `needs:` in the same PR** —
    a contract entry with no brick claiming it is how the matrix goes wrong.
  - **What to do when the contract changes** — the version stamp, the migration section, and the
    rule that the wiki records the contract as it is, not as the proposal being discussed upstream.
- A pointer from `en/contributing/_index.md` and from the contracts section page.

## Out of scope

- **No new contract pages** and no edits to the four epic 1 wrote — this is the instructions, not an
  entry.
- **No changes to `templates/contract.md`** or to the registry generator.
- **No recording of the five pending agent-protocol extensions** — those are open questions, and
  they belong to [Epic 4](/epic-4-project-map-freshness/EPIC_4.md), not to a how-to page.
- **No brick-authoring content** — [Issue 05](./05-add-brick-authoring-guide.md).
- No French translation.

## Acceptance criteria / Definition of done

- [ ] A contributor can add a contract entry from this page alone, with the result indistinguishable
      from the four entries epic 1 wrote.
- [ ] The enforced-versus-provisional distinction is stated with the real reference case on each
      side, named and cited.
- [ ] The guide requires the `exposes:` / `needs:` update in the same PR, explicitly.
- [ ] The new-major-version-is-a-new-entry rule is stated.
- [ ] The provisional banner is quoted byte-identical to the string in `templates/` and CONVENTIONS.
- [ ] `hugo` builds with warnings fatal; `validate` passes; 100-column wrap.

## Relevant files / areas

No existing content for this yet — path follows the decided tree, not verified against this
repository: `en/contributing/adding-a-contract.md`, linked from `en/contributing/_index.md` and
`en/contracts/_index.md`.

Sources: `templates/contract.md` as epic 1 leaves it;
[scope decision 09](../../../planning/scope/09-contract-registry-home.md);
[SPECS.md](../../../planning/SPECS.md) §Data model for the `exposes` / `needs` fields.

## Dependencies

Blocked by [Issue 01](./01-add-contributing-and-how-to-write.md).
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s contract template (Issue 04), contract pages
(Issue 22) and generated registries (Issue 11).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
