---
type: Decision
title: "Registries & generated tables"
description: "Are the contracts registry, freshness table and exposed/needs views hand-written, build-time templates, or committed generated markdown?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 06
slug: registries-and-tables
status: decided
verdict: "Committed generated markdown between markers on five surfaces, with regenerate-and-diff enforced in CI"
decided_via: triage
depends_on: [page-metadata, content-tree, okf-conformance]
---

# Question

Three M1 deliverables are aggregations of facts held elsewhere in the wiki: the **contracts
registry**, the **freshness table** (page → brick → version verified → date, placeholders
included), and the per-brick **exposed / needs** view
([decision](/scope/12-mvp-cut.md), [decision](/scope/09-contract-registry-home.md)).

Hand-maintained aggregations drift the moment a fourth page is added. But the obvious fix —
generate them at build time from templates — makes the tables invisible when the repo is read on
GitHub, breaking the fallback that [the markdown contract](/specs/03-markdown-contract.md)
exists to protect.

Scope's "no build-time generation" non-goal is about generating **from other repos' docs**
([decision](/scope/13-non-goals.md)); aggregating the wiki's own front matter is not that. Worth
stating so nobody reads the non-goal as forbidding this.

# Options

- **Hand-maintained tables** — honest, zero machinery, and guaranteed to be stale by M3 with
  several contributors filling pages in parallel.
- **Build-time only (Hugo template pages)** — always correct on the site; the source file is an
  empty stub on GitHub. Loses the fallback, and loses it precisely for the pages a maintainer
  most wants to skim in a PR diff.
- **Committed generated markdown** — a `tools/` command reads front matter across the tree and
  rewrites a table between `<!-- BEGIN GENERATED … -->` markers in a normal markdown page. The
  file is complete on GitHub, complete on the site, diffable in review, and CI fails if it is out
  of date (regenerate-and-diff).

# Recommendation

**Committed generated markdown, with CI enforcing freshness of the generation.**

Applies to five surfaces — the three aggregations, plus the two OKF listings that have exactly the
same drift problem ([decision](/specs/23-okf-conformance.md)):

| Surface | File | Source |
|---|---|---|
| Freshness table | `en/status/freshness.md` | every page's `verified` + `doc_state` |
| Contracts registry index | `en/contracts/_index.md` | contract pages' front matter |
| Exposed/needs matrix | `en/ecosystem/_index.md` | brick pages' `exposes` / `needs` |
| **OKF section listings** | every `_index.md` | sibling pages' `title` + `description` |
| **OKF bundle listing** | root `index.md` | section `_index.md` front matter |

Each is a hand-written page with prose, containing one generated block:

```markdown
<!-- BEGIN GENERATED: freshness -->
| Page | Brick | Verified | Date | State |
|---|---|---|---|---|
<!-- END GENERATED -->
```

Consequences worth accepting deliberately:

- **Contributors run one command** (`go run ./tools/gen`) or let CI tell them they forgot. The
  regenerate-and-diff check means a stale table is a red PR, not a discovered-in-six-months
  problem.
- **Contract *pages* stay hand-written.** Only the index is generated. Purpose, migration notes
  and enforcement status are prose that no aggregator can invent
  ([decision](/scope/09-contract-registry-home.md)).
- **The registry's authority is unchanged**: the `kern.*` JSON fixtures stay in their repos,
  CI-enforced there ([decision](/scope/06-source-of-truth.md)). The wiki aggregates its own pages'
  claims about contracts, not the contracts themselves.
- **Placeholders appear in the freshness table**, marked as such — that is what makes a
  half-empty wiki read as honest rather than unfinished.
- **Listings are generated, `log.md` is not.** A directory listing is derivable from front matter;
  a history entry is a judgement about what mattered. The log stays hand-written and is appended
  for structural changes only ([decision](/specs/23-okf-conformance.md)).

The one thing this does *not* do is verify claims against the bricks; that stays the M4 staleness
job's business ([decision](/specs/14-freshness-automation.md)) and, ultimately, the deferred
executed-quickstart.

# Verdict

**Committed generated markdown, CI-enforced**, accepted at triage. Five surfaces: freshness table,
contracts registry index, exposed/needs matrix, OKF section listings and the bundle listing.
Contract pages stay hand-written, `log.md` stays hand-written, and a stale generated block is a red
PR rather than a discovery months later.
