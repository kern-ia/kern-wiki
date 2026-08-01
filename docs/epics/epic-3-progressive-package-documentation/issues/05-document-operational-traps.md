---
type: Issue
title: "Document the two operational traps, verified by reproduction"
description: "Reproduce and document the kern-orch empty-service-environment failure and kern-link's daemon-mode OAuth revocation risk as first-class page content."
tags: [epic-3]
resource: https://github.com/kern-ia/kern-wiki/issues/40
timestamp: 2026-08-01T14:10:00Z
epic: 3
issue: 05
slug: document-operational-traps
size: M
status: open
gh_issue: 40
depends_on: [01, 02]
---

# Document the two operational traps, verified by reproduction

## Summary

Two failures only surface once Kern runs unattended, and both are silent — the reader does not get
an error that points at the cause:

1. **`kern-orch serve` under an empty service environment loses `HOME` and its API keys**, and fails
   as in-band "no API key" errors rather than as a startup failure.
2. **`kern-link`'s OAuth flows impersonate first-party clients**, which its own documentation warns
   gets accounts revoked in long-running daemons — so daemon mode is **API keys only**.

The epic's acceptance criteria require both to be documented as first-class content, not footnotes.
This issue is the one that discharges that criterion, and it is deliberately separate from the brick
pages so that it cannot be quietly dropped when those pages run long.

The work is mostly verification, not writing. Both traps are claims inherited from the planning
document, and this epic does not restate claims it has not checked.

## Scope

- **Reproduce trap 1** — run `kern-orch serve` under an environment stripped the way a service
  manager strips it, and record exactly what happens: whether `HOME` is lost, which key lookup
  fails, what the reader sees, and what makes it work. If it does not reproduce as described, the
  page documents what actually happens; a corrected trap is a successful outcome.
- **Verify trap 2** — read `kern-link`'s own documentation and the OAuth code path, and record what
  it states about impersonation and revocation, at a named version. This one is verified by reading,
  not by getting an account revoked.
- **Write both up as their own `###` subsections**, in full, on the brick page that owns each:
  `en/bricks/kern-orch.md` and `en/bricks/kern-link.md`. Each subsection names the symptom first
  (that is what the reader arrives with), then the cause, then what to do instead.
- Each is a **blockquote callout with a bold lead**, per the markdown contract, at the point in
  Configuration or Usage where a reader would otherwise walk into it.
- `# Citations` extended on both pages with the paths read; `verified` re-set only if the whole page
  still qualifies at the version cited, and lowered rather than left stale if it does not.

## Out of scope

- **No new page.** The reader adopting one brick must find its trap on that brick's page without
  following a link; a shared "running unattended" page would make both traps a footnote, which is
  exactly what the epic forbids.
- **No deployment guide** — no systemd units, no container images, no service files. The scope is
  the failure and how to avoid it, not how to deploy Kern.
- **No changes to `kern-orch` or `kern-link`.** If the reproduction shows the failure could be a
  clear startup error instead of a silent in-band one, that is an issue on the brick, opened
  separately.
- **No secrets, keys or tokens** in any command or example on either page.
- **No general environment-variable tutorial.** The reader is assumed to know what a service manager
  is; the page documents what Kern does under one.
- No French translation.

## Acceptance criteria / Definition of done

- [ ] The PR description states, for trap 1, what was run, on what, and whether it reproduced as the
      planning document describes.
- [ ] Trap 1 is documented from the observed failure — the actual message a reader sees, not a
      paraphrase — and names what makes it work.
- [ ] Trap 2 is documented from `kern-link`'s own documentation and code at a named version, with
      the API-keys-only rule for daemon mode stated as a rule, not as a suggestion.
- [ ] Each trap has its own heading on its brick's page and appears where a reader would hit it, not
      appended at the end.
- [ ] Neither write-up hedges: anything not established carries a gap block naming it.
- [ ] `# Citations` on both pages names the paths read, grouped by brick and version, matching
      `verified.version` wherever a stamp is present.
- [ ] `hugo` builds with warnings fatal; `validate` passes; hard-wrapped at 100 columns.

## Relevant files / areas

No `en/` tree exists in this repository yet — paths follow the decided tree and epic 1's output,
not verified locations: `en/bricks/kern-orch.md` and `en/bricks/kern-link.md`.

Sources: `github.com/yoann/kern-orch` — the `serve` command and its key/credential lookup;
`github.com/julienlegoux/kern-link` — its OAuth provider code and the documentation carrying the
revocation warning. Both at the versions you cite.

## Dependencies

Blocked by [Issue 01](./01-document-kern-link.md) and [Issue 02](./02-document-kern-orch.md) — both
pages are deepened first, and this issue adds to them rather than racing them.

## PR size note

Target ~500 changed lines; well under it — this is a small diff on two existing pages, and most of
the cost is the reproduction. It touches two pages but splits neither.
