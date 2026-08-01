---
type: Conventions
title: "Kern wiki — Conventions"
description: "The personal baseline re-aimed at a repository whose product is prose: nothing is enforced by discipline, because green CI is the only gate."
tags: [planning, conventions]
timestamp: 2026-08-01T10:05:00Z
status: final
baseline_version: 2026-07-20T13:00:00Z
---

# Kern wiki — Conventions

The standards this repository is written and reviewed by. It is the personal conventions baseline
with thirteen project decisions merged in — four re-aiming baseline rules calibrated for code at a
repository where roughly all of the diff is prose, nine filling gaps the baseline does not cover.

Full ledger: [conventions decision ledger](/conventions/index.md) — 13 decided.

Two facts shape everything below.

**Green CI is the only merge gate** ([decision](/conventions/06-review-and-merge.md)). No approval
is required anywhere. A convention that cannot become a check is therefore held by the person who
would break it — which is why the rules that protect criterion 1 are written here as *checks*,
with their fixtures, rather than as advice.

**This document is the source; the M2 "how to write here" page is its rendering** for contributors
([decision](/conventions/08-page-structure-and-templates.md)). Where they overlap, this one wins,
and a rule that exists only in the M2 page is a bug to fix here. Neither restates the validator:
anything mechanically enforced is documented as *CI checks this*, so a rule has one place to rot.

`docs/` — this bundle — ships in the repository but is listed in `.okfignore` and in Hugo's ignore
list ([decision](/conventions/01-planning-bundle-location.md)). One published bundle, one private
one, sharing a checkout.

## Code style & formatting

A formatter is law, in `tools/` — and nowhere else
([decision](/conventions/02-formatters-and-linters.md)).

- **Go**: `gofmt -l` failing on any output, and `golangci-lint` with its default set, warnings
  fatal. CI runs both.
- **Markdown**: no formatter and no linter. Vale and markdownlint were excluded by SPECS — *the
  risk here is asserting something untrue, not comma placement*
  ([decision](/specs/12-ci-checks.md)) — and no prose tool has been added since.
- The one whitespace rule: **hard-wrap markdown at 100 columns**; tables and fenced blocks exempt.
  Held by review, promotable to a validator rule if it doesn't hold.
- No commented-out code in committed files.

## Naming

- Descriptive over short; no abbreviations that aren't industry-standard.
- **Go** (`tools/`): community casing — PascalCase for exported identifiers, camelCase otherwise.
  Files named after the main thing they define.
- **Content files**: lowercase kebab-case on the canonical `kern-*` names, as decided in
  [specs](/specs/07-links-and-urls.md).
- Naming *in prose* is a separate and stricter matter — see [Terminology](#terminology).

## Repository layout

The repository root **is** the OKF bundle root ([decision](/specs/23-okf-conformance.md)), so the
baseline's "docs live under `docs/`, top level stays small" does not apply: the top level is
content trees, tooling and configuration, and the full shape is decided in
[specs](/specs/04-content-tree.md).

- `templates/` holds the page templates, copyable and never published.
- `tools/` holds the one Go binary: `validate`, `gen`, `stale`.
- `docs/` holds this planning bundle, ignored by both the validator and Hugo.

## Writing the wiki

This is the section that matters. Everything above and below governs a tenth of the diff.

### Prose style & voice

A short rule set, weighted toward truthfulness, held by review
([decision](/conventions/07-prose-style.md)).

**Register**

- **Second person for instructions**, third person for description. No first person — the wiki has
  no narrator.
- **Present tense for what is.** Explicit future only for what is planned, and planned things
  carry a maturity marker rather than a promise.
- **No marketing register**: no *powerful*, *seamless*, *simply*, *just*, *blazing*. An adjective
  nobody can check is the same failure as a false claim, only harder to spot.

**Truthfulness**

- **Every version-specific statement names its version.**
- **Uncertainty is a placeholder, never a hedge.** *May*, *should*, *probably* describing our own
  knowledge are forbidden; if it isn't verified, the gap block says so. (*May* describing genuine
  runtime behaviour is fine: "the call may return a rate-limit error".)
- **Nothing is described from its name.** A function, flag or field is documented only after
  someone read it — the no-invented-content non-goal, at sentence level.

**Shape**

