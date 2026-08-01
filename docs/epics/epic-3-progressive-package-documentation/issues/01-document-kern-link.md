---
type: Issue
title: "Document kern-link: install, configuration, usage and integration"
description: "Fill the kern-link brick page to adoption depth, and set the depth pattern the other three brick pages follow."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/36
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 01
slug: document-kern-link
size: L
status: open
gh_issue: 36
depends_on: []
---

# Document kern-link: install, configuration, usage and integration

## Summary

`kern-link` is the clearest case of the narrow reader this epic serves — a Go developer who wants a
unified LLM API across providers and does not care that Kern exists. If any brick can be adopted
from its wiki section alone, it is this one, so it goes first and **sets the depth pattern** the
other three follow: how much detail an Install section carries, what a worked example looks like,
how a provider table is shaped, where the line between the wiki and `pkg.go.dev` falls in practice.

[Epic 1](/epic-1-the-frame/EPIC_1.md) instantiated `en/bricks/kern-link.md` from the template and
filled only what was verifiable in passing. This issue reads the repository properly and replaces
the gap blocks that can be replaced.

## Scope

`en/bricks/kern-link.md`, deepened in place — one page, one PR.

- **Install** — the module path quoted verbatim as it exists today,
  `github.com/julienlegoux/kern-link`, with the `go get` line as it works today. Go version
  requirement taken from `go.mod`, not assumed.
- **Configuration** — how a provider is selected, how credentials are supplied, what the defaults
  are, and which settings have to be set for the package to work at all. Every field documented from
  the code that defines it; anything unread keeps its gap block.
- **Provider coverage** — the ~35 providers as **one GFM table**, not one subsection each: provider,
  the identifier the code uses, and whatever per-provider caveat was actually read. A count taken
  from the code, not from the README's prose, if the two disagree.
- **Usage patterns** — the calls an adopter makes, in the order they make them, with the shape of
  the request and response types as the code defines them.
- **Worked examples** — at least one complete, compiling Go program a reader can paste into a fresh
  module. It is **run before it is written up**; runnable content is stamped only after being run.
- **Integration** — what `kern-link` exposes and needs over the `kern.*` contracts, consistent with
  the `exposes:` / `needs:` front matter and with the contract pages, linked rather than restated.
- `doc_state` raised to whatever the page honestly is; `verified: {version, date}` set only if the
  whole page qualifies, and `# Citations` grouped by brick and version naming every path read.

## Out of scope

- **No daemon-mode OAuth guidance** — the impersonation trap and the API-keys-only rule are
  [Issue 05](./05-document-operational-traps.md). This page must not assert in the meantime that
  the OAuth path is safe for long-running processes; if the configuration section reaches that
  question, it carries a gap block naming it, never a hedge.
- **No API reference.** Signatures, types and doc comments belong to `pkg.go.dev`.
- **No re-hosting of repository internals** — architecture, dev logs, retros, changelog stay in
  `kern-link`.
- **No design rationale.** `kern-link` tracks `@earendil-works/pi-ai`; the page documents usage and
  points upstream for why.
- **No changes to `kern-link`.** Anything found while reading becomes an issue on the brick, opened
  separately, not a commit here.
- **No template change.** Worked examples are `###` subsections under the existing Usage heading;
  the template's section set is binding.
- No French translation — per-brick technical pages stay English-only.

## Acceptance criteria / Definition of done

- [ ] A Go developer who has never heard of Kern can install, configure and call `kern-link` from
      this page alone, in their own module.
- [ ] Every `go get`, import path and command on the page was executed and works today.
- [ ] The worked example compiles and runs as written, from a fresh module, and the PR description
      says so.
- [ ] Every configuration field and provider entry was read in the code; nothing is described from
      its name.
- [ ] The provider table's contents were taken from the code, and any disagreement with the README
      is stated on the page rather than silently resolved.
- [ ] Sections that stay unfilled keep their headings and their gap blocks — no deletions.
- [ ] `verified.version` matches the versions named in `# Citations`, and no stamp is set unless the
      whole page was checked at that version.
- [ ] The provisional banner appears if and only if `maturity: provisional`.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

This repository is still documentation-only — no `en/` tree exists yet, so the path below follows
the decided tree and epic 1's output rather than a verified location:
`en/bricks/kern-link.md`, against `templates/brick.md` and `data/vocab.yaml`.

Source: `github.com/julienlegoux/kern-link` at the tag or commit you cite — `go.mod`, the provider
implementations, and whatever defines the configuration surface.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s brick page for `kern-link` (Issue 18), its
templates (Issue 04) and its contract pages (Issue 22).
Should follow [Epic 2](/epic-2-conventions-contribution-surface/EPIC_2.md) — several people write
these pages and the conventions exist so they write them the same way.
Blocks [Issue 02](./02-document-kern-orch.md), [Issue 03](./03-document-kern-ui.md),
[Issue 04](./04-document-kern-anon.md), [Issue 05](./05-document-operational-traps.md) and
[Issue 07](./07-document-fifth-package.md) — all of which follow the depth pattern set here.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. **L, and it
cannot be split by section**: a content page is never split across two PRs
([conventions](../../../planning/CONVENTIONS.md#page-structure--templates)). If it genuinely
outgrows one page, the split is the one specs allow — `kern-link` becomes a directory with an
`_index.md`, changing no URL above it — and that restructure is its own PR, before this one.
