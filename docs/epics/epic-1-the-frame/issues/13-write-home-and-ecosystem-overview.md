---
type: Issue
title: "Write the home page and the ecosystem overview"
description: "Write what Kern is, the brick philosophy, and plainly what runs today versus what is planned — including the repository-name mapping table."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/18
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 13
slug: write-home-and-ecosystem-overview
size: M
status: open
gh_issue: 18
depends_on: [02, 04]
---

# Write the home page and the ecosystem overview

## Summary

Deliverable 6, and journey J1 — understand Kern in 60 seconds. `github.com/kern-ia` currently says
nothing about what Kern is; this is the page that fixes that. It carries the epic's sharpest risk:
the brick READMEs describe Kern as running AI agents, and today no LLM can run in a graph because
the `kern-agent` bridge does not exist. The page must be readable in a minute and still not
overpromise.

## Scope

- `en/_index.md` — what Kern is, in the first screen; the brick philosophy; and plainly what runs
  today versus what is planned, per brick, using the maturity markers.
- `en/ecosystem/_index.md` — the ecosystem section's own page: how the pieces relate, and the
  **repository-name mapping table**, which is the one place a repository's real name appears
  (`kern-orch` → `github.com/yoann/kern-orch`, and so on for all four). Module paths are quoted
  verbatim as they exist today, never normalized to what they ought to become.
- Links onward to the quickstart, the bricks, the contracts and the "what's missing" page — as
  bundle-relative links, tolerating targets that land later in the epic only if they exist by the
  time this merges.
- First use of each glossary term links the glossary.

## Out of scope

- **No diagram** — [Issue 14](./14-add-ecosystem-diagram.md) adds it to the ecosystem page.
- **No glossary** — [Issue 15](./15-add-glossary.md).
- **No per-brick detail** — a line each, then a link. The brick pages are Issues 18–21, and their
  depth is epic 3.
- **No licence claims.** Only `kern-link` advertises MIT and the licence audit is out of scope; this
  stays an open unknown.
- No marketing register: no *powerful*, *seamless*, *simply*, *just*, *blazing*.

## Acceptance criteria / Definition of done

- [ ] A reader who has never heard of Kern can say what it is and what runs today, from the home
      page alone, in under a minute.
- [ ] Every claim about a brick is checked against that brick's code or README at a named version,
      and cited under `# Citations` as a path at a version.
- [ ] Nothing planned is described as existing; the `kern-agent` gap is stated, not implied.
- [ ] Anything unverified carries a gap block, never a hedge — no *may*, *should* or *probably*
      about our own knowledge.
- [ ] Front matter carries `type`, `title`, `description`, `tags`, `timestamp`, `doc_state`,
      `maturity`, and `verified` only if the page is genuinely stamped.
- [ ] Bricks in prose are lowercase and backticked; capitalized spellings appear only in the mapping
      table.
- [ ] `hugo` builds and `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet — only `docs/` exists in this repository. Paths: `en/_index.md`,
`en/ecosystem/_index.md`.

Sources to read (not to paraphrase from memory): the four brick repositories' READMEs, at the commit
or tag you cite.

## Dependencies

Blocked by [Issue 02](./02-add-hugo-site-and-link-render-hook.md) and
[Issue 04](./04-add-page-templates-and-vocabulary.md).
Blocks [Issue 14](./14-add-ecosystem-diagram.md), [Issue 15](./15-add-glossary.md),
[Issue 16](./16-add-ownership-map.md) and [Issue 17](./17-add-whats-missing-page.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs — its correctness is internal coherence, and a reviewer can only judge
that whole.
