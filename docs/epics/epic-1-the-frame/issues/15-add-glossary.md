---
type: Issue
title: "Add the glossary"
description: "Consolidate and translate Kern-Orch/docs/GLOSSAIRE.md into the wiki's normative glossary, one canonical spelling per thing."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/20
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 15
slug: add-glossary
size: M
status: open
gh_issue: 20
depends_on: [13]
---

# Add the glossary

## Summary

Deliverable 11. The ecosystem's vocabulary currently exists, in French, trapped inside one repo —
`Kern-Orch/docs/GLOSSAIRE.md`. This page frees it and makes it **normative from this milestone**:
one canonical spelling per thing, which every other page and every future translation is checked
against.

## Scope

- `en/ecosystem/glossary.md` — every term from `Kern-Orch/docs/GLOSSAIRE.md`, translated to English,
  plus the terms the wiki itself introduces (brick, contract, maturity marker, gap block, stamp).
- **A French column from the start**, holding the term's French form — it is the source material's
  own language, and epic 5's translators are required to follow it. Keeping it now avoids losing the
  original wording.
- **Aliases rather than corrections**: where the wiki's term differs from a repo's, the glossary
  records the repo's spelling as an alias. The wiki does not correct the repos.
- A note stating the glossary accrues — a term not in it is added by the PR that first uses it — so
  it is not read as a frozen M1 deliverable.
- Contract identifiers appear with their versions; brick names lowercase and backticked.

## Out of scope

- **No French page** — the French *column* is vocabulary, not a translation. `fr/` is epic 5.
- **No re-hosting of `Kern-Orch`'s architecture notes** — the glossary takes the vocabulary, nothing
  else. That repo stays the authoritative home for its own docs.
- **No invented terms.** A term whose meaning you cannot establish from the source or the code gets
  a gap block, not a plausible definition.
- No glossary-coverage CI rule — it has no writable fixture and stays a checklist item.

## Acceptance criteria / Definition of done

- [ ] Every term in `Kern-Orch/docs/GLOSSAIRE.md` is present, translated, or explicitly recorded as
      dropped with the reason.
- [ ] No definition is written from a term's name; each is checked against the source or the code,
      and cited.
- [ ] Where the wiki and a repo disagree on a spelling, the repo's appears as an alias and no page
      tells the repo it is wrong.
- [ ] `# Citations` names `Kern-Orch` at the version read, with the path.
- [ ] The page does not contradict `Kern-Orch`'s own docs on any term (criterion 5).
- [ ] `hugo` builds; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No existing content for this yet. Path: `en/ecosystem/glossary.md`.

Source: `Kern-Orch/docs/GLOSSAIRE.md`, at the version you read — name it in `# Citations`.

## Dependencies

Blocked by [Issue 13](./13-write-home-and-ecosystem-overview.md).
Every later content issue links it on first use of a term.

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
