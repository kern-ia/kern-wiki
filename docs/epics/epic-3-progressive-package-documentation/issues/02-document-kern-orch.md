---
type: Issue
title: "Document kern-orch: install, configuration, usage and integration"
description: "Fill the kern-orch brick page to adoption depth, including graph definition, checkpoints and the provisional agent-CLI seam."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/37
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 02
slug: document-kern-orch
size: L
status: open
gh_issue: 37
depends_on: [01]
---

# Document kern-orch: install, configuration, usage and integration

## Summary

The orchestrator is the brick with the most surface to document and the one the ecosystem is built
around — graph definition, execution, checkpoints, and the seam to agent CLIs. It is also the brick
where the truthfulness rules are hardest to hold: the agent-CLI protocol is **provisional**, agent
nodes execute deterministic stubs rather than model calls because the `kern-agent` bridge does not
exist, and both facts have to stay visible while the page becomes genuinely useful.

Depth follows the pattern [Issue 01](./01-document-kern-link.md) sets.

## Scope

`en/bricks/kern-orch.md`, deepened in place — one page, one PR.

- **Install** — module path quoted verbatim as it exists today, `github.com/yoann/kern-orch`, with
  the `go get` line and any binary (`kern-orch serve` and its siblings) as they are invoked today.
  Go version from `go.mod`.
- **Configuration** — the flags, environment variables and config files `kern-orch` actually reads,
  each documented from the code that reads it, with defaults as the code sets them.
- **Usage patterns** — defining a graph, running it, and what checkpoints do: when one is written,
  what it contains, and what resuming from one guarantees. Checkpointing is the brick's distinctive
  claim and the least documented thing about it elsewhere.
- **Worked examples** — at least one complete graph, run before it is written up, with the output a
  reader should actually see. Agent nodes stated plainly as deterministic stubs.
- **Integration** — what `kern-orch` exposes and needs over the `kern.*` contracts, consistent with
  the front matter and the contract pages. **The provisional banner, verbatim**, wherever the
  agent-CLI seam is described.
- `doc_state`, `verified` and `# Citations` handled as in Issue 01 — stamp the whole page or none of
  it.

## Out of scope

- **No service-environment guidance** — the lost-`HOME` / missing-API-key trap under an empty
  service environment is [Issue 05](./05-document-operational-traps.md). This page does not
  half-document it, and does not imply that running under a service manager is equivalent to
  running in a shell.
- **No protocol specification.** Describe the agent-CLI seam as it is today and mark it provisional;
  the pending extensions are open questions on epic 1's "what's missing" page.
- **No API reference** — `pkg.go.dev`.
- **No re-hosting of `Kern-Orch`'s architecture notes, dev logs, retros or `docs/GLOSSAIRE.md`** —
  the vocabulary already moved to the wiki's glossary in epic 1; the rest stays in the repo.
- **No `Kern-Orch` × `kern-link` seam analysis** — that document belongs to
  [Epic 4](/epic-4-project-map-freshness/EPIC_4.md).
- **No changes to `kern-orch`.** Findings become issues on the brick.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] A developer can install `kern-orch`, define a graph and run it from this page alone.
- [ ] Checkpoint behaviour is described from the code that writes and reads checkpoints, cited by
      path at a version — not from the concept's name.
- [ ] Every flag, environment variable and default named on the page was read where it is consumed.
- [ ] The worked example was executed, and the PR description says on what and with what result.
- [ ] The stub reality — agent nodes are deterministic stubs, not model calls — is stated on this
      page, not only on the "what's missing" page.
- [ ] The provisional banner appears verbatim where the agent-CLI seam is described, and
      `maturity: provisional` is set to match.
- [ ] Sections that stay unfilled keep their headings and their gap blocks.
- [ ] `verified.version` matches the versions in `# Citations`; no partial stamp.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No `en/` tree exists in this repository yet — path follows the decided tree and epic 1's output,
not a verified location: `en/bricks/kern-orch.md`.

Source: `github.com/yoann/kern-orch` at the tag or commit you cite — `go.mod`, the graph and
checkpoint packages, the `serve` command, and whatever reads configuration.

## Dependencies

Blocked by [Issue 01](./01-document-kern-link.md) — the depth pattern.
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s `kern-orch` page (Issue 19), templates (Issue 04)
and contract pages (Issue 22).
Blocks [Issue 05](./05-document-operational-traps.md) and
[Issue 06](./06-verify-one-brick-adoption.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. **L, and it
cannot be split by section** — a content page is never split across two PRs. The allowed split is
the one specs permit: `kern-orch` becomes a directory with an `_index.md`, in its own PR first.
