---
type: Decision
title: "Observability & analytics"
description: "How does anyone know the site is healthy, and is reader behaviour measured?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 16
slug: observability-and-analytics
status: decided
verdict: "No analytics; CI failure, the weekly link check and the staleness issue are the health signals"
decided_via: triage
depends_on: [hosting-and-deployment, ci-checks]
---

# Question

A static site has no runtime to observe, but two questions still need answers: what tells the
team the site is broken, and is reader behaviour measured? The second is tempting — success
criterion 4 is "under 15 minutes from the site to a running hello graph", and criterion 9 is "the
status page actually gets used" ([decision](/scope/14-success-criteria.md)). Both sound like
analytics questions.

# Options

- **No analytics** — CI and the scheduled checks are the only health signal. Zero cost, zero
  privacy surface, and no data about whether anyone reads the thing.
- **Privacy-respecting analytics** (Plausible, GoatCounter, Umami) — page views without cookies.
  Either a bill or a self-hosted service; both violate the zero-budget/GitHub-native constraint,
  and a French-facing site adds a GDPR conversation nobody asked for.
- **Google Analytics** — free, and imports cookie banners and a consent regime into a five-page
  documentation site.

# Recommendation

**No analytics in v1.** Health comes from CI:

- **Build failure on `main`** — the deploy workflow failing is the outage signal, and GitHub
  already emails it.
- **Weekly external link check** ([decision](/specs/12-ci-checks.md)) — the closest thing to
  monitoring a static site has.
- **The staleness issue** ([decision](/specs/14-freshness-automation.md)) — the content-health
  signal, which is the one that actually matters here.

On the two criteria that look like analytics questions: neither is answered by page views.
"Under 15 minutes to a hello graph" is verified by *someone running it on a clean machine* — the
first real task of M1, per scope's own assumption list. "The status page gets used to pick a next
task" is answered by asking the two contributors. With this audience size, measurement is
conversation, and instrumenting a site to learn what two people did is theatre.

Revisit if the wiki ever gets meaningful external traffic — which is a good problem, and a cheap
reversal.

# Verdict

**No analytics in v1**, accepted at triage. No tracking, no cookie banner, no consent regime on a
bilingual documentation site. Health signals are the deploy workflow failing, the weekly external
link check, and the staleness issue — the last being the one that actually matters, since content
rot is this project's real outage.

The two success criteria that sound like analytics questions are answered by running the quickstart
and by asking the two contributors.
