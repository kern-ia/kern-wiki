# Specs decision ledger — Kern wiki

Durable triage view. Statuses: `open` (awaiting verdict) / `decided` / `na`.

**18 decided · 0 open · 5 n/a** — ledger closed, awaiting confirmation before SPECS.md is written.

Dependency order: the generator decides the toolchain, the toolchain decides most of the rest.
OKF conformance is listed first because it is a user constraint that cuts across the content
decisions rather than sitting beside them; its file number is 23 because it arrived after the
ledger was enumerated.

# Cross-cutting constraint

* [OKF conformance for wiki content](23-okf-conformance.md) - decided: repo root is the bundle root, no `index.md` inside the content trees, `_index.md` sections carry generated listings, `# Citations` on technical pages

# Decisions

* [Site generator & build runtime](01-site-generator.md) - decided: Hugo, extended edition, version-pinned in CI and locally
* [Documentation theme & site shell](02-theme.md) - decided: Hextra as a version-pinned Hugo Module; no theme shortcodes in content, overrides confined to `layouts/`
* [Markdown portability contract](03-markdown-contract.md) - decided: CommonMark + GFM only, mandatory OKF frontmatter, mechanically enforced
* [Content tree & repository layout](04-content-tree.md) - decided: language trees at the repo root (`en/`, `fr/`) as per-language contentDir, six fixed sections, `_index.md` in every directory
* [Page metadata schema](05-page-metadata.md) - decided: OKF core plus typed extensions (`maturity`, `doc_state`, `verified`, `exposes`/`needs`); `resource` feeds the staleness job; staleness derived, never authored
* [Registries & generated tables](06-registries-and-tables.md) - decided: committed generated markdown on five surfaces, regenerate-and-diff in CI
* [Links, URLs & permalinks](07-links-and-urls.md) - decided: bundle-relative `/en/…md` links via a custom link render hook; `/{lang}/{section}/{page}/`
* [Diagrams](08-diagrams.md) - decided: Mermaid fenced blocks only; dashed edges mean planned or missing
* [Bilingual mechanism](09-bilingual-mechanism.md) - decided: explicit fallback — a generated "not translated yet" stub, never silent English
* [Search](10-search.md) - decided: Hextra's built-in FlexSearch, one index per language, placeholders indexed
* [Hosting & deployment pipeline](11-hosting-and-deployment.md) - decided: Actions → `actions/deploy-pages` on `main`; build + artifact preview on every PR
* [CI checks & testing infrastructure](12-ci-checks.md) - decided: build + OKF conformance + validator + internal links from M1; external links and staleness scheduled; no prose linter
* [Repository tooling language](13-tooling-language.md) - decided: Go, one binary in `tools/` with `validate` / `gen` / `stale`
* [Freshness automation (staleness job)](14-freshness-automation.md) - decided: weekly, latest release with commit-count fallback, one rolling issue, never auto-stamps
* [Content moves & redirects](15-content-moves.md) - decided: Hugo `aliases`, kept permanently, missing alias on a rename fails CI
* [Observability & analytics](16-observability-and-analytics.md) - decided: no analytics; CI failure, link check and the staleness issue are the health signals
* [Secrets & cross-repo access](17-secrets-and-access.md) - decided: `GITHUB_TOKEN` only, least-privilege per job, no PAT

# Not applicable

* [Auth & authorization](18-auth.md) - na: public static site; write access is GitHub repo permissions + PR review
* [External integrations](19-external-integrations.md) - na: only GitHub itself and outbound links; fallbacks decided in 11, 12, 14
* [Performance & scale targets](20-performance-and-scale.md) - na: pre-rendered static pages on a CDN; the only budget that matters is the 15-minute human one
* [Background work](21-background-work.md) - na: no runtime; the two cron workflows are decided in 12 and 14
* [Database & persistent storage](22-database-and-storage.md) - na: git is the store, the OKF bundle is the schema — see 05, 06 and 23
