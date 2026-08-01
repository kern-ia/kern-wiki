---
type: Issue
title: "Document kern-ui: install, configuration, usage and integration"
description: "Fill the kern-ui brick page to adoption depth — how it attaches to a run, what it renders, and what it does not."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/38
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 03
slug: document-kern-ui
size: M
status: open
gh_issue: 38
depends_on: [01]
---

# Document kern-ui: install, configuration, usage and integration

## Summary

`kern-ui` is the live view over a run, and the half of the quickstart a reader reaches for second.
Epic 1's quickstart proved the `kern-orch` + `kern-ui` pairing end to end for one hello graph; this
issue documents the brick on its own terms — how it is installed, how it attaches to a run, what it
shows while the run is going, and where it stops.

Depth follows the pattern [Issue 01](./01-document-kern-link.md) sets.

## Scope

`en/bricks/kern-ui.md`, deepened in place — one page, one PR.

- **Install** — module path verbatim as it exists today, the `go get` line and however the server is
  started, with the Go version taken from `go.mod`.
- **Configuration** — the address it binds, where it reads run data from, and every other setting
  documented from the code that reads it.
- **Usage patterns** — attaching to a run in progress, what happens on reconnect, and what the
  reader sees for a run that has already finished. Described from behaviour that was observed or
  read, never from what a live view would presumably do.
- **What it renders and what it does not** — stated against the code. This is the page where the
  gap between "live run visualization" as a phrase and the current implementation is most likely to
  be papered over.
- **Worked example** — one run watched from start to finish, executed before it is written up.
- **Integration** — the contracts it consumes to receive run data, consistent with the `exposes:` /
  `needs:` front matter and with the contract pages.
- `doc_state`, `verified` and `# Citations` as in Issue 01.

## Out of scope

- **No quickstart rewrite** — `en/integration/quickstart.md` is epic 1's page. If this issue finds
  it wrong, fix it in a separate PR against that page rather than duplicating it here.
- **No screenshots or static images** — not part of the markdown contract for v1, so the page
  describes the view in prose.
- **No API reference** — `pkg.go.dev`.
- **No correction of `Kern-UI`'s README.** It is the origin of the exposed/needs convention; a
  disagreement becomes an issue on the brick and, for spelling, a glossary alias.
- **No changes to `kern-ui`.**
- No French translation.

## Acceptance criteria / Definition of done

- [ ] A developer can install `kern-ui` and watch a run from this page alone.
- [ ] Every setting named on the page was read where it is consumed; nothing from a field's name.
- [ ] What the view does *not* show is stated explicitly, not left to be inferred from silence.
- [ ] The example run was executed, and the PR description says what was observed.
- [ ] Sections that stay unfilled keep their headings and their gap blocks.
- [ ] `verified.version` matches the versions in `# Citations`; no partial stamp.
- [ ] The provisional banner appears if and only if `maturity: provisional`.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No `en/` tree exists in this repository yet — path follows the decided tree and epic 1's output,
not a verified location: `en/bricks/kern-ui.md`.

Source: the `Kern-UI` repository at the tag or commit you cite — `go.mod`, the server entry point,
the code that ingests run data, and the README that states the exposed/needs convention.

## Dependencies

Blocked by [Issue 01](./01-document-kern-link.md) — the depth pattern.
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s `kern-ui` page (Issue 20), templates (Issue 04),
contract pages (Issue 22) and quickstart (Issue 23), which this page links rather than repeats.
Blocks [Issue 06](./06-verify-one-brick-adoption.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs.
