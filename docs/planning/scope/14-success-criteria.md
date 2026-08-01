---
type: Decision
title: "Success criteria"
description: "How do we know v1 worked?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 14
slug: success-criteria
status: decided
verdict: "Ten walkability + integrity criteria, based on truthfulness, extensibility and uniformity — never coverage"
decided_via: triage
depends_on: [target-audiences, mvp-cut]
---

# Question

With no users yet, adoption metrics would be theatre. What is actually checkable?

**Refreshed twice.** "Zero duplicated prose" died with link-never-copy. And now that v1 is a
*frame* rather than a set of finished pages ([decision](/scope/12-mvp-cut.md)), criteria based
on completeness would be wrong too: a partly-placeholdered wiki is the intended v1 state, so
success has to be measured on **truthfulness, extensibility and uniformity** instead of coverage.

# Options

- **Adoption metrics** — stars, traffic, contributors. Measure Kern's appeal, not the wiki's
  quality, and can't be checked at ship time.
- **Coverage metrics** — pages written, sections filled. Directly contradicts structure-first:
  it would reward filling placeholders with invented content, the one thing forbidden.
- **Walkability + integrity tests** — each journey walkable using only the wiki, plus checks on
  the properties the frame is supposed to have.

# Recommendation

**Walkability + integrity tests**, each pass/fail, tagged with the milestone that makes it
checkable:

1. **M1 — No false information.** Every unfilled area is an explicit marked placeholder, and no
   page asserts anything not verified against the code. Auditable page by page, and it is the
   one criterion that must never be traded away ([decision](/scope/20-documenting-the-gap.md)).
2. **M1 — Extensibility.** Adding a new brick or a new contract is filling a template slot, not
   redesigning navigation. Tested for real by the fifth package when it lands — if that requires
   restructuring, the frame failed.
3. **M1 — Honest maturity.** A reader can tell, per brick and per capability, what runs today
   from what is planned; nobody can mistake `kern-agent` for something that exists.
4. **M1 — Under 15 minutes** from the site to a running `kern-orch` + `kern-ui` hello graph,
   using only the wiki, with the stubbed agents clearly stated. *(J2 — worth testing on an
   actual second person.)*
5. **M1 — Ownership respected.** Every subject has exactly one authoritative home per the
   ownership map, and no wiki page contradicts the repo docs on the same subject.
6. **M2 — Uniformity.** The other contributor adds or fills a page that matches the templates and
   markers **without asking how** — the real test of the conventions, and the reason M2 comes
   before the bulk writing.
7. **M3 — Adoption of one brick.** A developer installs, configures and successfully uses a
   single brick in their own Go project from its wiki section alone. *(J6)*
8. **M3 — Every technical page carries its version stamp** (brick + commit/tag + date verified).
   Mechanically checkable.
9. **M4 — You use the transverse status page** — not five `ROADMAP` files — to pick a next task
   at least once. *(J5; a usage test, because an internal page nobody opens is dead weight.)*
10. **M5 — Every French page has an English original and says the same thing.** Gaps are
    acceptable; contradictions are not.

Adoption metrics are worth watching but are explicitly **not** criteria: they would make the
wiki accountable for Kern's popularity.

# Verdict

**The ten criteria above**, accepted at re-triage. Coverage is explicitly excluded as a measure:
it would reward filling placeholders, which is the one thing forbidden
([decision](/scope/20-documenting-the-gap.md)). The two load-bearing criteria are #1 (no false
information) and #2 (adding the fifth package must be a filled slot, not a navigation redesign) —
the second gets tested for real, by that package, whether or not the frame is ready for it.
