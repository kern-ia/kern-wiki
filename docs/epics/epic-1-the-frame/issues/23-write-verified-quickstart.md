---
type: Issue
title: "Write the end-to-end quickstart, verified by running it"
description: "Run kern-orch executing a hello graph with kern-ui live in a browser on a clean machine, then write the quickstart from what actually happened."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/28
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 23
slug: write-verified-quickstart
size: M
status: open
gh_issue: 28
depends_on: [19, 20, 22]
---

# Write the end-to-end quickstart, verified by running it

## Summary

Deliverable 10, journey J2, and acceptance criterion 4 — under 15 minutes from landing on the site
to a running hello graph, using only the wiki. The epic states an assumption to verify first, not
read: **the `kern-orch` + `kern-ui` pairing works today on a clean machine is unverified**. Running
it is the first task of this issue, and the page is written from what happened, not from what should
happen.

## Scope

- **Run it first**, on a clean machine, following nothing but the brick repositories: `kern-orch`
  executing a hello graph with `kern-ui` live in a browser. Record every step actually taken,
  including the ones that were not in any README.
- `en/integration/quickstart.md` written from that run: copy-pasteable commands, real module paths
  as they exist today, and the output a reader should actually see.
- **Stamped with the contract version and the date** — runnable content is stamped only after being
  run.
- **Stating plainly that its agent nodes are deterministic stubs rather than model calls**, because
  the `kern-agent` bridge does not exist. This is the page most likely to overpromise.
- Prerequisites listed honestly, including anything the run needed that no README mentions.
- If the pairing **does not** work today: the page becomes gap blocks describing exactly how far it
  gets and where it stops, `doc_state` drops accordingly, and the findings are reported in the PR
  description as issues to open on the bricks. That is a successful outcome for this issue, not a
  blocked one.

## Out of scope

- **No changes to brick code, and no fixes to make the quickstart work.** Findings become issues on
  the brick, not commits — and opening those issues is not part of this PR.
- **No CI-executed quickstart job** — the real fix for a contract bump breaking this page, and
  deliberately deferred past epic 4. The version stamp is the interim mitigation.
- **No model calls, no API keys, no secrets** of any kind in the instructions.
- **No repository-internal architecture explanation** — link the brick pages.

## Acceptance criteria / Definition of done

- [ ] The PR description states, in one sentence, the machine it was run on and whether it worked.
- [ ] Every command on the page was executed, in the order written, from the state described.
- [ ] The page carries `verified: {version, date}` naming the **contract** version the run exercised,
      and `# Citations` naming the paths read at that version.
- [ ] The stub reality is stated on the page itself, not only on the "what's missing" page.
- [ ] A reader following only the wiki reaches a running hello graph in under 15 minutes — say in
      the PR how long it took you.
- [ ] No step depends on knowledge not on the page or on a page it links.
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/integration/quickstart.md`.

Sources: `github.com/yoann/kern-orch` and the `Kern-UI` repository, at the versions run — plus the
contract version the run exercised.

## Dependencies

Blocked by [Issue 19](./19-add-kern-orch-brick-page.md),
[Issue 20](./20-add-kern-ui-brick-page.md) and [Issue 22](./22-add-contract-pages.md) — the page
links all three and stamps a contract version.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR. Most of this
issue's cost is the run, not the diff.
