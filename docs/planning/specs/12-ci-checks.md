---
type: Decision
title: "CI checks & testing infrastructure"
description: "What runs on a pull request, and what does it actually guarantee?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 12
slug: ci-checks
status: decided
verdict: "Build + OKF conformance + project validator + internal links on every PR from M1; external links and staleness on a schedule; no prose linter"
decided_via: triage
depends_on: [page-metadata, registries-and-tables, hosting-and-deployment, tooling-language, okf-conformance]
---

# Question

A documentation repo has no unit tests in the usual sense, but it has the same problem: the
project's stated constraint is that **consistency, not capacity, is binding**
([decision](/scope/15-constraints.md)), and the Kern repos' own principle is that *"drift is
caught by tests, not by discipline"* ([decision](/scope/16-freshness-and-versioning.md)).

So: which of the wiki's rules are machine-checkable, and which run when? This is what the TDD
loop of downstream implementation work will actually execute.

# Options

- **Build only** — the site compiles. Catches broken syntax and nothing about truthfulness.
- **Build + link checking** — adds dead links, internal and external. Standard practice; scope
  already puts a link checker in M4.
- **Build + links + a project-specific validator** — additionally enforces the front matter
  schema, the markdown portability contract, and the generated-table freshness. This is the only
  layer that checks the rules this project actually lives by.
- **Add prose linting (Vale) and generic markdown style (markdownlint)** — catches passive voice,
  heading style, line length. Real value, real noise, and a second toolchain for style rather
  than truth.

# Recommendation

**Build + links + a project-specific validator, from M1** — not M4. Three of these are checks on
rules M1 itself introduces; introducing the rules without the checks is how the three-different-
ways-of-writing failure happens before M2 can prevent it.

On every pull request:

| Check | Guarantees | Tooling |
|---|---|---|
| `hugo --gc --minify`, warnings fatal | the site builds; no missing translation targets, no broken render hooks | Hugo, pinned |
| **OKF conformance** | every concept doc has parseable frontmatter with a non-empty `type`; no reserved filename misused; `log.md` headings are `## YYYY-MM-DD` newest-first ([decision](/specs/23-okf-conformance.md)) | `tools/` |
| **Front matter validator** | the project profile on top of OKF: closed vocabularies, `placeholder` ⇏ `verified`, every technical page stamped, `resource` present where required | `tools/` ([decision](/specs/13-tooling-language.md)) |
| **Portability check** | no shortcodes, no MDX, no disallowed raw HTML ([decision](/specs/03-markdown-contract.md)) | same binary |
| **Generated tables up to date** | regenerate-and-diff on the three generated blocks ([decision](/specs/06-registries-and-tables.md)) | same binary |
| **Internal links** | every bundle-relative `/en/…md` target exists, on both trees and on both surfaces | link checker, internal only |

On a schedule (weekly), not on PRs:

| Check | Why not on PRs |
|---|---|
| **External links** | third-party rot is not the PR author's fault, and rate-limited checks make PRs flaky |
| **Staleness** | ([decision](/specs/14-freshness-automation.md)) — M4 |

Deliberately **not** in v1: Vale/markdownlint. Style consistency is served by templates and the
M2 "how to write here" checklist; adding a prose linter now buys arguments about comma usage in a
repo whose actual risk is asserting something untrue. Revisit if review comments start being
about style rather than substance.

OKF conformance is checked by our own Go binary rather than by the reference `validate_okf.py`:
three rules are cheap to implement, and adding a Python step to CI for them would reintroduce the
second toolchain that [the tooling decision](/specs/13-tooling-language.md) exists to avoid. The
reference checker stays useful for occasional out-of-band verification that our implementation
agrees with the spec.

The validator is the piece worth building well — it is the mechanical half of success criteria 1,
2 and 6. Its rules are testable in isolation, so it gets real unit tests even though the wiki
does not.

# Verdict

**Build + OKF conformance + project validator + internal links, from M1**, accepted at triage;
external link checking and the staleness job on a weekly schedule. Vale and markdownlint are
deliberately out of v1.

The M1 timing is the substantive part of this verdict: the rules the checks enforce are introduced
by M1 itself, and shipping them without enforcement is how the three-different-ways-of-writing
failure happens before M2's conventions page can prevent it.
