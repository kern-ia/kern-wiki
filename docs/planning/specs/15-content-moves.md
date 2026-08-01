---
type: Decision
title: "Content moves & redirects"
description: "When a page moves or is renamed, how do existing links survive?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 15
slug: content-moves
status: decided
verdict: "Hugo `aliases` in front matter, kept permanently; a rename without an alias fails CI"
decided_via: triage
depends_on: [links-and-urls, content-tree]
---

# Question

The checklist's "data migrations" slot, in a project whose data is pages: once the wiki is linked
from four brick READMEs, from issues, and eventually from the org profile, **a URL is an external
contract**. And moves are certain, not hypothetical — the naming rule already anticipates
`Kern-Orch` → `kern-orch` ([decision](/scope/10-naming-and-identity.md)), and a brick that
outgrows one page becomes a directory ([decision](/specs/04-content-tree.md)).

# Options

- **Nothing** — moved pages 404. Cheap, and each 404 is a reader who concludes the wiki is
  unmaintained; on a documentation site that is the whole product.
- **Hugo `aliases`** — the moved page's front matter lists its old paths; Hugo emits a redirect
  stub at each. Native, no infrastructure, visible in the page's own front matter so a reviewer
  sees the history.
- **A central redirects file** — one map of old → new. Easier to audit in bulk, and detached from
  the page it describes, so it rots independently.

# Recommendation

**Hugo `aliases` in front matter, permanently kept.**

```yaml
aliases: ["/en/bricks/Kern-Orch/"]
```

- **Aliases are never removed.** They cost a stub file each. Removing one buys nothing and breaks
  a link somebody wrote down.
- **A rename PR that adds no alias fails the validator** ([decision](/specs/12-ci-checks.md)) —
  git tells the tooling a file moved, so this is checkable rather than remembered.
- **Bundle-relative links inside the wiki are updated at rename time**, not aliased. Aliases are
  for the outside world; internal links have a checker that will fail on the dangling target
  anyway ([decision](/specs/07-links-and-urls.md)).
- **A move changes the page's OKF concept ID**, since the ID is its path
  ([decision](/specs/23-okf-conformance.md)). Nothing in the bundle depends on IDs being stable —
  links are checked, not resolved by memory — but it is why the alias, which preserves the *URL*,
  is not also preserving the identity, and why moves stay rare rather than free.

GitHub's own file browser is the one surface aliases cannot help — a moved file is just moved.
That is acceptable: the fallback exists for readers of the repo, who have `git log`, not for
inbound links.

# Verdict

**Hugo `aliases`, kept permanently**, accepted at triage. Aliases are never removed, a rename PR
without one fails the validator, and internal links are rewritten at rename time rather than
relying on the alias. The anticipated first use is the `Kern-Orch` → `kern-orch` naming
normalisation.
