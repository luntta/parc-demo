---
id: 01KTHP0G3TR10KJ29KY2AQ71BC
type: todo
title: Put PgBouncer / RDS Proxy in front of Postgres
tags:
- database
- infra
links:
- 01KTHNYY5M
due: 2026-06-30
priority: high
status: open
created_at: 2026-06-07T18:37:34Z
updated_at: 2026-06-07T18:37:34Z
---

Transaction-mode pooling to survive connection bursts from serverless functions. Add statement_timeout and per-service pool caps. Validate with a load test.