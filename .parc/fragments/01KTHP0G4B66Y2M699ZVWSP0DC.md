---
id: 01KTHP0G4B66Y2M699ZVWSP0DC
type: todo
title: Rate limiting on the public API
tags:
- security
- infra
links:
- 01KTHNYY5MBB634ASSVA9S4T07
priority: high
status: open
created_at: 2026-06-07T18:37:34Z
updated_at: 2026-06-07T18:38:43Z
---

Per-tenant and per-IP rate limits at the edge to protect against abuse and to bound connection/load pressure. Return 429 with Retry-After.