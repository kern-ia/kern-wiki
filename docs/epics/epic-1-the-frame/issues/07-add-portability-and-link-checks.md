---
type: Issue
title: "Add the portability and internal link checks"
description: "Fail any page carrying generator-specific syntax, and any bundle-relative link whose target does not exist in either tree."
tags: [epic-1]
resource: https://github.com/kern-ia/kern-wiki/issues/12
timestamp: 2026-08-01T11:30:00Z
epic: 1
issue: 07
slug: add-portability-and-link-checks
size: M
status: open
gh_issue: 12
depends_on: [05]
---

# Add the portability and internal link checks

## Summary

Two body-scanning checks that together keep the markdown contract enforceable: the site must survive
a theme or generator swap without touching one content file, and every internal link must work on
both surfaces — the published site and GitHub's own markdown view.

## Scope

**Portability check** — an error on any of:

- Hugo shortcodes, `{{< … >}}` or `{{% … %}}`;
- MDX or JSX;
- raw HTML beyond `<br>` and comments;
- any other generator-specific directive;
- a fenced code block with no language tag.

**Internal link check** — for every bundle-relative link (`/en/bricks/kern-orch.md` form):

- the target file exists;
- the check runs across both language trees, and against both surfaces — the repository path and the
  permalink the render hook produces;
- a link written in any other form (site-relative, or a repository URL to a page that exists in this
  bundle) is an error naming the form to use;
- an anchor target that does not exist on the linked page is an error.

Fixtures first, one per rule.

## Out of scope

- **No external link checking** — that is weekly and belongs to epic 4.
- **No prose rules** — Vale and markdownlint are deliberately excluded from v1; the risk here is
  asserting something untrue, not comma placement.
- **No hard-wrap enforcement.** The 100-column rule is held by review; promote it to a rule only if
  it stops holding, and in a separate PR.
- No link rewriting — the checks report, they never fix.

## Acceptance criteria / Definition of done

- [ ] Each forbidden construct has a rejecting fixture; a page using only allowed constructs passes.
- [ ] A bundle-relative link to a missing file fails, naming the file and the missing target.
- [ ] A link written in a non-canonical form fails with the canonical form in the message.
- [ ] Both checks run as part of `validate` in the PR job.
- [ ] `go test ./tools/...`, `gofmt -l`, `golangci-lint` all clean.
- [ ] `validate` against the pages existing at merge time exits 0.

## Relevant files / areas

No existing code for this yet. Paths: `tools/` (two rule packages on Issue 05's skeleton),
`tools/testdata/`.

The link check and `layouts/_markup/render-link.html` from
[Issue 02](./02-add-hugo-site-and-link-render-hook.md) must agree on what resolves; if they
disagree, say which one you changed and why.

## Dependencies

Blocked by [Issue 05](./05-scaffold-tools-and-okf-conformance.md).

## PR size note

Target ~500 changed lines; if this grows past ~1000, split it before opening the PR.
