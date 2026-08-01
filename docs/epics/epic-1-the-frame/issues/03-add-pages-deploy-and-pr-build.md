---
type: Issue
title: "Add the GitHub Pages deploy and pull request build workflows"
description: "Publish the site to GitHub Pages on push to main, and build the full site as a fatal-warning artifact check on every pull request."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/8
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 03
slug: add-pages-deploy-and-pr-build
size: S
status: open
gh_issue: 8
depends_on: [01, 02]
---

# Add the GitHub Pages deploy and pull request build workflows

## Summary

Deliverable 2 of the epic: publishing on push to the default branch. Plus the pull request side of
it — every PR builds the full site with warnings fatal and uploads it as an artifact, which is the
accepted-as-weaker substitute for a preview URL in a zero-budget, GitHub-native project.

## Scope

- `.github/workflows/deploy.yml` — on push to `main`: build with the pinned Hugo, deploy with
  `actions/deploy-pages`. No build output committed to git.
- `.github/workflows/ci.yml` — on pull request: `hugo --gc --minify` with warnings fatal, uploading
  the built site as an artifact. This workflow is the file every later check issue adds a job to.
- Least-privilege permissions **per job**, `GITHUB_TOKEN` only — no PAT, no repository secrets.
- All actions pinned, and Dependabot configured to watch them (`.github/dependabot.yml`).
- Repository settings noted in the PR description: Pages source set to GitHub Actions, `main`
  protected (no force-push, no direct push, CI green required).

## Out of scope

- **No validator, portability, link, generated-block or stamp-coverage jobs** — each check issue
  adds its own job to `ci.yml`.
- **No weekly workflows** — external link checking and the staleness job are epic 4.
- **No executed-quickstart job** — explicitly deferred past epic 4.
- No preview-URL host; the artifact is the decided trade.

## Acceptance criteria / Definition of done

- [ ] A push to `main` publishes to `https://kern-ia.github.io/kern-wiki/` and the home page loads.
- [ ] A pull request runs the build, and a Hugo warning fails it.
- [ ] Each job declares its own `permissions` block; none grants more than it needs.
- [ ] No secret beyond `GITHUB_TOKEN` is referenced.
- [ ] Every action is pinned and covered by Dependabot.
- [ ] The built site is downloadable from the PR as an artifact.

## Relevant files / areas

No existing code for this yet — `.github/workflows/` is created empty by
[Issue 01](./01-initialize-repo-and-okf-bundle-root.md). Files:
`.github/workflows/deploy.yml`, `.github/workflows/ci.yml`, `.github/dependabot.yml`.

## Dependencies

Blocked by [Issue 01](./01-initialize-repo-and-okf-bundle-root.md) and
[Issue 02](./02-add-hugo-site-and-link-render-hook.md).
Blocks every check issue ([Issue 05](./05-scaffold-tools-and-okf-conformance.md) onward), which
extend `ci.yml`.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
