---
id: 01KTHNYBSGX38QS49PRQEQ6967
type: decision
title: Asynchronous work via a managed queue and background workers
tags:
- architecture
- infra
links:
- 01KTHNXY9G
status: proposed
created_at: 2026-06-07T18:36:24Z
updated_at: 2026-06-07T18:36:24Z
---

Context: webhook processing, email, exports, and usage aggregation should not block request threads.

Decision: introduce a managed queue (SQS / Cloud Tasks) with idempotent worker handlers. Stripe webhooks, transactional email, and CSV exports run as jobs. Each job carries tenant_id so workers can set RLS context.

Consequences: adds an async failure surface (DLQs, retries, poison messages) and requires idempotency keys everywhere. Eventual consistency between user action and side effect must be reflected in the UI.