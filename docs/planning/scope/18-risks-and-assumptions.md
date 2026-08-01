---
type: Decision
title: "Risks & assumptions"
description: "What could sink this, and what is being assumed without proof?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 18
slug: risks-and-assumptions
status: decided
verdict: "Named risks with mitigations — revised: content drift replaces link rot as the dominant risk"
decided_via: triage
depends_on: [milestones, source-of-truth, freshness-and-versioning]
---

# Question

Which risks are worth writing down now, and which assumptions are load-bearing enough that
being wrong about them would change the plan?

# Options

- **Named risks with mitigations** — each risk paired with what absorbs it, and each
  assumption marked as verifiable or not.
- **Risk register with severity scores** — heavier ceremony than a solo pre-launch
  documentation project earns.
- **Skip** — discover them in epic 3.

# Recommendation

Named risks with mitigations.

# Verdict

**Named risks with mitigations**, accepted at triage. The list below is revised: the
self-contained verdict ([decision](/scope/06-source-of-truth.md)) moved the dominant risk
from *link rot* to *content drift*, and added two new ones (bilingual rot, missing
governance files).

Risks, worst first:

- **The wiki contradicts the repos.** Duplication is now accepted, against five
  weekly-moving upstreams — so the failure mode is no longer a dead link, it is a page
  that is confidently wrong. *Mitigation:* the ownership map (one authoritative home per
  subject), version stamps on every technical page, and the freshness table
  ([decision](/scope/16-freshness-and-versioning.md)).
- **Documenting moving packages produces churn.** The bricks are two weeks old;
  `Kern-UI/docs/a-trancher.md` shows design decisions still open. Writing usage docs now is
  a deliberate bet ([decision](/scope/07-coverage-depth.md)). *Mitigation:* stability
  banners, and the rule that these pages are not translated.
- **The wiki rots under solo maintenance.** The project knowingly bought a larger surface
  than the capacity constraint suggests ([decision](/scope/15-constraints.md)): hosted
  usage docs × 4 bricks + a second language. *Mitigation:* milestones are independently
  shippable, so stopping after M2 still leaves something coherent; French is last and
  scoped to stable pages.
- **The French half rots.** The classic bilingual outcome. *Mitigation:* English is the
  source language and no French page exists without an English original, so FR can lag
  without producing contradictions — it produces gaps, which are honest.
- **The quickstart breaks on a contract bump.** J2 spans two bricks coupled by
  `kern.step-event/v2`. *Mitigation:* version + date stamp on the page; the CI-executed
  quickstart is the real fix and is deferred.
- **The front door overpromises.** The READMEs describe Kern as running AI agents; today no
  LLM can run in a graph because the `kern-agent` bridge doesn't exist. Documenting the design
  without the gap is the fastest way to lose the first reader.
  *Mitigation:* [decision](/scope/20-documenting-the-gap.md) — maturity markers, a dashed
  edge in the diagram, an explicit "stubbed agents" note on the quickstart.
- **Documenting a protocol that is officially about to change.** The orch↔agent-CLI seam is
  marked provisional and has five planned extensions
  ([decision](/scope/09-contract-registry-home.md)). Writing it up risks freezing it by
  documentation, or being wrong within weeks. *Mitigation:* provisional banner, pending
  extensions listed as open questions rather than as spec.
- **Module paths are inconsistent in more than one direction.** `kern-link` declares
  `github.com/julienlegoux/kern-link`; `kern-orch` declares `github.com/yoann/kern-orch` —
  neither matches `kern-ia`, and they don't match each other. Any `go get` line written today
  is wrong or will be. *Mitigation:* document current paths verbatim, prefer linking each
  repo's own install snippet, flag the migration on the M4 open-questions page.
- **Undocumented operational traps that only surface in production.** The compat analysis
  names two the docs must carry: `kern-orch serve` under an empty service environment loses
  `HOME` and API keys, failing as silent in-band "no API key" errors; and kern-link's
  OAuth flows impersonate first-party clients, which its own docs warn gets accounts revoked
  when wired into a long-running daemon — so **API keys only for `serve`**. *Mitigation:*
  these are M2 content, not footnotes.
- **Contributors find no `CONTRIBUTING.md` where GitHub shows one** — `.github` is out of
  scope ([decision](/scope/08-governance-content.md)), so J4 is served by a site page that
  GitHub's own affordances won't surface. *Accepted*, revisited when that repo is cleaned up.
- **Scope drifts into brick work.** Writing usage docs across four young packages will
  surface bugs and API awkwardness. *Mitigation:* the "no brick code" non-goal; findings
  become issues on the brick.
- **Generator choice stalls content.** *Mitigation:* generator-agnostic markdown, so writing
  starts before `define-specs` picks one — but note the bilingual requirement narrows the
  field ([decision](/scope/03-delivery-form.md)).

Assumptions:

- The four bricks stay public, in the `kern-ia` org, under their current names for the
  duration of M1–M2. *(Verifiable, cheap to re-check.)*
- ~~One maintainer.~~ **Corrected: two contributors today, more expected**, and a fifth package
  already in progress. [decision](/scope/15-constraints.md) was reopened and re-based on this;
  the binding constraint became cross-contributor consistency rather than capacity.
- **The ecosystem will keep growing during this project.** A fifth package is in progress and
  its name, role and contracts are unknown to this plan. *(Certain, not assumed — which is why
  extensibility is a success criterion rather than a nice-to-have.)*
- **The target architecture is not fully specified.** Documented deliberately as *planned* with
  placeholders; the plan assumes it will settle incrementally rather than in one design pass.
  *(Unverified, and the reason no milestone promises a complete architecture description.)*
- **The `kern-orch` + `kern-ui` pairing works today on a clean machine.** The quickstart's
  whole premise, and unverified: it must be *run*, not read. First real task of M1.
- Each brick's public surface is stable enough that usage docs written now survive weeks,
  not days. *(Unverified, and the bet this project's size rests on. If wrong, M2 splits
  per brick and the least stable brick's section is postponed.)*
- `kern-link` stays a tracking port of `@earendil-works/pi-ai`, so its section documents
  usage and points upstream for design. *(Verifiable from `upstream-sync.yml`.)*
- No external users, no launch date, no compatibility obligation. *(If wrong, milestone
  order changes — notably French would move earlier.)*
- The bricks each carry a licence. *(Only `kern-link` advertises MIT; the audit that would
  have checked this is now out of scope, so this stays an open unknown rather than a
  verified fact.)*
