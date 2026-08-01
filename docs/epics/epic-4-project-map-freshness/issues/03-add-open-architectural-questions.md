---
type: Issue
title: "Add the open architectural questions register"
description: "One register of the five questions that belong to no single repo, each with what is at stake, who owns it, and a link to the per-repo issue or an explicit no-issue-yet."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/45
epic: 4
issue: 03
slug: add-open-architectural-questions
size: M
status: open
gh_issue: 45
depends_on: []
---

# Add the open architectural questions register

## Summary

Knowledge that belongs to no single repository currently has nowhere to live. A question about the
seam between two bricks is not a `kern-orch` question and not a `kern-link` question, so it stays in
someone's head.

This page is where those five live:

1. **The `kern-agent` bridge** — the missing piece that keeps an LLM from running in a graph.
2. **The five pending agent-protocol extensions** on the orch↔agent-CLI seam.
3. **A possible `kern-contracts` extraction.**
4. **The Go module-path migration.**
5. **The `.github` cleanup.**

Questions 1 and 2 are already framed for readers on epic 1's *what's missing* page. Here they are
register entries — one line plus a link — not a second telling. The wiki must not describe the same
gap twice in two voices.

## Scope

- `en/status/open-questions.md`, typed against `data/vocab.yaml`.
- **A table or one `##` per question**, each carrying: what the question is, what it blocks or
  unblocks, which repository would own the change, and either a link to the issue where it is
  tracked or an explicit *no issue yet*.
- **Questions 1 and 2 are summarized in one line each and link to
  `en/ecosystem/whats-missing.md`.** Do not restate the bridge or enumerate the five protocol
  extensions here.
- **Questions 3, 4 and 5 are written here in full**, because no other page covers them:
  - `kern-contracts` extraction — what would move, what depends on it today, and that it is a
    possibility rather than a decision.
  - Module-path migration — the current paths quoted verbatim, what a migration would break, and
    that the breaking change stays owned by each repo.
  - `.github` cleanup — what is there now and what is wrong with it, recorded as a question.
- Each entry states **what would settle it**, so the register is actionable rather than a list of
  worries.
- The provisional banner verbatim wherever the register describes the provisional orch↔agent-CLI
  seam.
- `# Citations` naming the repository paths and issues actually read.

## Out of scope

- **Nothing here is performed.** The `.github` cleanup is recorded, not done; the module-path
  migration is flagged, not started; the `kern-contracts` extraction is a question, not a plan. The
  epic defers all three explicitly.
- **No issues opened on the brick repositories from this PR.** Where a question has no tracking
  issue, the register says *no issue yet* — opening one is a per-repo decision made by that repo's
  owner, not a side effect of a documentation PR.
- **No protocol specification.** Question 2 stays a link; writing the spec would freeze a
  provisional protocol by documentation, which the scope rejects outright.
- **No repo renames**, and no changes to any brick repository.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] All five questions appear, in one register, on one page.
- [ ] Questions 1 and 2 link to `en/ecosystem/whats-missing.md` and do not restate its content —
      a reader who follows the link finds the detail exactly once.
- [ ] Questions 3, 4 and 5 each state what is at stake, which repo owns it, and what would settle
      it.
- [ ] Every question carries either a link to its tracking issue or an explicit *no issue yet*. No
      question is left ambiguous about whether it is tracked.
- [ ] Module paths are quoted verbatim as they exist today, including in the migration entry.
- [ ] Nothing is described from its name — anything named was read, and is cited at a version.
- [ ] The provisional banner appears verbatim where the provisional seam is described, and
      `maturity` is set to match.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet — paths follow the decided content tree, not verified locations:
`en/status/open-questions.md`, `en/ecosystem/whats-missing.md` (from epic 1), `data/vocab.yaml`.

Sources: the `.github` repository as it stands, each brick's `go.mod`, and the issue trackers of
the repositories that would own each change.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) — specifically its *what's missing* page, which
questions 1 and 2 link to rather than duplicate. Independent of
[Issue 01](./01-add-transverse-status-page.md) and
[Issue 02](./02-add-consolidated-roadmap-page.md), though all three land in `en/status/`.

## PR size note

Target ~500 changed lines; one content page, under it.
