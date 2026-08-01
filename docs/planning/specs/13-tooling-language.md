---
type: Decision
title: "Repository tooling language"
description: "What language are the validator, the table generator and the staleness job written in?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 13
slug: tooling-language
status: decided
verdict: "Go, one binary in `tools/` with `validate` / `gen` / `stale`; OKF rules reimplemented rather than importing the Python reference checker"
decided_via: triage
depends_on: [site-generator]
---

# Question

Three pieces of custom tooling are implied by the decisions above: the OKF-conformance, front
matter and portability **validator** ([decision](/specs/23-okf-conformance.md)), the generated
listings and tables **generator** ([decision](/specs/06-registries-and-tables.md)), and the M4
**staleness job** ([decision](/specs/14-freshness-automation.md)). They need a language.

OKF ships a reference validator in Python. Adopting it would settle this decision by default —
and would put a Python toolchain in the repo for three conformance rules, while the generator and
the staleness job still need a home.

A documentation repo acquiring a programming toolchain deserves a moment's suspicion — but the
alternative is these rules living in prose, which the constraints already rejected.

# Options

- **Go** — the language every contributor already has (and which Hugo Modules require anyway,
  [decision](/specs/01-site-generator.md)). Single static binary, `go test` for the validator's
  rules, `actions/setup-go` in CI, YAML and the GitHub API both have first-class libraries. Cost:
  more ceremony than a script for the trivial parts.
- **Bash + `gh` + `yq`/`jq`** — no toolchain at all, and the standard way these jobs get written.
  Untestable in practice, and the validator is not trivial: it walks a tree, parses front matter,
  cross-references vocabularies and diffs generated blocks.
- **Node or Python** — best-in-class ecosystems for exactly this, and each imports a second
  runtime into a repo that otherwise needs none, for people who write Go.

# Recommendation

**Go, in `tools/`, as one binary with subcommands** (`validate`, `gen`, `stale`).

The deciding argument is not elegance, it is that this tooling encodes the project's rules and
therefore must be **testable** — the validator's job is to be right about criterion 1 (no false
information) in edge cases nobody will re-read by hand. `go test ./tools/...` gives that for free,
and Go is already installed on every contributor's machine.

Practical constraints to keep it from growing:

- **Standard library plus a YAML parser plus the GitHub API client.** No framework, no CLI
  library with a plugin system.
- **One binary, no build step for consumers**: `go run ./tools validate` works from a clean
  checkout; CI does the same. The wiki repo gets a `go.mod` and no vendored dependencies beyond
  those two.
- **Tooling failures never block reading the wiki.** Every check gates merges, not the site — if
  the validator breaks, pages still build and publish.

Bash is the honest runner-up and would be the right call for the staleness job alone. It loses
because the validator is the piece that matters, and an untested validator that silently stops
catching unstamped pages is worse than no validator: it converts an absent guarantee into a false
one.

# Verdict

**Go, one binary in `tools/` with `validate` / `gen` / `stale` subcommands**, accepted at triage.
Standard library plus a YAML parser and a GitHub API client, unit-tested, runnable from a clean
checkout with `go run`. Tooling failures gate merges, never the published site.

OKF's three conformance rules are reimplemented here rather than importing the Python reference
checker, which stays available for occasional out-of-band verification.