- Lead with what the reader came for; no preamble restating the heading.
- Code blocks are copy-pasteable and real, with module paths **as they exist today**.
- Prefer a table to a list of parallel facts, a list to a paragraph of them.
- American spelling, matching the Go ecosystem and the existing repos.
- **Headings are descriptive, never clever** — no puns, idioms or metaphors. They are translated
  later, and a clever heading makes the two languages unverifiable against each other.

### Page structure & templates

Templates are **binding on the section set and their order, free below `###`**
([decision](/conventions/08-page-structure-and-templates.md)).

- Each `type` in the closed vocabulary carries its required heading list in `data/vocab.yaml`.
  *CI checks this*: presence, order, and the absence of unknown `##` headings on typed pages.
- **A section with nothing true to say keeps its heading and carries a gap block.** It is never
  deleted — a missing section and an unwritten one must not look the same.
- Changing a template updates every instantiated page in the same PR, or opens issues for them.
- A page is a page: **content is never split across two PRs**, because its correctness is internal
  coherence and a reviewer can only judge that whole
  ([decision](/conventions/05-pr-size-and-unit.md)).

### Placeholders & maturity

The convention the scope names as the one not to cut under time pressure
([decision](/conventions/09-placeholder-phrasing.md)). `maturity` describes the code, `doc_state`
describes the page, `timestamp` describes the file — three fields, deliberately.

**The gap block**, placed inside the section that has nothing true to say, lead verbatim so it is
greppable and countable:

> **Not documented yet.** *(one line naming what is missing and, if known, what would settle it.)*

It **never guesses** — "not documented yet: the retry policy", never "…probably exponential
backoff".

**One banner, for `provisional` only**, written literally in the page rather than rendered from
front matter — a build-time banner is invisible on GitHub, where every page must stay readable,
and that would hide the sharpest warning the wiki has on half its surfaces:

> **This describes a provisional interface.** It is expected to change, and changes are not
> announced.

`works-today` carries no banner — the default state does not announce itself. `planned` carries
none either: the page is already made entirely of gap blocks, and a banner would repeat what every
section says. `provisional` is the dangerous state precisely because the content is correct,
verified and useful, with nothing in the page's structure signalling that it can break.

*CI checks this*: `maturity: provisional` ⟺ that exact block present, both directions;
`doc_state: placeholder` ⟺ a gap block present, both directions; `planned` implies a gap block in
every content section.

### Terminology

The glossary is **normative from M1**, with one canonical spelling per thing
([decision](/conventions/10-terminology-and-naming.md)).

- **Bricks in prose**: lowercase, backticked — `kern-orch`, `kern-ui`, `kern-link`, `kern-anon`.
  A repository's real name appears only when the sentence is about the repository or a URL; the
  mapping table lives once, on the ecosystem page.
- **Contracts** are written as their identifier, always with the version: `kern.run.v1`. A
  contract without its version is not a contract.
- **Module paths are quoted verbatim as they exist today** — `github.com/yoann/kern-orch` — never
  normalized to what they ought to become. A `go get` line that doesn't work is a false claim.
- The ecosystem is **Kern**; the packages are **bricks** — not modules, services or components.
- First use of a glossary term on a page links the glossary; later uses don't.
- **A term not in the glossary is added to it in the PR that first uses it.** The glossary accrues;
  it is not an M1 deliverable that then freezes.
- Where the wiki's term differs from a repo's, the glossary records the repo's as an alias rather
  than correcting the repo.

*CI checks this*, at warning level: capitalized brick spellings outside link targets, code blocks
and the mapping table.

### Citations

Technical pages end with `# Citations`, and a citation is **a path at a version**
([decision](/conventions/11-citations-discipline.md)):

```
# Citations

- `kern-orch` v0.2.0 — `internal/graph/checkpoint.go`, `docs/GLOSSAIRE.md`
- `kern-link` v0.1.1 — `README.md`, `providers/anthropic/client.go`
- `kern-orch-kern-link-compat.md` (external analysis, 2026-07-28)
```

- **Grouped by brick and version**, because the version is what the stamp claims.
- **Paths, not repository homes.** A bare repo link cites nothing.
- **What was *read***, not what supports the claim in retrospect. The audience is the next person
  verifying the page, who needs to know where to look.
