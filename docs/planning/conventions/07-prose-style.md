---
type: Decision
title: "Prose style & voice"
description: "The house style for the wiki's actual product — the baseline covers code style and says nothing about writing."
tags: [decision, conventions]
timestamp: 2026-08-01T09:22:00Z
phase: conventions
decision: 7
slug: prose-style
status: decided
verdict: "a short truthfulness-weighted rule set: second person, present tense, no unverifiable adjectives, versions named, uncertainty is a placeholder and never a hedge"
decided_via: triage
depends_on: []
---

# Question

The binding constraint on this project is **consistency across several writers**
([scope](/scope/15-constraints.md)), and criterion 6 is that another contributor writes a page
matching the templates *without asking how*. The baseline has a Code style section and nothing
about prose. With no prose linter by design ([decision](/conventions/02-formatters-and-linters.md)),
whatever is decided here is held by review — so it must be short enough to remember.

# Options

- **A full style guide** — voice, tense, punctuation, Oxford comma, capitalization tables. Nobody
  reads it, and it invites the comma-placement review SPECS explicitly refused.
- **A short rule set aimed at truthfulness** — half a dozen rules, each of which prevents a page
  from asserting more than it knows, plus two or three that keep pages recognizably one wiki.
- **Nothing; imitate neighboring pages** — works for two people and fails the moment a third
  arrives, which the scope says is expected.

# Recommendation

**A short rule set, weighted toward truthfulness.** Proposed as the whole of it:

**Register**

- **Second person for instructions** ("run `kern-orch serve`"), third person for description. No
  first person, singular or plural — the wiki has no narrator.
- **Present tense for what is; explicit future only for what is planned**, and planned things
  carry a maturity marker rather than a promise.
- **No marketing register.** No "powerful", "seamless", "simply", "just", "blazing". A brick does
  what it does; adjectives that can't be checked are the same failure as a false claim, only
  harder to spot.

**Truthfulness**

- **Every version-specific statement names its version.** "kern-orch checkpoints to disk" is a
  claim about a version, so it says which.
- **Uncertainty is a placeholder, never a hedge.** "may", "should", "probably" describing *our*
  knowledge is forbidden — if it isn't verified, the placeholder block says so
  ([decision](/conventions/09-placeholder-phrasing.md)). ("may" describing genuine runtime
  behavior is fine: "the call may return a rate-limit error".)
- **Nothing is described from its name.** A function, flag or field is documented only after
  someone read it — the no-invented-content non-goal, at sentence level.

**Shape**

- **Lead with what the reader came for.** No preamble paragraph restating the section title.
- **Code blocks are copy-pasteable and real** — actually run, with the module path as it exists
  today, not as it should be ([scope](/scope/18-risks-and-assumptions.md)).
- **Prefer a table to a list of parallel facts**, a list to a paragraph of them.
- British/American spelling: **American**, matching the Go ecosystem and the existing repos.

# Verdict

**The short rule set above is the whole of the prose standard**, accepted at triage — register,
truthfulness, shape, and American spelling. Held by review, not by a linter
([decision](/conventions/02-formatters-and-linters.md)). Its load-bearing rules are the three
truthfulness ones: every version-specific statement names its version, uncertainty is a
placeholder rather than a hedge, and nothing is described from its name.
