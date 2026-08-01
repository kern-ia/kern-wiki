---
type: Issue
title: "Add the weekly external link check"
description: "Extend validate with an external-link mode and run it weekly off the pull request path, reporting into one rolling issue instead of a silently red scheduled workflow."
tags: [epic-4]
timestamp: 2026-08-01T16:05:00Z
resource: https://github.com/kern-ia/kern-wiki/issues/46
epic: 4
issue: 04
slug: add-weekly-external-link-check
size: M
status: open
gh_issue: 46
depends_on: []
---

# Add the weekly external link check

## Summary

Epic 1 checks internal links on every pull request. External links cannot go on that path — they are
slow, they are flaky, and a third-party outage must never block a merge. SPECS puts them weekly, off
the pull request path, alongside the staleness job.

This issue adds that check. A dead link to a brick's README is the cheapest kind of wrong the wiki
can be, and the only kind it can detect without reading code.

## Scope

- **Extend `validate` with an external-link mode** — a flag, not a fourth subcommand. SPECS fixes
  the binary's subcommand set at `validate` / `gen` / `stale`
  ([decision](/specs/13-tooling-language.md)); adding `links` alongside them would be a fourth
  source of truth about what the tool does.
- Collect every external (non-bundle-relative) link target across both content trees, deduplicate by
  URL, and request each one. Follow redirects; a permanent redirect is reported as a link to fix,
  not as a failure.
- **Distinguish dead from flaky**: retry with backoff, and classify timeouts, 429s and 5xx
  separately from 404s and 410s. A report that mixes them trains people to ignore it.
- `.github/workflows/links.yml` — weekly schedule plus `workflow_dispatch`, `GITHUB_TOKEN` only,
  least-privilege per job, pinned actions.
- **The result lands in one rolling issue**, labelled `broken-links`, created once and edited in
  place — the same pattern the staleness job uses
  ([decision](/specs/14-freshness-automation.md)). A scheduled workflow that merely goes red is
  invisible; nobody watches the Actions tab weekly. When nothing is broken, the issue body says so
  and the issue is closed rather than deleted.
- Standard library HTTP client. A new dependency needs a one-line justification in the PR, and this
  one does not need one.

## Out of scope

- **Not on the pull request path.** Do not add this to the PR workflow, not even as a
  non-blocking job.
- **No internal link checking** — epic 1 issue 07 owns it, on every PR, and this must not duplicate
  it.
- **No third-party link-checker action.** The zero-budget, GitHub-native constraint plus the
  prefer-the-standard-library rule both point the same way, and a scheduled job running someone
  else's binary against every URL in the wiki is a dependency worth not having.
- **No fixing of the links it finds** — that is what the issue it opens is for.
- **No auto-editing of content.** Nothing in this job writes to a page.

## Acceptance criteria / Definition of done

- [ ] Every rule starts as a failing fixture under `tools/testdata/`, committed in the same PR, red
      before green. A rule with no fixture is not merged.
- [ ] The HTTP client is faked at the boundary in tests — no test makes a real network request.
- [ ] Dead links (404/410) and flaky results (timeout/429/5xx) are reported in separate sections,
      and a flaky result never reads as a dead link.
- [ ] Permanent redirects are reported as links to update.
- [ ] The workflow runs weekly and on `workflow_dispatch`, uses `GITHUB_TOKEN` only, declares
      least-privilege permissions per job, and pins its actions.
- [ ] Re-running with nothing broken edits the existing issue and closes it, rather than opening a
      second one.
- [ ] Error messages name the file, the URL and the status — the audience is whoever fixes it.
- [ ] `gofmt -l` is silent, `golangci-lint` passes with warnings fatal, `go test ./tools/...`
      passes.

## Relevant files / areas

No `tools/` binary exists in this repository yet — paths follow the decided layout
([specs](/specs/13-tooling-language.md)) and epic 1's output, and are not verified locations:
`tools/` (the `validate` subcommand from epic 1 issues 05–07), `tools/testdata/`,
`.github/workflows/`.

## Dependencies

Blocked by [Epic 1](/epic-1-the-frame/EPIC_1.md) — the `tools/` binary and its `validate`
subcommand, and the link collection this reuses. Independent of the staleness job
([Issue 05](./05-add-stale-version-comparison.md) onward), though the two share the rolling-issue
pattern; whichever lands first sets it.

## PR size note

Target ~500 changed lines; Go code plus fixtures plus one workflow. If the report rendering and the
issue upsert push it past ~1000, split the upsert out — but the same upsert is needed by
[Issue 06](./06-add-weekly-staleness-issue.md), so prefer factoring it into a shared helper here and
reusing it there.
