---
type: Issue
title: "Document kern-anon: install, configuration, usage and integration"
description: "Fill the kern-anon brick page to whatever depth the code supports — the epic's clearest test of stopping at what was actually read."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/39
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 04
slug: document-kern-anon
size: M
status: open
gh_issue: 39
depends_on: [01]
---

# Document kern-anon: install, configuration, usage and integration

## Summary

`kern-anon` is the brick the plan knows least about, which makes it the epic's sharpest test of its
own rule: the page gets exactly as deep as the reading supports, and no deeper. Detection and
anonymization are a domain where a plausible-sounding sentence is very easy to write and very hard
for a reader to falsify — which entity types are recognized, what "anonymized" replaces a value
with, whether anything is reversible. Every one of those is read or gap-blocked.

Depth follows the pattern [Issue 01](./01-document-kern-link.md) sets. A page that ends up half gap
blocks and wholly true is a successful outcome for this issue, not a partial one.

## Scope

`en/bricks/kern-anon.md`, deepened in place — one page, one PR.

- **Install** — module path quoted verbatim as it exists today, `go get` line, Go version from
  `go.mod`.
- **Configuration** — every setting documented from the code that consumes it, defaults as set.
- **Usage patterns** — the calls an adopter makes and what comes back, including the exact shape of
  the transformation applied to a detected value. If reversibility is not established in the code,
  it is a gap block naming the question, not an omission and not a guess.
- **Detection coverage** — what the code detects, as a table, taken from the definitions themselves
  rather than from the README's summary; and what it explicitly does not.
- **Worked example** — one complete program, run before it is written up, showing input and the
  actual output.
- **Integration** — what it exposes and needs over the `kern.*` contracts, consistent with the front
  matter and the contract pages. Where it participates in no contract, the page says so.
- `doc_state`, `verified` and `# Citations` as in Issue 01.

## Out of scope

- **No inference from the name.** *Anon* suggests anonymization; the page documents what the code
  does. This is restated from epic 1 because it is the standing risk on this brick.
- **No privacy, compliance or regulatory claims** of any kind — no GDPR, no "safe to log", no
  assertion that output is de-identified. The wiki documents behaviour; it does not certify it.
- **No API reference** — `pkg.go.dev`.
- **No changes to `kern-anon`.** Findings become issues on the brick.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] Every statement on the page traces to a path at a version in `# Citations`.
- [ ] The detection table was built from the definitions in the code, and its provenance is named.
- [ ] Reversibility is either documented from the code or carries a gap block naming it — never
      implied either way.
- [ ] The page makes no compliance or privacy-guarantee claim.
- [ ] The worked example was executed, and the PR description says so.
- [ ] Sections that stay unfilled keep their headings and their gap blocks; `doc_state` reflects
      what the page actually is, and `placeholder` carries no stamp.
- [ ] `verified.version` matches the versions in `# Citations`; no partial stamp.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No `en/` tree exists in this repository yet — path follows the decided tree and epic 1's output,
not a verified location: `en/bricks/kern-anon.md`.

Source: the `Kern-Anon` repository at the tag or commit you cite — `go.mod`, the detector
definitions, the transformation code, and whatever reads configuration.

## Dependencies

Blocked by [Issue 01](./01-document-kern-link.md) — the depth pattern.
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s `kern-anon` page (Issue 21), templates
(Issue 04) and contract pages (Issue 22).
Blocks [Issue 06](./06-verify-one-brick-adoption.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs.
