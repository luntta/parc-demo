---
id: 01KTHP0G3BY7XFKHFBKNYA6XTW
type: todo
title: Nightly Stripe<->DB subscription reconciliation job
tags:
- billing
links:
- 01KTHNYY58
priority: high
status: open
created_at: 2026-06-07T18:37:34Z
updated_at: 2026-06-07T18:37:34Z
---

Scheduled job that diffs Stripe subscription/plan state against local tenant records and alerts on drift. Depends on the idempotent event log.