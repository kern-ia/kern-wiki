---
type: Decision
title: "Citations discipline"
description: "SPECS mandates a `# Citations` section on technical pages; what counts as a citation is undecided."
tags: [decision, conventions]
timestamp: 2026-08-01T09:30:00Z
phase: conventions
decision: 11
slug: citations-discipline
status: decided
verdict: "a citation is a path at a version, grouped by brick; a bare repository link cites nothing; cited versions must match `verified.version`"
decided_via: triage
depends_on: [prose-style]
---

# Question

Technical pages end with `# Citations` naming what was actually read
([decision](/specs/03-markdown-contract.md)). The validator can check the section *exists*. It
cannot check that a link to `github.com/yoann/kern-orch` — the repository home page — represents
anything anyone read.

An unenforceable section that everyone fills with a repo link is worse than no section: it looks
like evidence.

# Options

- **Anything cited is fine** — the section becomes a "see also" list and stops meaning anything.
- **Citations name file and version** — a citation is a specific path at a specific tag or commit,
  which is checkable by a human in seconds and partially checkable by machine.
- **Citations are permalinks to a commit SHA** — maximally precise, unreadable, and rots visibly
  the moment a file moves.

# Recommendation

**A citation is a path at a version, in one shape:**

```
# Citations

- `kern-orch` v0.2.0 — `internal/graph/checkpoint.go`, `docs/GLOSSAIRE.md`
- `kern-link` v0.1.1 — `README.md`, `providers/anthropic/client.go`
- `kern-orch-kern-link-compat.md` (external analysis, 2026-07-28)
```

Rules:

- **Grouped by brick and version**, because the version is what the `verified` stamp claims and
  the two must agree ([decision](/conventions/12-stamping-and-done.md)).
- **Paths, not repository homes.** A bare repo link cites nothing. If the whole of a short README
  was read, cite `README.md` — that is a path.
- **What was *read*, not what supports the claim in retrospect.** This is the difference between
  a citation list and a bibliography, and it is the point: the section's real audience is the
  next person verifying the page, who needs to know where to look, and the staleness job's human
  reader, who needs to know what to re-read.
- **Non-repository sources are cited too** — the compatibility analysis, an upstream project's
  docs, an issue thread — with a date, since they have no version.
- **A page with no citations has nothing verified in it**, which means it is a placeholder, and
  the validator's `placeholder ⇏ verified` rule already says so. The two checks are the same
  claim from two directions.

Mechanically checkable, and worth adding: every line begins with a backticked identifier, and
every version mentioned in `# Citations` matches `verified.version` where the front matter
carries one. That catches the common failure — a page stamped v0.2.0 whose citations were taken
from v0.1.

# Verdict

**A citation is a path at a version**, accepted at triage, in the shape shown above: grouped by
brick and version, paths rather than repository homes, what was actually *read* rather than what
supports the claim in retrospect, and non-repository sources cited with a date. The mechanical
check is adopted — every line begins with a backticked identifier, and versions named in
`# Citations` must match `verified.version` where the page carries one.
