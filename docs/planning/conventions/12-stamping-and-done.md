---
type: Decision
title: "Stamping and the definition of done for a page"
description: "What a human must have done before setting `verified` and flipping `doc_state` to documented."
tags: [decision, conventions]
timestamp: 2026-08-01T09:32:00Z
phase: conventions
decision: 12
slug: stamping-and-done
status: decided
verdict: "stamp stays per page; coverage is derived from git (diff since the commit that last set `verified`), reported as a non-blocking sticky PR comment and carried by the weekly staleness issue"
decided_via: discussion
depends_on: [citations-discipline, review-and-merge]
---

# Question

SPECS defines `verified: {version, date}` and forbids the staleness job from ever writing it,
because *a stamp means a human read the code* ([decision](/specs/14-freshness-automation.md)).
That sentence is the whole honesty mechanism — and it is currently a sentence in a spec, not a
rule anyone can apply. Nothing says what "read the code" means, who may claim it, or when
`doc_state` moves `partial → documented`.

Without it, the stamp degrades into "someone edited this page recently", and the freshness table
— an M1 deliverable and criterion 8 — measures nothing.

# Options

- **Stamp on edit** — any substantive edit refreshes the stamp. Zero friction, and the stamp
  becomes a modification date, which `timestamp` already is.
- **Stamp on verification, with a stated meaning** — the writer read the named sources at the
  named version and each claim on the page is true of it.
- **Stamp only after executing** — run every command on the page before stamping. Correct for
  the quickstart, impossible for a configuration reference.

# Recommendation

**Stamp on verification, with the meaning written down**, plus one carve-out for executable
content.

Setting `verified: {version: vX, date: D}` asserts, of *the whole page*:

1. every claim on it was checked against `vX` of the brick, by reading the sources listed in
   `# Citations` ([decision](/conventions/11-citations-discipline.md));
2. anything that could not be checked carries a gap block
   ([decision](/conventions/09-placeholder-phrasing.md)) rather than a hedge;
3. no section was skipped — the stamp covers the page, not the paragraph that was edited.

Consequences, deliberately:

- **Editing one section re-stamps the whole page, or the stamp is left alone.** There is no
  partial stamp. Someone fixing a typo does not touch `verified` — and does not need to.
- **`doc_state: documented` requires a stamp** (already a validator rule) **and no gap blocks**
  (proposed in decision 9). `partial` is the honest state for most pages for most of this
  project's life, and is not a defect.
- **Runnable content is stamped only after being run** — the quickstart, install commands,
  configuration examples. The scope already says the quickstart is *verified by running it*; this
  generalizes it: a command nobody executed is a claim nobody checked.
- **First stamp on a page requires review** ([decision](/conventions/06-review-and-merge.md));
  re-stamps do not, since the meaning is by then established and the citations show the work.
- **The staleness job never writes a stamp, and neither does any other automation** — restated
  here because this is where a future contributor would come looking for permission.

The friction is real and intended: a stamp is expensive to place, which is what makes it worth
reading. The escape valve is that an unstamped page is perfectly legitimate — it just says
`placeholder` or `partial` and tells the truth about itself.

# Verdict

**The stamp's meaning stands as recommended** — it asserts, of the whole page, that every claim
was checked against version `vX` by reading the sources in `# Citations`, that anything
uncheckable carries a gap block, and that no section was skipped. Runnable content is stamped
only after being run. The staleness job, and any other automation, never writes a stamp.

Two amendments came out of the discussion.

**1. "First stamp requires review" is dropped** — [decision 06](/conventions/06-review-and-merge.md)
removed every approval gate, so the clause had nothing to attach to.

**2. Coverage is derived from git rather than re-asserted.** The granularity problem — a one-line
edit to an eight-section page nominally forcing a whole-page re-verification — is answered by
history: git knows the commit that last set `verified` on a file, so
`git diff <that-commit>..HEAD -- <path>` is exactly what entered the page since it was checked.

- **The stamp still covers the whole page.** Git narrows the *work*, not the scope: a two-line
  diff can invalidate everything around it, so the rule is *re-read the diff and whatever it
  touches* — a human judgement, not a mechanical one.
- Two complementary axes, neither redundant: the staleness job asks *the brick moved, did the
  page?* ([decision](/specs/14-freshness-automation.md)); this one asks *the page moved, did the
  verification?*
- **`tools/` gains the second axis** in `stale`, plus a `diff-since-stamp <page>` helper that
  prints what is left to re-read.
- **Non-blocking.** A PR whose body changed without its stamp does **not** fail. A job posts a
  **sticky comment** on the PR — rewritten in place on each push, not appended — listing the
  affected pages and what changed since their stamp. It is a prompt, not a gate: a typo fix must
  not cost a re-verification.
- **The escape valve stands**: if you don't re-verify, lower `doc_state` rather than leave a
  stamp that no longer covers the page.

Two operational consequences to carry into M1: `actions/checkout` needs `fetch-depth: 0` in any
job doing this (the default depth of 1 has no history to read), and that job needs
`pull-requests: write` — the first permission beyond read in a repository whose rule is
least-privilege per job ([decision](/specs/17-secrets-and-access.md)). No PAT is involved.

**The weakness, stated.** With no approval gate and a non-blocking comment, nothing *forces*
re-verification — a PR comment also disappears from view the moment the PR merges. What catches
it afterwards is the weekly staleness issue, which is persistent and carries the same axis. If
pages start merging with stamps that no longer cover them, the fix is to make this check
blocking, not to reintroduce review.
