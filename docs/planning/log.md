# Log

## 2026-08-01

* **Creation**: [CONVENTIONS.md](/CONVENTIONS.md) written from the decided set after user
  confirmation — the personal baseline (`baseline_version: 2026-07-20`) filtered by the stack and
  merged with 13 project decisions. Unlike scope and specs, the ledger enumerates only deviations
  and gaps: [conventions decision ledger](/conventions/index.md), 13 decided, 0 open. Two verdicts
  re-weighted the rest. [Review](/conventions/06-review-and-merge.md) made **green CI the only
  merge gate** — no approval anywhere, the reviewer checklist surviving as a self-checklist —
  which turned [placeholder phrasing](/conventions/09-placeholder-phrasing.md) and
  [stamping](/conventions/12-stamping-and-done.md) from wording decisions into tooling ones, since
  a convention that isn't a check is now held by the person who would break it. And
  [PR size](/conventions/05-pr-size-and-unit.md) **removed a subject from the document**: sizing
  and grouping belong to `create-issues`, so only "a content page is not split across PRs" is kept
  — a rationale that is not project-specific and is recorded as a candidate for promotion into the
  baseline itself.
* **Update**: two deep-dives changed their own recommendation. The maturity banner was cut from
  three states to **one** — `provisional` only, because `planned` pages are already made entirely
  of gap blocks and `works-today` needs no announcement — and moved from a Hugo-rendered block to
  literal markdown, since a build-time banner is invisible on GitHub where every page must stay
  readable. And stamp granularity was answered by **git rather than by front matter**: the commit
  that last set `verified` makes `git diff <that-commit>..HEAD` the exact re-reading list, which
  narrows the work without narrowing the stamp's scope, reported as a non-blocking sticky PR
  comment. Three new obligations land in M1 as a result: `fetch-depth: 0`,
  `pull-requests: write` on one job, and four additional validator rules with their fixtures.

* **Creation**: [SPECS.md](/SPECS.md) written from the decided set after user confirmation — Hugo
  (extended) + Hextra, the repository itself an OKF v0.1 bundle with language trees at `en/` and
  `fr/`, one bundle-relative link form resolved by a custom render hook, typed front matter as the
  data model, GitHub Pages via Actions, and the OKF/validator/link checks landing in M1 rather than
  M4. Two weaker options accepted deliberately and recorded as such: artifact-only PR previews, and
  Hextra's single-maintainer bus factor — the latter bounded by content carrying no theme-specific
  syntax.

## 2026-07-31