- Non-repository sources are cited too, with a date.

*CI checks this*: every line begins with a backticked identifier, and versions named here match
`verified.version` where the page carries one — which catches a page stamped v0.2.0 whose
citations were taken from v0.1.

### Stamping, and when a page is done

Setting `verified: {version: vX, date: D}` asserts, **of the whole page**
([decision](/conventions/12-stamping-and-done.md)):

1. every claim on it was checked against `vX`, by reading the sources listed in `# Citations`;
2. anything uncheckable carries a gap block rather than a hedge;
3. no section was skipped — the stamp covers the page, not the paragraph that was edited.

Consequently:

- **There is no partial stamp.** A typo fix does not touch `verified`, and does not need to.
- **`doc_state: documented` requires a stamp and no gap blocks.** `partial` is the honest state for
  most pages for most of this project's life, and is not a defect.
- **Runnable content is stamped only after being run** — the quickstart, install commands,
  configuration examples. A command nobody executed is a claim nobody checked.
- **No automation ever writes a stamp**, the staleness job included. A stamp means a human read
  the code.

**Coverage is derived from git, not re-asserted.** Git knows the commit that last set `verified` on
a file, so `git diff <that-commit>..HEAD -- <path>` is exactly what entered the page since it was
checked. This narrows the *work* — re-read the diff and whatever it touches — without narrowing the
*scope*: a two-line diff can invalidate everything around it, and that judgement stays human.

Two complementary axes, neither redundant:

| Axis | Question | Where it surfaces |
|---|---|---|
| Staleness ([specs](/specs/14-freshness-automation.md)) | the brick moved — did the page? | weekly rolling issue |
| Stamp coverage | the page moved — did the verification? | sticky PR comment, and the same weekly issue |

The PR comment is **non-blocking** and rewritten in place on each push: a typo fix must not cost a
re-verification. If you don't re-verify, **lower `doc_state`** rather than leave a stamp that no
longer covers the page.

Two operational requirements follow: `actions/checkout` with `fetch-depth: 0` in any job reading
history, and `pull-requests: write` on that job — the first permission beyond read in a repository
whose rule is least-privilege per job ([specs](/specs/17-secrets-and-access.md)). No PAT.

### Translation

**Translation is transposition, not adaptation**
([decision](/conventions/13-translation-authoring.md)). The mechanism — mirror paths, generated
stubs, inherited stamps — is decided in [specs](/specs/09-bilingual-mechanism.md); the authoring
rules are:

- **Same path, same headings, same order.** The heading-order check applies to a `fr/` page against
  its original, not only against the template.
- **No FR-only content and no FR-only omissions within a translated page.** A page is translated
  whole or absent — the generated stub covers absent. This is what makes *gaps yes, contradictions
  no* mechanically true.
- **Identifiers are never translated**: brick and contract names, field names, commands, code
  blocks and their comments. Only prose is translated.
- **Technical vocabulary follows the glossary's French column**; a translator inventing a French
  term adds it to the glossary in the same PR.
- **Stamps are inherited, never re-earned.** The translator did not read the code; re-stamping a
  translation would assert a verification that did not happen.
- **The original changes first.** An error found while translating is fixed in `en/` and then
  translated — never fixed only in French.

## Git & PRs

**Commit types are re-aimed at the wiki as the product**
([decision](/conventions/04-commit-convention.md)) — `docs:` on every commit in a documentation
repository carries no information:

| Type | Means |
|---|---|
| `feat:` | a new page, section or contract entry; a new tooling capability |
| `fix:` | corrects something **wrong** — a false claim, a broken link, a bug in `tools/` |
| `content:` | fills or deepens an existing page without changing its structure |
| `chore:` | CI, dependencies, pins, layout shell |
| `refactor:` | moves or restructures without changing meaning — always paired with an alias ([specs](/specs/15-content-moves.md)) |
| `test:` | fixtures and tests under `tools/` |

`content:` is non-standard, and exists because this repository's most common commit — a placeholder
became prose — is neither a feature nor a fix. Scope is optional and disambiguates only
(`feat(tools):` vs `feat(bricks):`). Imperative subject, no trailing period.

**A commit that changes a `verified` stamp names the version read in its body**, so the history of
what was verified stays greppable.

