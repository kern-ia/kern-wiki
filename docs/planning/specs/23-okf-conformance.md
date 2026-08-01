---
type: Decision
title: "OKF conformance for wiki content"
description: "The wiki's markdown must be an OKF v0.1 knowledge bundle — where is the bundle root, and how does that coexist with Hugo?"
tags: [decision, specs, cross-cutting]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 23
slug: okf-conformance
status: decided
verdict: "Repository root is the bundle root; no index.md inside the content trees; `_index.md` section pages carry generated listings"
decided_via: triage
depends_on: [markdown-contract, content-tree, page-metadata, links-and-urls]
---

# Question

User constraint, given before triage: **the wiki's markdown must follow OKF** (Open Knowledge
Format v0.1) — the same format the planning bundle already uses. This is cross-cutting: it is an
input to decisions 03–07 and 12–14 rather than a decision that sits beside them, which is why it
is recorded once here and the affected docs are refreshed against it.

OKF conformance itself is three rules: every non-reserved `.md` file opens with parseable YAML
frontmatter containing a non-empty `type`; `index.md` and `log.md` are reserved for directory
listings and history; `log.md` date headings are `## YYYY-MM-DD`, newest first. Everything else
— `title`/`description`/`tags`/`timestamp`/`resource`, the `# Citations` convention,
bundle-relative links — is strong convention.

Two of those rules collide with Hugo head-on, and both collisions are structural rather than
cosmetic:

1. **`index.md` is reserved by OKF and load-bearing in Hugo.** In Hugo, a directory containing
   `index.md` is a *leaf bundle*: its sibling `.md` files stop being pages and become attached
   resources. An OKF listing dropped into `en/bricks/` would silently delete every brick page
   from the site.
2. **`/`-prefixed links mean different things.** OKF resolves `/tables/x.md` against the **bundle
   root**; GitHub resolves it against the **repository root**. They agree only if the bundle root
   *is* the repository root.

# Options

**Where the bundle root sits:**

- **Per-language bundles** (`content/en/` as a bundle root) — two bundles, and `/bricks/x.md`
  resolves to a non-existent repo-root path on GitHub. Breaks the fallback that
  [the markdown contract](/specs/03-markdown-contract.md) exists to guarantee.
- **`content/` as the bundle root** — one bundle, and `/en/bricks/x.md` still misses on GitHub,
  which looks for `<repo>/en/bricks/x.md`.
- **The repository root as the bundle root**, with the language trees at `en/` and `fr/` and a
  `.okfignore` excluding everything that is not knowledge (`layouts/`, `static/`, `data/`,
  `tools/`, `templates/`, `.github/`, `README.md`, config). Then `/en/bricks/kern-orch.md` means
  the same file to OKF, to GitHub, and to a human reading the tree.

**How to satisfy OKF's listings without breaking Hugo:**

- **Per-directory `index.md` + Hugo exclusion** (`ignoreFiles`, or `module.mounts` `files` globs
  since Hugo 0.153). Two files per directory with overlapping purpose, and it rests on Hugo's
  bundle classifier honouring the exclusion — plausible, undocumented, and a bad thing to be
  wrong about.
- **No `index.md` inside the content trees.** OKF makes per-directory `index.md` *optional*
  (§6; conformance explicitly forbids rejecting a bundle for missing index files). Hugo's section
  pages `_index.md` are ordinary non-reserved concept documents — they take OKF frontmatter like
  any other page — and carry the directory listing in their body. The bundle root keeps a real
  `index.md` and `log.md` at the repository root, **outside** the Hugo content directories, so
  Hugo never sees a reserved filename at all.
- **No listings anywhere** — conformant, and throws away progressive disclosure, which is most of
  why OKF is worth adopting.

# Recommendation

**Repository root as the bundle root; no `index.md` inside the content trees; section `_index.md`
pages carry generated listings.**

Concretely:

```
kern-wiki/                     # bundle root == repo root == GitHub link root
├── index.md                   # OKF bundle listing — okf_version: "0.1", no other frontmatter
├── log.md                     # OKF history, ## YYYY-MM-DD newest first
├── .okfignore                 # layouts/ static/ data/ tools/ templates/ .github/ README.md …
├── en/                        # Hugo contentDir for English
│   ├── _index.md              # concept doc (type: Section) + generated listing block
│   └── bricks/
│       ├── _index.md
│       └── kern-orch.md
└── fr/                        # Hugo contentDir for French (M5)
```

This buys three things at once: one link form (`/en/bricks/kern-orch.md`) that is simultaneously
OKF-preferred, correct on GitHub, and resolvable by Hugo
([decision](/specs/07-links-and-urls.md)); no reserved filename anywhere Hugo looks; and a bundle
whose root listing is the same file a human or an agent would open first.

Three consequences worth stating plainly:

- **OKF is the floor, the project profile is stricter.** OKF says consumers must tolerate unknown
  keys and missing optional fields; our validator is a *producer-side* lint and will reject an
  unstamped brick page anyway ([decision](/specs/05-page-metadata.md)). Both are true at once —
  the bundle stays consumable by any OKF reader, while this repo holds its own contributors to
  more.
- **`# Citations` becomes a load-bearing convention, not decoration.** The wiki's one
  non-negotiable is no invented content ([decision](/scope/13-non-goals.md)); OKF already
  provides the place to record what was actually read to write a page. Technical pages cite the
  repo files and versions behind their claims.
- **`log.md` is for structure, not typos.** New brick page, new contract entry, template or
  convention change — not every content edit, which is what git is for. Otherwise the log
  becomes a second changelog nobody writes.

The rejected `ignoreFiles` route stays the documented fallback if per-directory `index.md` files
are ever wanted: it is one config line plus a verification spike, and it changes no content.

# Citations

[1] [OKF v0.1 spec](https://github.com/GoogleCloudPlatform/knowledge-catalog) — `okf/SPEC.md`,
    §3.1 reserved filenames, §5 cross-linking, §6 index files, §9 conformance.
[2] [Hugo — page bundles](https://gohugo.io/content-management/page-bundles/) — leaf bundle
    definition and its effect on sibling files.
[3] [Relative links in markup files](https://github.blog/2013-01-31-relative-links-in-markup-files/)
    — GitHub resolves `/`-prefixed links against the repository root.

# Verdict

**Repository root as the bundle root; no `index.md` inside the content trees; `_index.md` section
pages carry the listings.** Accepted at triage.

The wiki's markdown is an OKF v0.1 bundle, on the same terms as the planning bundle. One link form
(`/en/bricks/kern-orch.md`) is simultaneously OKF-preferred, correct on GitHub and resolvable by
Hugo; no reserved filename appears anywhere Hugo reads; `# Citations` becomes the place the
no-invented-content rule is discharged on technical pages.

The `ignoreFiles` route to per-directory `index.md` stays documented as the fallback, unverified
against Hugo's leaf-bundle classifier and deliberately not relied upon.
