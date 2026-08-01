---
type: Issue
title: "Add the \"what's missing\" page"
description: "Frame the kern-agent bridge and the pending protocol extensions as the ecosystem's open work and a contributor entry point, not as an apology."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/22
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 17
slug: add-whats-missing-page
size: S
status: open
gh_issue: 22
depends_on: [13, 14]
---

# Add the "what's missing" page

## Summary

The epic's thirteen deliverables plus this one. The `kern-agent` bridge does not exist, and the
orch↔agent-CLI protocol has five planned extensions — this is the highest-value open work in the
ecosystem, so the page is written as somewhere to start contributing rather than as a list of
regrets.

## Scope

- `en/ecosystem/whats-missing.md` — for each gap: what is missing, what depends on it, what exists
  today in its place, and what would settle it.
- **The `kern-agent` bridge** — the reason no LLM runs in a graph today, matching the dashed edge in
  the diagram from [Issue 14](./14-add-ecosystem-diagram.md).
- **The five pending agent-protocol extensions**, recorded as **open questions rather than spec**.
  Documenting a protocol officially about to change is one of this epic's named risks; the mitigation
  is the provisional banner plus this framing.
- The provisional banner verbatim wherever the page describes the provisional orch↔agent-CLI seam.
- Each gap linked to the repository and issue where the work would land, where one exists — and
  marked as having no issue yet where it does not.

## Out of scope

- **No protocol specification.** Recording the extensions as open questions is the deliverable;
  writing the spec would freeze a provisional protocol by documentation, which the scope rejects
  outright.
- **No transverse roadmap and no consolidated open-architectural-questions page** — epic 4 owns
  those, including the `kern-contracts` extraction, the module-path migration and the `.github`
  cleanup. Do not pre-empt them; this page covers the `kern-agent` bridge and the protocol
  extensions.
- **No issues opened on the brick repos** from this PR.
- No estimate, no date, no promise.

## Acceptance criteria / Definition of done

- [ ] Every gap states what exists today in its place, so a reader is not left guessing whether
      something partial is available.
- [ ] The five protocol extensions are phrased as open questions; no field, message or flag is
      described as decided.
- [ ] Nothing is described from its name — anything named here was read, and is cited at a version.
- [ ] The provisional banner appears verbatim where the provisional seam is described, and
      `maturity: provisional` is set accordingly.
- [ ] The page reads as an entry point: a contributor can tell where to start.
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/ecosystem/whats-missing.md`, linked from
`en/ecosystem/_index.md` and the home page.

Sources: `Kern-Orch`'s agent-CLI protocol documentation and code at the version read; the brick
repositories' open issues.

## Dependencies

Blocked by [Issue 13](./13-write-home-and-ecosystem-overview.md) and
[Issue 14](./14-add-ecosystem-diagram.md) — the dashed edges and this page must agree.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
