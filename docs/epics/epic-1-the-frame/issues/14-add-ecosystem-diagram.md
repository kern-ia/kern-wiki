---
type: Issue
title: "Add the ecosystem diagram"
description: "Draw the bricks and contracts as a Mermaid diagram that renders on GitHub and in the site, with the kern-agent gap dashed and a legend carrying the convention."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/19
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 14
slug: add-ecosystem-diagram
size: S
status: open
gh_issue: 19
depends_on: [13]
---

# Add the ecosystem diagram

## Summary

Deliverable 7. One picture of how the bricks connect through the `kern.*` contracts — and, just as
importantly, where they do not: the `kern-agent` bridge is the ecosystem's highest-value gap and it
is drawn as such.

## Scope

- A Mermaid diagram in a fenced ` ```mermaid ` block on `en/ecosystem/_index.md`, exclusively — the
  only diagram form that renders both on GitHub and in the published site.
- **Line style encodes maturity**: solid for what runs today, **dashed for planned or missing**, the
  `kern-agent` bridge being the reference case.
- **A legend node inside the diagram** carrying that convention, so the diagram is self-explaining
  wherever it is rendered.
- Layout that leaves room for packages still to come — a fifth package is in progress and its name
  and role are unknown to this plan; adding it must be adding a node, not redrawing.
- Edges labelled with the contract identifier and version they carry (`kern.run.v1`, never
  `kern.run`).

## Out of scope

- **No image files, no SVG, no external diagram tool.** Mermaid in a fenced block, exclusively.
- **No sequence or deployment diagrams** — one ecosystem view.
- **No speculative nodes.** A package whose name and role are unknown is not drawn; the room left
  for it is layout, not a placeholder box.
- No restatement of the mapping table; the diagram uses lowercase brick names.

## Acceptance criteria / Definition of done

- [ ] The diagram renders on GitHub's markdown view **and** in the built site — check both, and say
      in the PR that you did.
- [ ] Every dashed edge or node corresponds to something that does not exist today, and every solid
      one to something verified against a named version.
- [ ] The legend is a node in the diagram, not prose beside it.
- [ ] Every contract on an edge is written with its version.
- [ ] Adding a node for a new brick requires no other change to the diagram.
- [ ] `hugo` builds; `validate` passes; the portability check accepts the block.

## Relevant files / areas

No existing content for this yet. Path: `en/ecosystem/_index.md` (extending the page written by
[Issue 13](./13-write-home-and-ecosystem-overview.md)).

## Dependencies

Blocked by [Issue 13](./13-write-home-and-ecosystem-overview.md).
Feeds [Issue 17](./17-add-whats-missing-page.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
