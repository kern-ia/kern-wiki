---
type: Decision
title: "Bilingual mechanism"
description: "How do EN and FR coexist — translation linking, the language switch, and what happens on an untranslated page?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 09
slug: bilingual-mechanism
status: decided
verdict: "Explicit fallback — a generated 'not translated yet' stub, never a silent English page"
decided_via: triage
depends_on: [site-generator, content-tree, links-and-urls]
---

# Question

The site is bilingual EN/FR with English as the source language; no French page exists without an
English original, and M5 translates **front-door pages only** — deliberately not the per-brick
technical sections while the packages move ([decision](/scope/05-content-language.md)).

So the French tree is *permanently and intentionally partial*. The mechanism has to make that
state legible rather than looking like a broken site. The decision is due now, at M1, even though
French lands at M5: it constrains the content tree and the URL shape, and retrofitting is exactly
the file-moving scope forbade.

# Options

- **No fallback** — a page absent in French is simply not in the French navigation, and the
  language switch is disabled on pages with no counterpart. Honest; a reader browsing in French
  can hit a wall with no explanation.
- **Silent fallback to English** — Hugo can serve the English page under the French tree. The
  site looks complete and lies about it: a French reader sees English content with no signal, and
  worse, a *stale* English page can outlive its French translation invisibly. Against the
  project's one non-negotiable ([decision](/scope/13-non-goals.md)).
- **Explicit fallback** — the French navigation shows the page, the switch always works, and the
  French URL serves a short French stub stating "not translated — here is the English original",
  linking through. Complete navigation, no invented content, no illusion.

# Recommendation

**Explicit fallback**, built on Hugo's core multilingual mode with per-language `contentDir`
([decision](/specs/04-content-tree.md)).

- **Translation linking by mirrored path**: `/fr/bricks/kern-orch.md` is the translation of
  `/en/bricks/kern-orch.md`. No `translationKey` needed while paths mirror; it becomes the escape
  hatch if a page is ever renamed in one language only.
- **The language switch is always present** and always lands on the same subject — the whole
  point of switching mid-read.
- **Untranslated pages get a generated stub** at build time, from a layout rather than a
  committed file: nobody hand-writes fifty "pas encore traduit" pages, and the stub can never
  drift from reality. This is the one place a build-time template is right, because the artefact
  is a signpost, not content — and because a committed stub would be an OKF concept document
  asserting nothing, which is the empty-plausible-page failure mode
  ([decision](/specs/23-okf-conformance.md)).
- **Translation drift is a lint, not a hope**: the validator flags a French page whose English
  original changed after it was last touched (git dates), and flags any French page with no
  English original at all — the rule scope stated.

The FR tree carries **no** `verified` stamps of its own; a translation inherits its original's
stamp. Two stamps for one fact is [the drift](/specs/05-page-metadata.md) we already refused.

Gaps between languages are acceptable; contradictions are not — this mechanism is that sentence
made operational.

# Verdict

**Explicit fallback**, accepted at triage. Translations link by mirrored path, the language switch
is always present and always lands on the same subject, and an untranslated page serves a generated
French stub pointing at the English original. Translations inherit their original's version stamp
rather than carrying a second one, and translation drift is a lint rather than a hope.
