---
type: Decision
title: "Placeholder and maturity phrasing"
description: "SPECS decided the fields; the words a reader actually sees are a convention, and they are criterion 1's front line."
tags: [decision, conventions]
timestamp: 2026-08-01T09:26:00Z
phase: conventions
decision: 9
slug: placeholder-phrasing
status: decided
verdict: "one banner, for `provisional` only, written literally in the page; the validator asserts banner ⟺ front matter both ways, and gap block ⟺ `doc_state`"
decided_via: discussion
depends_on: [page-structure-and-templates]
---

# Question

`doc_state` and `maturity` are front matter ([decision](/specs/05-page-metadata.md)); the reader
never sees them. What the reader sees is whatever each writer types into an empty section — and
"TODO", "coming soon", "*(to be documented)*" and a silently empty section are four different
promises, three of which are wrong.

The placeholder convention is named in the scope as **the deliverable not to cut under time
pressure**. Its wording is therefore not a detail.

# Options

- **One canonical block, copied from the template** — uniform, and drifts as people retype it.
- **One canonical block, generated** — the writer sets `doc_state`/`maturity` and the block is
  rendered by the theme layer from the front matter, so the words cannot vary.
- **Free-form, reviewed** — every review re-litigates the wording of not-knowing.

# Recommendation

**Generated from front matter where it can be, canonical text where it can't.**

Two distinct things, kept distinct — the SPECS invariant is that `maturity` describes the code
and `doc_state` describes the page:

- **A maturity banner**, rendered once at the top of a page from `maturity`:
  - `works-today` — no banner. The default state needs no announcement.
  - `provisional` — *"This describes a provisional interface. It is expected to change, and
    changes are not announced."*
  - `planned` — *"This is planned, not built. Nothing described here runs today."*
- **A gap block**, placed inside the section that has nothing true to say:
  > **Not documented yet.** *(one line naming what is missing and, if known, what would settle
  > it — an issue link, a package that hasn't landed, a protocol extension.)*

The rules around them:

- **A gap block never guesses.** The one line says what is missing, never what the answer is
  likely to be — "not documented yet: the retry policy" and never "not documented yet: probably
  exponential backoff".
- **Exactly one wording each.** The gap block's lead is verbatim `**Not documented yet.**`, which
  makes it greppable, countable, and mechanically checkable against `doc_state`.
- **The validator asserts the pair**: a page with `doc_state: documented` containing a gap block
  fails; a page with `doc_state: placeholder` containing *no* gap block fails. This is the
  cheapest possible enforcement of "no false information" and belongs in M1's validator, with
  fixtures.
- **`planned` implies a gap block** in every content section — a planned thing has no
  configuration to document, and inventing one is the exact non-goal.
- The rendering lives in `layouts/`, not in a shortcode: content stays shortcode-free
  ([decision](/specs/03-markdown-contract.md)), so the banner is derived from front matter at
  build time and the gap block is plain markdown that reads correctly on GitHub too.

# Verdict

**Amended in discussion, and smaller than recommended.** The question "what is a banner actually
for?" removed two thirds of it.

A banner earns its place in exactly one state. Criterion 3's reader often arrives by search or a
deep link, on a single page, having seen neither the registry nor the freshness table — and:

- `works-today` — no banner; the default state does not announce itself.
- `planned` — no banner. The page is already made entirely of gap blocks, because there is
  nothing true to write about something that does not exist. A banner would repeat what every
  section already says.
- `provisional` — **banner**. The only dangerous case: the content is correct, verified and
  useful, there is no gap block anywhere, and the `verified` stamp reads as reassurance — while
  the interface described can change without announcement. Nothing in the page's structure
  signals that. This is the orch↔agent-CLI seam, and the scope commissioned it by name
  ([risks](/scope/18-risks-and-assumptions.md)).

So, decided:

- **One banner text, for `provisional` only**, written literally in the page (copied from the
  template, like the gap block) rather than rendered from front matter:

  > **This describes a provisional interface.** It is expected to change, and changes are not
  > announced.

  Literal rather than generated because a build-time banner is invisible on GitHub, where the
  scope requires every page to stay readable — which would hide the wiki's sharpest warning on
  half its surfaces. No sixth `gen` surface is needed for a single state.

- **The validator asserts the equivalence both ways**: `maturity: provisional` ⟺ that exact block
  present. Roughly ten lines of Go and its fixtures.
- **The gap block is unchanged**: verbatim `**Not documented yet.**` lead, one line naming what
  is missing, never guessing what the answer is likely to be; `doc_state` and gap-block presence
  checked against each other in both directions; `planned` implies a gap block in every content
  section.
