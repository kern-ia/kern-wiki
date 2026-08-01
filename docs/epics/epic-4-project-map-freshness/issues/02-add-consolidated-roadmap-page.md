---
type: Issue
title: "Add the consolidated roadmap page"
description: "Merge the per-repo roadmaps into one ordered view of what is coming across the ecosystem, reporting only what the repos themselves state."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/44
epic: 4
issue: 02
slug: add-consolidated-roadmap-page
size: M
status: open
gh_issue: 44
depends_on: []
---

# Add the consolidated roadmap page

## Summary

The other half of J5. The transverse status page says where each brick *is*;
this one says where each brick *says it is going*, in one place, so a maintainer stops opening N
repositories to answer that.

The hard constraint is the no-invented-content rule. A roadmap is the single easiest page on this
wiki to fill with plausible fiction — every entry here is something a repository actually wrote
down, or it is not on the page.

## Scope

- `en/status/roadmap.md`, typed against `data/vocab.yaml`.
- **One section per brick**, each listing what that repository states about its own next steps —
  from its roadmap file, its milestones, its open issues labelled as planned, or its README,
  whichever it actually maintains.
- **Each entry names its source and carries no date the repository did not itself give.** No
  estimates, no ordering the maintainers did not state, no "expected soon".
- **A brick with no published roadmap gets a section carrying the verbatim gap block**, naming that
  the repository publishes no roadmap. That is a true and useful fact; an empty section that looks
  identical to an unwritten one is not.
- Cross-ecosystem ordering only where a repository states a dependency itself — otherwise the page
  presents the bricks side by side and says nothing about sequencing.
- A link to [Issue 03](./03-add-open-architectural-questions.md)'s register, since the open
  questions are the part of the roadmap that belongs to no single repo.
- `# Citations` naming, per brick, the files read and at what version or date.

## Out of scope

- **No planning.** This page reports roadmaps; it does not create one, reconcile conflicts between
  two repos' plans, or propose an order. A contradiction between two repos is recorded as a
  contradiction, not resolved here.
- **No generated content** — same reasoning as [Issue 01](./01-add-transverse-status-page.md); the
  generated set is fixed at five and a roadmap is a judgement.
- **No issues opened on brick repos**, and no changes to any brick repository.
- **No blog or changelog aggregation** — deferred by the epic outright.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] Every brick has a section; a brick with no published roadmap carries a gap block naming that,
      rather than being omitted.
- [ ] Every entry traces to a source in `# Citations`. Nothing on the page was inferred from a
      brick's name, its issue titles, or what would be sensible.
- [ ] No date, estimate or ordering appears that the source repository did not itself state.
- [ ] Nothing hedges — no *may*, *should* or *probably* describing our own knowledge. Uncertainty is
      a gap block.
- [ ] `maturity` reflects the code, not the roadmap's ambition.
- [ ] Bricks are written lowercase and backticked; contracts carry their version.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet — paths follow the decided content tree, not verified locations:
`en/status/roadmap.md`, `en/status/_index.md`, `data/vocab.yaml`.

Sources: each brick repository's roadmap file, milestones and README, at the version you cite.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) for the `en/status/` section. Reads alongside
[Issue 01](./01-add-transverse-status-page.md) but does not depend on it — the two pages are
independent and can land in either order.

## PR size note

Target ~500 changed lines; one content page, well under it.
