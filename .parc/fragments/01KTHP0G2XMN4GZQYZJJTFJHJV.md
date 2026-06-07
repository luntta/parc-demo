---
id: 01KTHP0G2XMN4GZQYZJJTFJHJV
type: todo
title: Implement Stripe webhook signature verification + idempotent event log
tags:
- billing
links:
- 01KTHNYY58
due: 2026-06-15
priority: high
status: in-progress
created_at: 2026-06-07T18:37:34Z
updated_at: 2026-06-07T18:37:34Z
---

Persist raw Stripe events keyed by event id, verify signatures, and make handlers idempotent. Prereq for the reconciliation job.