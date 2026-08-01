---
type: Decision
title: "Diagrams"
description: "How are the ecosystem diagram and later diagrams authored and rendered?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 08
slug: diagrams
status: decided
verdict: "Mermaid in fenced code blocks, exclusively; dashed edges mean planned or missing"
decided_via: triage
depends_on: [markdown-contract, theme]
---

# Question

Scope names the ecosystem diagram as an M1 deliverable with two hard requirements: it must
**render on GitHub and in the site**, and it must draw the `kern-agent` gap **dashed**, with room
for packages still to come ([decision](/scope/12-mvp-cut.md)). It is also the single artefact J1
leans on — understand Kern in 60 seconds.

# Options

- **Mermaid in fenced code blocks** — GitHub renders ` ```mermaid ` natively; Hextra renders it
  client-side from the same fence ([decision](/specs/02-theme.md)). Diagram source is diffable
  in PR review, dashed edges (`-.->`) are one character, adding a brick is one line. Cost:
  limited layout control, and complex graphs get ugly.
- **Committed SVG/PNG images** — total control, and a binary blob no reviewer can diff, redrawn
  in some external tool nobody else has. For a diagram whose whole job is to change as packages
  arrive, this is the wrong trade.
- **D2 / Graphviz rendered at build time** — better layouts, adds a toolchain and produces
  nothing on GitHub.
- **Excalidraw / draw.io** — pleasant to author, same diff and toolchain problems as images.

# Recommendation

**Mermaid in fenced code blocks, exclusively.**

The requirement "renders on GitHub *and* in the site" is met by exactly one option, and the
diagram's other stated property — that it must accommodate packages not yet named — favours a
text format anyone can extend in a one-line PR.

Two conventions to fix now, since they carry the diagram's meaning:

- **Line style encodes maturity**: solid for a working edge, dashed (`-.->`) for a planned or
  missing one. The `kern-agent` bridge is the reference case. A legend node in the diagram itself
  states this, so the convention travels with the image.
- **One canonical ecosystem diagram**, in `ecosystem/`, included by reference from other pages
  rather than copy-pasted. A second copy is a second thing to keep true.

If a diagram ever genuinely exceeds Mermaid — a sequence across five bricks, say — the escape
hatch is a committed SVG **plus** its source, not a silent switch to images. Revisit then, not
now.

# Verdict

**Mermaid in fenced code blocks, exclusively**, accepted at triage. Line style encodes maturity —
dashed for the `kern-agent` bridge and anything else planned or missing — with a legend node
carrying the convention inside the diagram. One canonical ecosystem diagram, referenced rather than
copied.
