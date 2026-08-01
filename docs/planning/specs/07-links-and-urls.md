---
type: Decision
title: "Links, URLs & permalinks"
description: "How are internal links written so they work on GitHub and on the site, and what URL shape do pages get?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 07
slug: links-and-urls
status: decided
verdict: "Bundle-relative `/en/…md` links resolved by a custom link render hook; URLs are `/{lang}/{section}/{page}/`"
decided_via: triage
depends_on: [site-generator, content-tree, markdown-contract, okf-conformance]
---

# Question

Now three surfaces, one link syntax: the GitHub file browser, the built site, and OKF's own link
semantics ([decision](/specs/23-okf-conformance.md)). A link that satisfies one has historically
broken another:

- `../bricks/kern-orch.md` — works on GitHub, allowed by OKF (§5.2) but not its preferred form,
  and fragile when a page moves.
- `/en/bricks/kern-orch.md` — OKF's **recommended** form (bundle-relative, survives moves), and
  correct on GitHub too, since GitHub resolves `/`-prefixed links against the repository root —
  which is the bundle root ([decision](/specs/23-okf-conformance.md)).
- `{{< relref >}}` — Hugo's traditional answer, and a shortcode, which the portability contract
  forbids ([decision](/specs/03-markdown-contract.md)).

Compounding it: a GitHub Pages **project** site is served from a subpath
(`https://kern-ia.github.io/kern-wiki/`), so any hand-written site path is wrong in production and
right in `hugo server` — the worst kind of bug.

URLs are a one-way door in the ordinary sense: once the wiki is linked from four READMEs, changing
them breaks other people's links.

# Options

- **Bundle-relative `/en/…` links + a custom link render hook** — one form, correct on GitHub and
  preferred by OKF. Hugo's *embedded* hook cannot resolve it: for the English language,
  `contentDir` is `en/`, so `/en/bricks/x.md` would resolve as `en/en/bricks/x.md`. A custom
  `layouts/_markup/render-link.html` that strips the leading language segment and resolves via
  `.GetPage` is roughly ten lines.
- **Relative `.md` links + Hugo's embedded hook** — zero custom templating, and demotes OKF's
  recommended link form to its tolerated one, in a bundle whose whole point is being idiomatic.
  Also worse across sections: `../../ecosystem/glossary.md` is a link nobody verifies by eye.
- **Absolute site paths** (`/bricks/kern-orch/`) — correct on the site, dead on GitHub, and
  subpath-fragile.
- **Full URLs to the published site** — works from anywhere including other repos; makes every
  internal link a network round trip, breaks on PR previews, and makes a domain change a
  repo-wide sed.

# Recommendation

**Bundle-relative `/en/…` links everywhere internally, resolved by a custom link render hook.**

The hook is the only custom Hugo templating this project takes on, and it earns its place: it
collapses three link conventions into one, and the ten lines live in `layouts/` where CI exercises
them on every build. Both surfaces are checked ([decision](/specs/12-ci-checks.md)) — the file
target must exist *and* the built site must have no broken link.

URL shape:

- **`/{lang}/{section}/{page}/`** — language in the path for both languages, including English, so
  the URL mirrors the content tree one-to-one and a concept ID maps to a URL by inspection. A
  site root that redirects to `/en/` costs one line and avoids the migration where English pages
  move under `/en/` when French arrives at M5 — exactly the file-moving scope forbade
  ([decision](/scope/12-mvp-cut.md)).
- **`baseURL` set to the full project-pages URL**, never a bare `/`. Relative link resolution and
  the search index both depend on it.
- **Lowercase kebab-case filenames**, matching the canonical `kern-*` naming rule
  ([decision](/scope/10-naming-and-identity.md)) — so `en/bricks/kern-orch.md` even though the
  repo is currently `Kern-Orch`. The page says what the real repo name is; the URL says what the
  name will be.
- **Cross-language links are explicit** (`/fr/…` from a French page), which the hook resolves the
  same way — no implicit "current language" magic that would break the moment a French page links
  to an untranslated English one ([decision](/specs/09-bilingual-mechanism.md)).

Links **out** to the brick repos and `pkg.go.dev` are full URLs, unavoidably. They are also the
main thing that rots, which is why the link checker runs on a schedule and not only on PRs.

# Verdict

**Bundle-relative `/en/…md` links, resolved by a custom link render hook**, accepted at triage.
URLs are `/{lang}/{section}/{page}/` with the language present for both languages, `baseURL` is the
full project-pages URL, and filenames are lowercase kebab-case on the canonical `kern-*` names.

The custom hook in `layouts/_markup/render-link.html` is the project's only bespoke Hugo
templating, accepted because it collapses three link conventions into one and is exercised by every
CI build.
