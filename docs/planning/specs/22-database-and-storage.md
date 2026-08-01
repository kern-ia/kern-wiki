---
type: Decision
title: "Database & persistent storage"
description: "Is there a database, and where does persistent state live?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 22
slug: database-and-storage
status: na
verdict: "N/A — no database; the git repository is the store and front matter is the schema"
decided_via: na
depends_on: [page-metadata, registries-and-tables]
---

# Question

Where does the system's data live — relational, document, files, none?

# Verdict

**N/A in the conventional sense, but not vacuous.** The store is the git repository: markdown
files, reviewed by pull request, with history — structured as an OKF knowledge bundle, which is
the closest thing this project has to a schema declaration
([decision](/specs/23-okf-conformance.md)). There is no database and nothing to migrate.

The checklist's real concern — *the structure that is expensive to change later* — is answered by
two decisions that carry the weight instead:

- **[Page metadata schema](/specs/05-page-metadata.md)** — the typed front matter that makes
  version stamps, maturity markers and contract wiring machine-readable. This is the data model.
- **[Registries & generated tables](/specs/06-registries-and-tables.md)** — how aggregate views
  are derived from it without a second copy of any fact.

The schema-evolution question that a database would raise is answered there too: unknown keys
fail the validator, vocabularies are closed sets in `data/vocab.yaml`, and changing either means a
tree-wide edit in one PR — cheap while the wiki is dozens of pages, which is another reason to
fix the schema at M1 rather than at M3.