* **Creation**: specs decision ledger enumerated at [/specs/index.md](/specs/index.md) — 17 open
  decisions and 5 recorded as N/A, covering the full specs checklist plus project-specific items
  (markdown portability contract, registries & generated tables, bilingual mechanism, diagrams,
  content moves). Scope was read as input rather than re-asked; no intake questions were needed.
  Two facts drove the generator recommendation and were verified rather than recalled: Hextra
  renders Mermaid from plain ` ```mermaid ` fences and ships offline FlexSearch with no Node
  dependency, and `mkdocs-static-i18n` — the i18n layer Material for MkDocs would have needed —
  is frozen as-is because MkDocs core upstream is unmaintained. Awaiting triage.
* **Update**: user constraint added before triage — **the wiki's own markdown must be an OKF
  bundle**, recorded as a cross-cutting decision
  ([OKF conformance](/specs/23-okf-conformance.md)). Two structural collisions with Hugo were
  found and resolved rather than papered over: `index.md` is reserved by OKF *and* turns a Hugo
  directory into a leaf bundle that unpublishes its siblings; and `/`-prefixed links resolve
  against the bundle root in OKF but the repository root on GitHub. Both are answered by making
  the repository root the bundle root, moving the language trees to `en/` and `fr/`, and keeping
  listings in `_index.md` section pages. Refreshed accordingly:
  [content tree](/specs/04-content-tree.md) and [links](/specs/07-links-and-urls.md) rewritten
  (the link form changed from relative to bundle-relative, which costs a custom render hook),
  [page metadata](/specs/05-page-metadata.md) re-based on OKF core fields with `resource` now
  feeding [the staleness job](/specs/14-freshness-automation.md), and
  [markdown contract](/specs/03-markdown-contract.md),
  [registries](/specs/06-registries-and-tables.md),
  [bilingual](/specs/09-bilingual-mechanism.md), [CI](/specs/12-ci-checks.md),
  [tooling](/specs/13-tooling-language.md), [content moves](/specs/15-content-moves.md) and
  [storage](/specs/22-database-and-storage.md) amended.
* **Update**: first triage pass — 17 accepted as recommended, 1 flagged for discussion
  ([theme](/specs/02-theme.md)). [Search](/specs/10-search.md) is recorded as decided but
  contingent on that verdict: its substance (offline, client-side, per-language, no hosted
  service) holds regardless, while the engine named in it does not.
* **Update**: [theme](/specs/02-theme.md) deep-dived and decided — **Hextra**, version-pinned as a
  Hugo Module. The decision had narrowed by the time it was examined: with theme shortcodes
  banned and the link hook and translation stub layout already ours, the theme supplies only
  navigation, search, the language switch and dark mode. Its bus-factor risk was accepted because
  content carries no theme-specific syntax, so a swap touches `layouts/` and no content file.
  [Search](/specs/10-search.md) refreshed — its contingency resolves to Hextra's built-in
  FlexSearch. **Ledger closed: 18 decided, 5 n/a, 0 open.**

## 2026-07-30

* **Creation**: bundle established. Scope decision ledger enumerated at
  [/scope/index.md](/scope/index.md) — 18 open decisions covering the full scope
  checklist plus project-specific items (governance files, contract registry home,
  naming consistency, freshness), and 1 recorded as N/A
  ([module-path migration](/scope/19-module-path-migration.md)). Context gathered by
  reading the five `kern-ia` repos rather than by interview. Awaiting triage.
* **Update**: first triage pass. 14 decisions accepted, 4 with user amendments —
  [language](/scope/05-content-language.md) split (English source, bilingual site),
  [source of truth](/scope/06-source-of-truth.md) **reversed** to a self-contained wiki,
  [coverage](/scope/07-coverage-depth.md) deepened to per-brick technical documentation,
  [governance](/scope/08-governance-content.md) cut to out-of-scope. Dependents refreshed
  accordingly: J6 added to [journeys](/scope/11-core-journeys.md),
  [MVP](/scope/12-mvp-cut.md) rescoped, "zero duplicated prose" replaced in
  [success criteria](/scope/14-success-criteria.md),
  [freshness](/scope/16-freshness-and-versioning.md) rebuilt around visible staleness,
  [milestones](/scope/17-milestones.md) 3 → 5, [risks](/scope/18-risks-and-assumptions.md)
  reordered around content drift.
* **Update**: read `kern-orch-kern-link-compat.md` (external analysis, Kern-Orch v0.2.0 ×
  kern-link v0.1.1). Two consequences: [contracts](/scope/09-contract-registry-home.md)
  reframed into an enforced class (orch→ui, CI-asserted) and a provisional unenforced class
  (orch→agent CLI, five extensions pending); and a new decision
  [documenting the gap](/scope/20-documenting-the-gap.md) — the `kern-agent` bridge does not
  exist, so no LLM runs in a graph today, which the front door must not hide.
* **Update**: second triage pass, and the project's shape changed. Three facts from the user:
  contracts will keep accumulating as packages arrive (a fifth is in progress); **v1 is the
  structure**, filled progressively, with placeholders and never invented content; and there are
  **two contributors, more expected**. Consequences:
  [contracts](/scope/09-contract-registry-home.md) decided as a growing registry with a per-brick
  exposed/needs block, [the gap](/scope/20-documenting-the-gap.md) decided as
  target-architecture-with-placeholders, `.github` confirmed untouched (so no org profile
  README — [hosting](/scope/04-hosting-and-location.md),
  [non-goals](/scope/13-non-goals.md)), and
  **[constraints](/scope/15-constraints.md) reopened**: the solo-maintainer premise was wrong
  and load-bearing, re-based on cross-contributor consistency. Refreshed downstream:
  [MVP](/scope/12-mvp-cut.md) rebuilt as a 13-deliverable frame,
  [milestones](/scope/17-milestones.md) reordered so conventions precede bulk writing,
  [success criteria](/scope/14-success-criteria.md) re-based on truthfulness/extensibility/
  uniformity instead of coverage, [freshness](/scope/16-freshness-and-versioning.md) extended to
  three page states, [coverage](/scope/07-coverage-depth.md) amended to progressive depth.
* **Update**: ledger closed — 19 decided, 1 n/a, 0 open — and [SCOPE.md](/SCOPE.md) written from
  the decided set after user confirmation. Five milestones: The frame · Conventions &
  contribution surface · Progressive package documentation · Project map & freshness · French
  edition. One fact still unknown and deliberately left open in the scope: the name and role of
  the fifth package in progress.
