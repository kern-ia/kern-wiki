---
type: Decision
title: "Documenting what doesn't exist yet"
description: "The bridge that would let Kern run a real LLM agent doesn't exist, and the target architecture isn't fully known. What does the wiki say?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 20
slug: documenting-the-gap
status: decided
verdict: "Describe the target architecture, with an explicit placeholder + maturity convention — structure first, content progressively, never invented content"
decided_via: discussion
depends_on: [coverage-depth, mvp-cut]
---

# Question

`kern-orch` never calls an LLM itself: every `agent` node spawns an external CLI subprocess
(`KERN_AGENT_CLI`). `kern-link` is a library and ships no binary speaking that protocol. The
compat analysis is blunt:

> **zero integration exists today**: kern-link ships no binary that speaks §3.
> `KERN_AGENT_CLI` currently has nothing to point to.

The missing piece is named — `kern-agent`, ~200 lines of glue in `cmd/kern-agent/` — but not
written. So **today, out of the box, no real LLM runs inside a Kern graph**; what runs is the
deterministic `Stub` runner, which is also why the quickstart needs no configuration.

A home page saying "Kern runs AI agents as a team" would describe software that doesn't exist
yet. What does the wiki say?

# Options

- **Document only what runs today** — truthful, and Kern looks like an orchestrator with no AI
  in it, which undersells the design and contradicts the READMEs.
- **Document the intended architecture** — reads well, and gets a project called vaporware when
  a reader finds nothing to point `KERN_AGENT_CLI` at.
- **Both, with an explicit maturity layer** — what runs *and* what is intended, every page
  stating which side of the line it is on.

# Verdict

**Describe the target architecture — and build the structure first, fill it progressively,
with a placeholder system and no invented content.** The user's framing matters more than the
original options: the target architecture is not fully specified yet and I don't have the
context to describe it, so the deliverable is *the frame the documentation will live in*, not a
finished description of a system still being designed.

Four rules, and they become the wiki's core convention — the thing every contributor follows
([decision](/scope/12-mvp-cut.md)):

1. **Maturity marker on every page and every capability** — *works today* / *provisional* /
   *planned*. The four bricks are at different maturities; flattening that is the fastest way
   to lose a reader's trust.
2. **Placeholders are explicit and first-class.** A section that isn't documented yet says so —
   visibly, with what's missing and why — and is listed in the freshness table
   ([decision](/scope/16-freshness-and-versioning.md)). An empty marked slot is a valid, honest
   state for a page to be in.
3. **No false information. Ever.** A placeholder is never filled with plausible-sounding
   invented content, and nothing gets asserted that hasn't been checked against the code. This
   is the hard rule the whole approach rests on: a wiki that is 40 % filled and 100 % true is
   useful; one that is 100 % filled and 90 % true is worse than nothing, because the reader
   can't tell which 10 %.
4. **Planned ≠ described as existing.** The target architecture appears — `kern-agent`
   included — marked *planned*, with the gap drawn: a dashed edge in the ecosystem diagram, a
   quickstart that states its agent nodes are stubs, and a "what's missing" page listing the
   bridge and the pending protocol extensions.

That last page is useful content, not an apology: it is the highest-value contributor entry
point in the ecosystem (journey J4), and the compat analysis specifies it down to a suggested
`main()`.

Consequence accepted knowingly: the front door will read "promising, incomplete, honest about
which is which" rather than "ready". For a two-week-old ecosystem that is the accurate
description, and a reader who finds the docs accurate comes back.
