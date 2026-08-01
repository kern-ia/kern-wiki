---
type: Decision
title: "Auth & authorization"
description: "Does the wiki need identity, accounts or access control?"
tags: [decision, specs]
timestamp: 2026-07-31T09:14:28Z
phase: specs
decision: 18
slug: auth
status: na
verdict: "N/A — public static site; write access is GitHub repository permissions"
decided_via: na
depends_on: [hosting-and-deployment]
---

# Question

Is there any notion of identity in this system?

# Verdict

**N/A.** The deliverable is a public static site with no server, no session and no user-specific
content ([decision](/scope/04-hosting-and-location.md)). Read access is "anyone with the URL" by
design — the wiki exists to be the front door for developers who have never heard of Kern
([decision](/scope/02-target-audiences.md)).

Write access is GitHub repository permissions on `kern-ia/kern-wiki` plus pull-request review —
already the contribution model scope chose over the GitHub Wiki tab precisely because it *has*
review ([decision](/scope/03-delivery-form.md)). Nothing here is an application-level decision.

Revisit only if the wiki ever needs to document something not publishable, which would be a scope
change, not a spec one.
