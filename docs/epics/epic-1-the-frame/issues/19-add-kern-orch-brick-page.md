---
type: Issue
title: "Add the kern-orch brick page"
description: "Instantiate the brick template for kern-orch — filled where verifiable against the code, gap-blocked everywhere else, with the provisional agent-CLI seam banner-marked."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/24
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 19
slug: add-kern-orch-brick-page
size: S
status: open
gh_issue: 24
depends_on: [04, 13, 18]
---

# Add the kern-orch brick page

## Summary

The graph orchestrator, and half of the quickstart's premise. It is also the brick that touches the
provisional orch↔agent-CLI protocol, so this page is where the provisional banner earns its
existence: the content is correct, verified and useful, with nothing in the page's structure
otherwise signalling that it can break.

## Scope

- `en/bricks/kern-orch.md`, from `templates/brick.md`, every section filled or gap-blocked.
- The **exposed / needs** declaration — what `kern-orch` exposes and what it needs, with contract
  identifiers written with their versions.
- **The provisional banner**, verbatim, wherever the agent-CLI seam is described, with
  `maturity` set to match.
- Module path quoted verbatim as it exists today (`github.com/yoann/kern-orch`).
- The stub reality stated where it is relevant: agent nodes execute deterministic stubs, not model
  calls, because the `kern-agent` bridge does not exist.
- `# Citations` as paths at a version.

## Out of scope

- **No depth** — epic 3 fills the technical sections.
- **No protocol specification.** The five pending extensions are open questions on
  [Issue 17](./17-add-whats-missing-page.md)'s page, not spec here.
- **No re-hosting of `Kern-Orch`'s architecture notes, dev logs or glossary** — the glossary's
  vocabulary is [Issue 15](./15-add-glossary.md)'s; everything else stays in the repo.
- **No changes to `kern-orch`.**
- No licence claim.

## Acceptance criteria / Definition of done

- [ ] Every heading required for `type: Brick` is present, in order, none deleted.
- [ ] Every filled statement was checked against `kern-orch`'s code at a named version, cited by
      path.
- [ ] The provisional banner appears verbatim if and only if `maturity: provisional`.
- [ ] Every contract named carries its version.
- [ ] Every unfilled section carries a gap block naming what is missing, with no guess.
- [ ] Commands are copy-pasteable, use today's module path, and are stamped only if run.
- [ ] The page contradicts nothing in `Kern-Orch`'s own docs (criterion 5).
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/bricks/kern-orch.md`, from `templates/brick.md`.

Source: `github.com/yoann/kern-orch` at the tag or commit you cite, including its `docs/`.

## Dependencies

Blocked by [Issue 04](./04-add-page-templates-and-vocabulary.md),
[Issue 13](./13-write-home-and-ecosystem-overview.md) and
[Issue 18](./18-add-kern-link-brick-page.md) (template shape settles there).
Blocks [Issue 23](./23-write-verified-quickstart.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. A content page
is never split across two PRs.
