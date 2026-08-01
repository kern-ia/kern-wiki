---
type: Issue
title: "Add the transverse status page"
description: "One hand-written page showing, per brick, where its repository actually stands — release, activity, maturity and documentation state — with everything unknown marked as unknown."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/43
epic: 4
issue: 01
slug: add-transverse-status-page
size: M
status: open
gh_issue: 43
depends_on: []
---

# Add the transverse status page

## Summary

Maintainers have N roadmaps across repos that each move weekly, and no transverse view — journey
**J5**. This is the page that answers *where does the project stand* in one screen, and it is the
page the epic's single acceptance criterion is about: it has to be good enough that someone actually
picks their next task from it.

It is deliberately the first issue of the epic. The link checker and the staleness job protect the
wiki; this page is the thing a human opens.

## Scope

- `en/status/_index.md` gains this page beneath it as `en/status/status.md` (name it against the
  section shape epic 1 landed — one page, one file), typed against `data/vocab.yaml`.
- **One row per brick**, hand-written, covering at minimum: brick, repository (module path verbatim
  as it exists today), latest release, `maturity`, `doc_state`, and licence.
- **Everything the repos do not say is written as unknown**, not inferred. The licence column is the
  named case: only `kern-link` advertises MIT and the licence audit is out of scope, so every other
  cell reads *unknown* rather than *presumably MIT*.
- Prose above the table stating what the page is for, how often it is refreshed, and — explicitly —
  that it is hand-maintained rather than generated, so a stale row is a PR and not a bug report.
- `# Citations` naming, per brick, the repository paths actually read to fill its row, at a version.

## Out of scope

- **This is not a sixth generated surface.** SPECS fixes the generated set at five — freshness
  table, contracts registry index, exposed/needs matrix, section listings, bundle listing
  ([decision](/specs/06-registries-and-tables.md)). Do not add generator support, do not add
  `<!-- BEGIN GENERATED -->` markers, and do not extend `gen`. A judgement is not derivable, and
  this page is judgement.
- **No freshness table here** — epic 1 issue 24 owns `en/status/freshness.md`. This page links to it
  and does not restate a single row.
- **No consolidated roadmap** — [Issue 02](./02-add-consolidated-roadmap-page.md).
- **No open architectural questions register** — [Issue 03](./03-add-open-architectural-questions.md).
- **No licence audit.** Recording *unknown* is the deliverable; going and determining each brick's
  licence is not this issue and not this epic.
- **No changes to any brick repository**, and no issues opened on them from this PR.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] The page exists under `en/status/`, is reachable from the status section listing, and its
      `type` is in `data/vocab.yaml` (extended in this PR if it is not).
- [ ] Every brick documented in the wiki has a row; a brick with nothing known still has a row, with
      unknown cells, rather than being absent.
- [ ] No cell is inferred. Every non-unknown cell traces to something in `# Citations`.
- [ ] Licences are listed as unknown wherever they are unknown, with the single known case named.
- [ ] Module paths are quoted verbatim as they exist today, never normalized to what they ought to
      become.
- [ ] The page states in prose that it is hand-maintained, and how a wrong row gets fixed.
- [ ] Any section with nothing true to say keeps its heading and carries the verbatim gap block.
- [ ] `# Citations` are grouped by brick and version, and versions match `verified.version`.
- [ ] `hugo --gc --minify` builds with warnings fatal; `validate` passes; hard-wrapped at 100
      columns.

## Relevant files / areas

No `en/` tree exists in this repository yet — the paths below follow the decided content tree
([specs](/specs/04-content-tree.md)) and epic 1's output, and are not verified locations:
`en/status/status.md`, `en/status/_index.md`, `data/vocab.yaml`.

Sources to read: each brick's repository — `github.com/julienlegoux/kern-link`,
`github.com/yoann/kern-orch`, and the `kern-ui` and `kern-anon` repositories at whatever paths they
actually carry — their releases, their READMEs, and their licence files where present.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md), which creates `en/status/` and the vocabulary this
page's `type` comes from. Feeds [Issue 08](./08-verify-status-page-picks-next-task.md), which is the
acceptance check on this page.

## PR size note

Target ~500 changed lines; one content page plus a possible vocabulary entry, comfortably under it.
A content page is never split across two PRs.
