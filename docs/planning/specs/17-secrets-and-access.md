---
type: Decision
title: "Secrets & cross-repo access"
description: "What credentials does the wiki's automation need, given it reads other repos?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 17
slug: secrets-and-access
status: decided
verdict: "`GITHUB_TOKEN` only, least-privilege per job, no PAT and no other repository secrets"
decided_via: triage
depends_on: [hosting-and-deployment]
---

# Question

The site itself has no configuration and no secrets — it is static files. The automation is a
different matter: the staleness job reads **other repositories'** releases
([decision](/specs/14-freshness-automation.md)), and the workflow's built-in `GITHUB_TOKEN` is
scoped to the wiki repo alone.

Whether that is a problem depends on a fact worth stating rather than assuming: whether every
brick repo is public. `kern-link` and `Kern-Orch` are known-public; the rest is unverified, and
the licence audit that would have established this is out of scope
([decision](/scope/13-non-goals.md)).

# Options

- **`GITHUB_TOKEN` only** — reads public repos' metadata fine (the token authenticates the
  request for rate-limit purposes even when the target is public), writes issues in the wiki repo.
  Zero secrets to manage, zero rotation. Fails on any brick repo that is private.
- **A fine-grained PAT stored as a repo secret** — works for private repos, and is a long-lived
  credential in a documentation repo that one person must remember to rotate.
- **A GitHub App installed on the org** — the clean answer for cross-repo reads, and real setup
  work for a weekly metadata poll.

# Recommendation

**`GITHUB_TOKEN` only, with `contents: read` / `pages: write` / `id-token: write` on the deploy
job and `issues: write` on the staleness job — and no other secrets in the repository.**

If a brick repo turns out to be private, the fix is *not* a PAT: it is that the wiki does not
document a private brick, since scope's audience is external readers who could not use it anyway.
The staleness job reports an unresolvable repo as an error rather than skipping it
([decision](/specs/14-freshness-automation.md)), so this surfaces as a visible failure the first
time it happens instead of as silence.

Corollaries, small but worth writing down once:

- **Least-privilege per job**, declared in each workflow — the default read-all token permission
  is a habit worth not forming in a repo the org will copy from.
- **No secret can appear in the built site.** With no build-time configuration at all, this is
  structural rather than a rule to follow.
- **Dependabot on GitHub Actions** — the only dependency surface that can be attacked here is the
  actions themselves; pinning plus updates is cheap.

# Verdict

**`GITHUB_TOKEN` only, least-privilege per job, no other secrets**, accepted at triage. Dependabot
watches the Actions themselves, the only dependency surface that exists.

If a brick repo turns out to be private, the answer is that the wiki does not document it — not a
PAT. The staleness job surfaces that as a visible error the first time it happens.
