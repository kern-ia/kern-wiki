# CONVENTIONS.md — kern-wiki

Local authority for this repo, as announced by the org-wide
[CONTRIBUTING.md](https://github.com/kern-ia/.github/blob/main/CONTRIBUTING.md). The rules
shared by all `kern-ia` repos are restated below; the "Specifics" sections cover what belongs
only to `kern-wiki`.

`kern-wiki` hosts the org's design and package documentation (the stated purpose in
`CONTRIBUTING.md`: "Design notes and package documentation live in the wiki"). Based on
in-progress commits (Epics 1 through 5), the repo is becoming a static Hugo site with its own
CI check suite — this document describes the target, not yet a stabilized state.

## Language

Code and comments (site tooling, build scripts, any future Hugo template logic) are written
in English — no exceptions. Internal documentation such as this file, `README.md`, or
`CLAUDE.md` stays in whatever language the team works in day to day. This does not decide the
language of the wiki's actual published content, which is a separate, content-level choice.

## Branches

- `main`: stable, published branch. Protected — no direct pushes.
- Working branches: `feature/<slug>`, `docs/<slug>`, or epic-named branches (already observed
  pattern: `epic-2-github-surface-resolved`) while the repo is under construction — converge
  toward `feature/epic-N-<slug>` once the structure stabilizes.
- Any change to `main` goes through a Pull Request — already respected (PR #60 in progress).

## Commits

Conventional Commits: `docs:` naturally dominates here (content = documentation), `feat:`/
`chore:` for site tooling (Hugo build, CI). No tool signature (`Co-Authored-By`,
`Claude-Session`, or equivalent trailer) in commit messages.

## Pull Requests

- One subject per PR, linked to the issue/epic it resolves.
- PR template inherited from `kern-ia/.github`.
- No semver concept applies to this repo (not a package) — the corresponding box in the PR
  template can be marked `none`.

## Content

- One page = one subject, linked to the epic or issue that produced it.
- Design decisions published here should link back to the originating RFC or issue rather
  than duplicate its content.
- No real personal data in screenshots, examples, or diagrams.

## CI

> **Current gap**: no GitHub Actions workflow exists yet on this repo, even though
> in-progress commits ("the CI check suite that makes criterion 1 a lint rule") announce its
> arrival as part of Epic 1. Add it before the page volume makes drift hard to catch up on.

## Documentation for the repo itself

- `README.md` to add if not already present at the root, describing how to build and serve
  the Hugo site locally.
- No `CLAUDE.md` today — to create if Claude Code sessions start working on this repo
  regularly (already the case based on the commit history).

## Security / privacy

See the org-inherited `SECURITY.md`. Nothing repo-specific beyond that: this repo doesn't
contain code that runs in production.
