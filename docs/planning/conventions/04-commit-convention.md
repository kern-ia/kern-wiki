---
type: Decision
title: "Commit convention for a content repository"
description: "Conventional commits are the baseline — but `docs:` on every commit in a docs repo carries no information."
tags: [decision, conventions]
timestamp: 2026-08-01T09:16:00Z
phase: conventions
decision: 4
slug: commit-convention
status: decided
verdict: "conventional types re-aimed at the wiki as the product, with a non-standard `content:` type; stamp changes named in the commit body"
decided_via: triage
depends_on: []
---

# Question

The baseline prescribes conventional commits (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`,
`test:`, imperative, no trailing period). In a repository whose product *is* documentation, the
type set collapses: nearly everything is arguably `docs:`, which makes the prefix pure ceremony.

# Options

- **Reinterpret the types against the wiki as the product** — `feat:` adds a page or a section,
  `fix:` corrects something wrong, `docs:` is reserved for the repo's own meta-documentation
  (README, contributing page). Keeps the vocabulary, changes what it points at.
- **Add a scope, keep the types literal** — `docs(bricks): …`, `feat(tools): …`. More typing,
  and the scope duplicates the path already visible in the diff.
- **Drop conventional commits** — nothing here consumes them: no semantic-release, no changelog
  generation (the scope's non-goals reject changelog aggregation).

# Recommendation

**Reinterpret the types against the wiki as the product**, with a scope only where the type is
ambiguous:

| Type | Means |
|---|---|
| `feat:` | a new page, section or contract entry; a new tooling capability |
| `fix:` | corrects something that was **wrong** — a false claim, a broken link, a bug in `tools/` |
| `content:` | fills or deepens an existing page without changing its structure |
| `chore:` | CI, dependencies, pins, layout shell |
| `refactor:` | moves or restructures without changing meaning — always paired with an alias ([decision](/specs/15-content-moves.md)) |
| `test:` | fixtures and tests under `tools/` |

`content:` is a non-standard type, added because the single most common commit in this repo —
*a placeholder became prose* — is neither a feature nor a fix, and hiding it under `docs:` would
make `git log` unreadable at exactly the moment the log is the only record of what was verified.

Scope is optional and used only to disambiguate: `feat(tools):` vs `feat(bricks):`.

The subject line stays imperative, no trailing period. **A commit that changes a page's
`verified` stamp says so in the body**, naming the version read — the stamp is the project's
central honesty mechanism ([decision](/conventions/12-stamping-and-done.md)) and its history
should be greppable.

# Verdict

**Types reinterpreted against the wiki as the product**, accepted at triage, with the six-type
table above and `content:` added for the repository's most common commit — a placeholder becoming
prose. Scope optional, used only to disambiguate `tools/` from content. Imperative subject, no
trailing period. A commit that changes a `verified` stamp names the version read in its body, so
the history of what was verified stays greppable.
