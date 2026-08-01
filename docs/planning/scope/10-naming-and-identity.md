---
type: Decision
title: "Naming & identity consistency"
description: "Does this project fix the inconsistent brick names, or only document the canonical ones?"
tags: [decision, scope]
timestamp: 2026-07-30T05:03:34Z
phase: scope
decision: 10
slug: naming-and-identity
status: decided
verdict: "Document canonical lowercase kern-* only; renames and module paths stay with each repo"
decided_via: triage
depends_on: [delivery-form]
---

# Question

Identity is currently inconsistent, and a wiki makes every inconsistency visible on one
page:

- Casing: `kern-link` vs `Kern-Anon` vs `Kern-Orch` vs `Kern-UI`.
- `Kern-Anon`'s README titles itself **PresidioGo**, not Kern-Anon.
- Go module paths still read `github.com/julienlegoux/kern-link` after the move to the
  `kern-ia` org, so published install instructions and the org URL disagree.
- `kern-link`'s CI badges still point at `julienlegoux/kern-link`.

# Options

- **Document only** — the wiki states a canonical naming rule, uses it consistently, and
  files a follow-up issue per repo for the mismatches. Fixes the reader's experience now;
  the repos stay inconsistent until each is touched.
- **Document and fix** — this project also renames repos and migrates module paths.
  Renaming a Go module is a breaking change for importers and touches every file with an
  import path, plus badges, CI, and `pkg.go.dev`. That is brick work, not wiki work.
- **Ignore** — use whatever each repo calls itself. Cheapest, and it makes the front
  door look like four unrelated projects, which is the exact problem being solved.

# Recommendation

**Document only.** Adopt lowercase `kern-*` as the canonical written form (matching Go
convention and the existing `kern-link`), use it everywhere in the wiki, and note the
actual repo names where they differ so links stay correct. Open one issue per affected
repo for the rename/module-path work and link them from the maintainer milestone — the
wiki surfaces the debt without taking it on. `Kern-Anon`'s "PresidioGo" identity deserves
one explicit sentence rather than a silent rename: it is a port, and the upstream name
carries real information.

# Verdict

**Document only**, accepted at triage: canonical written form is lowercase `kern-*`, real
repo names noted wherever they differ so links stay correct, one follow-up issue per repo
for the mismatches. `Kern-Anon`'s "PresidioGo" identity gets an explicit sentence rather
than a silent rename.
