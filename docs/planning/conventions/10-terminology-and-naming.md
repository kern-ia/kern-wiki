---
type: Decision
title: "Terminology & naming in prose"
description: "One vocabulary across writers and repos, when the repos themselves disagree on their own names."
tags: [decision, conventions]
timestamp: 2026-08-01T09:28:00Z
phase: conventions
decision: 10
slug: terminology-and-naming
status: decided
verdict: "the glossary is normative from M1; lowercase `kern-*` in prose, contracts always with their version, module paths verbatim; new terms land in the glossary in the same PR"
decided_via: triage
depends_on: [prose-style]
---

# Question

The baseline's naming section governs identifiers. The problem here is prose: the ecosystem's
vocabulary is defined in `Kern-Orch/docs/GLOSSAIRE.md`, is being consolidated into the wiki's
glossary at M1, and is currently used inconsistently across repos. Worse, the **names themselves
disagree** — `Kern-Orch` on GitHub, `kern-orch` in prose, `github.com/yoann/kern-orch` as a module
path, with a canonical-naming rule scheduled for M2
([decision](/scope/10-naming-and-identity.md)).

Two writers each resolving that per page produces exactly the inconsistency that is the project's
binding constraint.

# Options

- **Glossary is normative, one canonical spelling** — terms and names have one form in prose, and
  the real-world variants are recorded once in one place.
- **Per-page judgement** — each page uses whichever name fits its context. Cheapest today, and
  the reader can no longer tell whether `Kern-Orch` and `kern-orch` are one thing.
- **Defer to M2's naming rule** — but M1 writes twelve pages before M2 exists.

# Recommendation

**The glossary is normative, from M1, with one canonical spelling per thing.**

- **Bricks in prose: lowercase `kern-*`** — `kern-orch`, `kern-ui`, `kern-link`, `kern-anon` —
  in backticks. The repo's actual name is used **only** when the sentence is about the repository
  or a URL, and the M1 ecosystem page carries the mapping table once
  ([scope](/scope/10-naming-and-identity.md)).
- **Contracts are written exactly as their identifier**: `kern.run.v1`, in backticks, always with
  the version suffix. A contract without its version is not a contract.
- **Module paths are quoted verbatim as they exist today** — `github.com/yoann/kern-orch` — never
  normalized to what they ought to become. A `go get` line that doesn't work is a false claim
  ([scope](/scope/18-risks-and-assumptions.md)).
- **The ecosystem is "Kern"; the packages are "bricks"**, not modules, services or components.
  One word per concept, taken from the glossary.
- **First use of a glossary term on a page links to the glossary**; later uses don't.
- **A term not in the glossary gets added to the glossary in the same PR that first uses it** —
  the glossary is not a M1 deliverable that then freezes, it is where vocabulary accrues.
- Where the wiki's chosen term differs from a repo's, the glossary entry records the repo's term
  as an alias rather than correcting the repo — no changes to brick code is a non-goal, and
  contradicting a repo's own vocabulary violates criterion 5.

Enforcement is review plus one cheap mechanical rule worth having: the validator can flag
capitalized brick spellings (`Kern-Orch`) outside of link targets, code blocks and the mapping
table. Proposed as a **warning-level** check, since legitimate exceptions exist.

# Verdict

**The glossary is normative from M1, one canonical spelling per thing**, accepted at triage:
lowercase backticked `kern-*` in prose with the repo-name mapping table carried once on the
ecosystem page, contracts always written with their version suffix, module paths quoted verbatim
as they exist today, "Kern" for the ecosystem and "bricks" for the packages. First use on a page
links the glossary. A term not in the glossary is added to it in the PR that first uses it, and a
repo's differing term is recorded as an alias rather than corrected.

The capitalized-spelling check is adopted at **warning level**, since legitimate exceptions
exist.