One branch per issue, `issue-<n>-<slug>`, short-lived; a PR closes exactly one issue via
`Closes #<n>`. **PR sizing and grouping are not decided here** — they belong to `split-epics` and
`create-issues`, and a line target restated here would be a second source of truth for a number
those skills own ([decision](/conventions/05-pr-size-and-unit.md)). The one constraint they need
from this document is that a content page is not split across PRs.

### Review & merge

**Green CI is the only gate** ([decision](/conventions/06-review-and-merge.md)). No approval is
required on any area, `tools/` and `templates/` included; self-merge is permitted wherever the
checks pass, and `implement-epic` merges its own PRs without pausing. `main` stays protected: no
force-push, no direct push, CI green required.

The checklist below is therefore a **self-checklist**, run by whoever opens the PR, and is what the
CI cannot see. It goes into the M2 page as the contributor's own review checklist:

1. Is every claim verifiable against the code as it is today?
2. Do the citations name what was actually read — repo, path, version?
3. Does the maturity marker match reality, not intent?
4. Does the page contradict the owning repo's docs on the same subject (criterion 5)?
5. Does it read like the rest of the wiki — template order, glossary terms, voice?

The trade, stated plainly: criterion 1 now has no human gate. A page asserting something untrue
merges the moment the build is green. What follows is not optional — **every convention that can
become a check must become one**, and the weekly staleness issue is the after-the-fact review. If a
false claim reaches the site and no check could have caught it, the answer is a new check; only if
none is possible, an approval requirement on that area.

## Testing & enforcement

**Test-first applies to `tools/`, strictly; the CI check suite is the content's test suite**
([decision](/conventions/03-tdd-scope.md)).

- **Every validator rule starts as a failing fixture** — a small markdown file under
  `tools/testdata/` the rule must reject, committed in the same PR, red before green. *A rule with
  no fixture is not merged.*
- Golden files for the generator's five surfaces; the staleness job's version comparison
  unit-tested with the GitHub client faked at the boundary. Mock only true externals.
- **Content carries no unit tests.** Its equivalent is the check suite below and the
  self-checklist. Adding a rule to the wiki is a `tools/` change with a fixture, not a paragraph in
  a style guide — *drift is caught by tests, not by discipline*, applied to this repository itself.
- The consequence, worth naming to contributors: **a convention nobody can write a fixture for is a
  checklist item, and is weaker than one that has one.**

What CI holds, on every PR — the six checks from [specs](/specs/12-ci-checks.md), plus what these
conventions add:

| Check | Added by |
|---|---|
| `hugo --gc --minify`, warnings fatal | specs |
| OKF conformance; front matter validator; portability; generated blocks; internal links | specs |
| `gofmt -l`, `golangci-lint`, `go test ./tools/...` | conventions |
| Required headings, presence and order, per `type` | conventions |
| Banner ⟺ `maturity: provisional`, both directions | conventions |
| Gap block ⟺ `doc_state`, both directions | conventions |
| Citation shape, and citation versions vs `verified.version` | conventions |
| Capitalized brick spellings *(warning)* | conventions |
| Stamp coverage vs git history *(non-blocking PR comment)* | conventions |

## Error handling

Applies to `tools/`.

- Fail fast; never swallow an error silently — handle it meaningfully or propagate it with context
  added.
- Error messages state what was being attempted, not just what broke. A validator failure names the
  file, the rule and what would satisfy it: its audience is someone who just wrote a page and needs
  to know what to change.
- Tooling failures gate merges, never the published site ([specs](/specs/13-tooling-language.md)).

## Dependencies

- Prefer the standard library; a new dependency needs a one-line justification in the PR that adds
  it. SPECS already bounds this to a YAML parser and a GitHub API client.
- **Pin or lock everything the ecosystem lets you lock** — the Hugo version, the Hextra module, the
  Actions. Dependabot watches the Actions.

## Documentation & comments

- Code comments only for constraints the code can't show — invariants, workarounds with links,
  non-obvious *why*. Never narration of the next line.
- A validator rule's comment says **which convention it enforces**, linking the section of this
  document. A rule whose reason is unfindable gets deleted by someone eventually.
- Every substantive document produced while working lands in the OKF bundle, not in scattered
  ad-hoc markdown.
