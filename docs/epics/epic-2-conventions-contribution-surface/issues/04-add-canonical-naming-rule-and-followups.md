---
type: Issue
title: "Add the canonical naming rule page and open the per-repo naming follow-up issues"
description: "State the lowercase kern-* rule with today's real repo names noted where they differ, and open one issue per affected repository for the rename and module-path debt."
tags: [epic-2]
resource: https://github.com/kern-ia/kern-wiki/issues/33
timestamp: 2026-08-01T12:30:00Z
epic: 2
issue: 04
slug: add-canonical-naming-rule-and-followups
size: M
status: open
gh_issue: 33
depends_on: [01]
---

# Add the canonical naming rule page and open the per-repo naming follow-up issues

## Summary

Identity is inconsistent across the ecosystem, and a wiki puts every inconsistency on one page:
`kern-link` versus `Kern-Anon` versus `Kern-Orch` versus `Kern-UI`; `Kern-Anon`'s README titling
itself **PresidioGo**; Go module paths still reading `github.com/julienlegoux/kern-link` and
`github.com/yoann/kern-orch` after the move to the `kern-ia` org.

The scope decided **document only**: the wiki adopts lowercase `kern-*` as the canonical written
form, notes the real repo names wherever they differ so links and `go get` lines stay correct, and
**opens one issue per repository** for the rename and module-path work. The issues are this
deliverable — the renames are not, and stay owned by each repo.

The wiki surfaces the debt without taking it on.

## Scope

- `en/contributing/naming.md`:
  - The rule: **lowercase `kern-*` in prose, backticked**, matching Go convention and the existing
    `kern-link`.
  - When the real repository name is used instead: only when the sentence is about the repository
    itself, or in a URL or a link target.
  - **Module paths are quoted verbatim as they exist today** and never normalized to what they ought
    to become — a `go get` line that doesn't work is a false claim.
  - **Contracts** are written as their identifier, always with the version: `kern.run.v1`.
  - `Kern-Anon`'s **PresidioGo** identity gets one explicit sentence: it is a port, and the upstream
    name carries real information — it is not a naming mistake to be corrected silently.
  - A pointer to the canonical → real-name mapping table, which lives **once**, on the ecosystem
    page, and is not duplicated here.
  - A short "what to do when they disagree" rule for contributors, and a link to the follow-up
    issues below so the debt is visible from the rule that describes it.
- **One GitHub issue per affected repository**, opened on that repository, naming precisely: the
  current name, the canonical name, the module path as it reads today, the badge and CI references
  that point at the old owner, and the fact that a module-path change is breaking for importers.
  One issue per repo, not one umbrella issue.
- A table on the page linking each opened issue, so a maintainer can see the state of the debt from
  the wiki.

## Out of scope

- **No repo renames and no Go module-path migration** — the whole point of the *document only*
  decision. The follow-up issues are the deliverable; closing them is not.
- **No changes to brick code**, no PRs against brick repos, no badge fixes.
- **No edits to the ecosystem mapping table** beyond linking to it — the table is epic 1's, and
  duplicating it here would create the second source of truth this rule exists to prevent.
- **No renaming inside this wiki** of anything epic 1 already wrote — if epic 1's pages violate the
  rule, that is a `fix:` in its own PR.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] The canonical rule is stated once, unambiguously, and the page does not restate the mapping
      table it links.
- [ ] Every module path quoted on the page matches what the repository publishes **today**, checked
      against the repo rather than assumed.
- [ ] One issue exists per affected repository, each naming that repo's specific mismatches — not a
      generic body copied across four repos.
- [ ] Every opened issue is linked from the page, and every link resolves.
- [ ] `Kern-Anon`'s PresidioGo identity is explained rather than erased.
- [ ] Nothing on the page asserts what a repo contains without that having been checked and cited.
- [ ] `hugo` builds with warnings fatal; `validate` passes, including the capitalized-brick-spelling
      warning check, which this page will deliberately trip in its mapping references — confirm the
      exemption covers link targets, code blocks and the mapping table as designed.

## Relevant files / areas

No existing content for this yet — path follows the decided tree, not verified against this
repository: `en/contributing/naming.md`, linking `en/ecosystem/` for the mapping table.

External: the four brick repositories under `kern-ia` (plus wherever `kern-link` and `kern-orch`
currently publish their module paths from). Read each repo's README, `go.mod` and CI badges before
writing a line about it.

Sources: [scope decision 10](../../../planning/scope/10-naming-and-identity.md) and
[decision 19](../../../planning/scope/19-module-path-migration.md);
[CONVENTIONS.md](../../../planning/CONVENTIONS.md) §Terminology.

## Dependencies

Blocked by [Issue 01](./01-add-contributing-and-how-to-write.md).
Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md)'s ownership map and ecosystem pages (Issues 13 and
16), which host the mapping table this page points at.
Blocks [Issue 05](./05-add-brick-authoring-guide.md) — a new brick has to be named before it can be
declared.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. Note the
GitHub issues opened here are not part of the diff — the PR itself stays small.
