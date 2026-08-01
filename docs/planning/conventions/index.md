# Conventions decision ledger — Kern wiki

Durable triage view. Statuses: `open` (awaiting verdict) / `decided` / `na`.

**13 decided · 0 open** — ledger closed, awaiting confirmation before CONVENTIONS.md is written.

Two verdicts re-weighted the rest. [06](06-review-and-merge.md) made green CI the only merge
gate, so a convention that isn't a check isn't enforced by anything — which is why
[09](09-placeholder-phrasing.md) and [12](12-stamping-and-done.md) became tooling decisions
rather than wording ones. And [05](05-pr-size-and-unit.md) removed a whole subject from this
document: sizing work belongs to `create-issues`, not here.

Unlike the scope and specs ledgers, this one does **not** enumerate the whole subject. The
personal conventions baseline applies by default, filtered by this project's stack; listed here
are only the **deviations** from it and the **gaps** it does not cover. Anything not listed is
settled by the baseline as written.

Two things dominate the list. First, the baseline is calibrated for a repository of code, and
here roughly all of the diff is prose — so its formatter, test-first and PR-size rules need
re-aiming rather than re-deciding. Second, the baseline says nothing about writing, and this
project's binding constraint is that several people must write the same way.

# Deviations from the baseline

* [Where the planning bundle lives](01-planning-bundle-location.md) - decided: `docs/` ships but is ignored by `.okfignore` and Hugo; CONVENTIONS.md is planning, the M2 page its rendering
* [Formatters & linters](02-formatters-and-linters.md) - decided: gofmt + golangci-lint over `tools/`; no prose linter, markdown wrapped at 100 columns
* [Where test-first applies](03-tdd-scope.md) - decided: strict red-green for `tools/`, fixture-first per rule; the CI suite is the content's test suite
* [PR size and the unit of change](05-pr-size-and-unit.md) - decided: no PR-size rule here — sizing belongs to `create-issues`; only "a page is not split across PRs" is kept

# Gaps the baseline does not cover

* [Commit convention for a content repository](04-commit-convention.md) - decided: types re-aimed at the wiki as the product, plus a `content:` type
* [Review, approval and merge](06-review-and-merge.md) - decided: green CI is the only gate, no approval anywhere; the checklist survives as a self-checklist
* [Prose style & voice](07-prose-style.md) - decided: a short rule set weighted toward truthfulness
* [Page structure, templates and where the authoring rules live](08-page-structure-and-templates.md) - decided: templates binding on section set and order; CONVENTIONS.md is the source, the M2 page a rendering
* [Placeholder and maturity phrasing](09-placeholder-phrasing.md) - decided: one literal banner, `provisional` only; verbatim gap block; validator asserts both equivalences
* [Terminology & naming in prose](10-terminology-and-naming.md) - decided: the glossary is normative from M1; one canonical spelling per thing
* [Citations discipline](11-citations-discipline.md) - decided: a citation is a path at a version, grouped by brick
* [Stamping and the definition of done](12-stamping-and-done.md) - decided: stamp covers the page; coverage derived from git, reported as a non-blocking sticky PR comment
* [Translation authoring rules](13-translation-authoring.md) - decided: translation is transposition; rules for English writers from M1

# Applying unchanged (not re-opened)

Baseline sections that survive the stack filter and need no project decision: **Naming**
(Go casing and file naming, for `tools/`), **Error handling**, **Dependencies** (stdlib-first,
pin everything — already echoed by SPECS), **Documentation & comments**, and the parts of
**Git & PRs** not listed above (conventional-commit grammar, `issue-<n>-<slug>` branches,
`Closes #<n>`, CI green before merge, no force-push to `main`).

Dropped by the stack filter: the JS/TS, Python and Rust formatter and casing variants, and the
visual-fidelity testing carve-out (no UI code in this repository).
