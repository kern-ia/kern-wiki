---
type: Decision
title: "Hosting & deployment pipeline"
description: "How does a merged change become a published page, and what does a PR author see before merging?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 11
slug: hosting-and-deployment
status: decided
verdict: "GitHub Actions building Hugo and deploying with actions/deploy-pages on main; every PR builds and uploads the site as an artifact"
decided_via: triage
depends_on: [site-generator, links-and-urls]
---

# Question

Scope fixed the destination — GitHub Pages on `kern-ia/kern-wiki`, publishing on push to the
default branch, zero budget ([decision](/scope/04-hosting-and-location.md),
[decision](/scope/12-mvp-cut.md)). What is left: the publishing *mechanism*, and whether
reviewers can see a change rendered before it goes live.

The second half matters more than it looks. Contributors write against templates and a
placeholder convention ([decision](/scope/12-mvp-cut.md)); if the only way to see a rendered page
is to merge it, review degrades to reading raw markdown — and uniformity, the M2 success
criterion, is judged on the rendered result.

# Options

- **Pages' native Jekyll build** — no workflow at all. Incompatible: Hugo, not Jekyll.
- **GitHub Actions → `actions/deploy-pages`** — the modern Pages flow: build the site as an
  artifact, deploy it via the Pages API. No build output committed to git, deployment history
  visible per run, environment protection available.
- **Actions → commit to a `gh-pages` branch** — the older `peaceiris`-style flow. Works
  everywhere, pollutes git history with generated files, and makes `git log` on the repo useless
  for tracking what humans actually wrote.
- **PR previews** — a real gap in the GitHub-native world: Pages serves one site. The zero-budget
  options are (a) build on every PR and upload the site as a downloadable artifact, (b) a second
  Pages-like host such as Netlify/Cloudflare previews — free tiers, but a non-GitHub dependency
  scope's constraint discourages.

# Recommendation

**GitHub Actions building Hugo and deploying with `actions/deploy-pages`, on push to `main`**,
plus **a build-and-upload-artifact job on every PR**.

- **`main` is the published site.** No release branches, no versioned trees
  ([decision](/scope/16-freshness-and-versioning.md)) — the published site is always the latest
  merged state.
- **Every PR builds the full site with warnings fatal** (`hugo --gc --minify` plus the checks in
  [CI](/specs/12-ci-checks.md)) and uploads the result as an artifact. A reviewer who wants to see
  a page rendered downloads it; more importantly, a PR that *breaks the build* cannot be merged
  and then discovered later.
- **The Hugo version is pinned** in the workflow, so "works on my machine" and "works in CI"
  cannot diverge silently.
- **No custom domain** ([decision](/scope/13-non-goals.md)) — `kern-ia.github.io/kern-wiki/`, and
  `baseURL` set to match ([decision](/specs/07-links-and-urls.md)).

Downloadable-artifact previews are frankly worse than a real preview URL. They are recommended
anyway because the alternative imports a third-party host into a project whose constraint is
GitHub-native and zero-budget, to serve two contributors. If the wiki later takes outside
contributions at volume, revisit — it changes no content, so it is a cheap reversal.

# Verdict

**Actions → `actions/deploy-pages` on `main`, plus build-and-upload-artifact on every PR**,
accepted at triage. No build output in git, no custom domain, Hugo version pinned, `baseURL` set to
the project-pages URL.

Artifact previews are accepted as the weaker option, chosen over importing a third-party preview
host into a zero-budget GitHub-native project for two contributors. Revisit if outside
contributions arrive at volume — it changes no content.
