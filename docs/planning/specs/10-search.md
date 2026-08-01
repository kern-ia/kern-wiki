---
type: Decision
title: "Search"
description: "How does a reader search the wiki, and does it work per language?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 10
slug: search
status: decided
verdict: "Hextra's built-in FlexSearch, one index per language, placeholders indexed"
decided_via: triage
depends_on: [theme, bilingual-mechanism]
---

# Question

Search is one of the two reasons scope chose a generated site over plain markdown on GitHub
([decision](/scope/03-delivery-form.md)) — J3 ("arrive with a need, land on the right brick")
depends on it as much as on navigation. Zero budget rules out anything with a bill.

# Options

- **Hextra's built-in FlexSearch** — client-side, offline, index generated at build, no
  configuration, no service. Already paid for by [the theme decision](/specs/02-theme.md).
- **Pagefind** — better at large sites, low-bandwidth chunked index, excellent multilingual
  support. Adds a post-build step (a Rust binary in CI) and a UI to wire in.
- **Algolia DocSearch** — best relevance, free for open-source docs. An external dependency with
  an application process, an API key, and a crawler — three things that can silently stop working
  on a project nobody is paid to babysit.
- **None** — GitHub's own repo search as the fallback. Fails J3 for anyone who isn't already a
  contributor.

# Recommendation

**Hextra's built-in FlexSearch**, with a per-language index.

It is zero marginal cost against a theme already chosen, it is offline (so it cannot break
independently of the site), and at wiki scale — a few dozen pages, growing by brick — relevance
differences between the engines are academic.

Two points to fix rather than discover:

- **One index per language.** Searching in French must not return English pages that happen to
  share tokens, and vice versa; Hugo's multilingual build produces per-language output naturally
  ([decision](/specs/09-bilingual-mechanism.md)).
- **Placeholders are indexed, not hidden.** A reader searching "kern-agent" should land on the
  "what's missing" page. Making unwritten areas findable is the whole point of marking them
  explicitly ([decision](/scope/20-documenting-the-gap.md)) — hiding them would recreate the
  silence the project exists to fix.

Pagefind is the upgrade path if the index ever gets heavy; it changes no content and no URL, so
it is a cheap reversal — which is why it is not worth arguing about now.

# Verdict

**The theme's built-in client-side search**, accepted at triage: offline, zero marginal cost, one
index per language, placeholders indexed so unwritten areas stay findable. Algolia and any other
hosted service are rejected on the zero-budget, GitHub-native constraint.

**Contingency resolved:** [decision 02](/specs/02-theme.md) landed on Hextra, so this is Hextra's
built-in FlexSearch — no post-build step and no additional dependency. Pagefind remains the
upgrade path if the index ever gets heavy; it changes no content and no URL.
