---
type: Issue
title: "Add the citation and terminology checks"
description: "Enforce the citation shape and its agreement with the version stamp, and warn on capitalized brick spellings outside their allowed contexts."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/14
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 09
slug: add-citation-and-terminology-checks
size: M
status: open
gh_issue: 14
depends_on: [06]
---

# Add the citation and terminology checks

## Summary

A citation is a path at a version, and the version is what the stamp claims — so a page stamped
`v0.2.0` whose citations were taken from `v0.1` is a page nobody actually verified. This check
catches exactly that. The terminology half enforces one canonical spelling per thing, at warning
level, because the glossary is normative from this milestone.

## Scope

**Citation check** — on every page carrying a `# Citations` section:

- every line begins with a backticked identifier — a brick or a non-repository source;
- entries are grouped by brick and version, and name **paths**, not repository homes; a bare repo
  link is an error;
- non-repository sources carry a date;
- **versions named in citations match `verified.version`** where the page carries a stamp;
- a page whose `type` `vocab.yaml` marks as technical has a `# Citations` section at all.

**Terminology check** — at **warning** level, per conventions:

- capitalized brick spellings (`Kern-Orch`, `Kern-UI`, …) outside link targets, code blocks and the
  ecosystem page's repository-name mapping table;
- contract identifiers written without their version (`kern.run` rather than `kern.run.v1`) — a
  contract without its version is not a contract.

Fixtures first, and warnings must be distinguishable from errors in both the exit code and the
output.

## Out of scope

- **No glossary-term coverage check** — "a term not in the glossary is added in the PR that first
  uses it" has no fixture anyone can write; it stays a checklist item, and the PR should say so.
- **No check that a citation was actually read.** Nothing mechanical can establish that; the stamp
  and review carry it.
- **No French glossary column checks** — epic 5.
- No auto-formatting of citation blocks.

## Acceptance criteria / Definition of done

- [ ] A citation naming only a repository home fails; one naming `brick vX — path` passes.
- [ ] A page stamped at one version citing another fails, with both versions in the message.
- [ ] A capitalized brick spelling in prose warns; the same spelling inside a code block, a link
      target or the mapping table does not.
- [ ] A warning does not fail the build; an error does.
- [ ] Every rule has a fixture, red before green.
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (rule package), `tools/testdata/`. The allowed
contexts for capitalized spellings depend on the ecosystem page's mapping table from
[Issue 13](./13-write-home-and-ecosystem-overview.md) — key the exemption off the page, not off a
hard-coded path, if that page does not exist yet at merge time.

## Dependencies

Blocked by [Issue 06](./06-add-front-matter-validator.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
