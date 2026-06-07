---
id: 01KTHNXY7H1ERXV9DXC9C6YDR5
type: decision
title: 'Multi-tenant architecture: shared DB with row-level security'
tags:
- architecture
- database
links: []
status: accepted
created_at: 2026-06-07T18:36:10Z
updated_at: 2026-06-07T18:36:10Z
---

Context: we need to serve many business customers cost-effectively while keeping a single deployable codebase. Options considered: (1) database-per-tenant, (2) schema-per-tenant, (3) shared schema with a tenant_id column enforced by Postgres Row-Level Security (RLS).

Decision: go with shared schema + RLS. Every tenant-scoped table carries tenant_id; RLS policies bind queries to the current tenant via a session GUC set per request. This keeps migrations and ops simple at our scale while giving a hard, database-enforced isolation boundary.

Consequences: all app DB connections must set the tenant context; connection pooling must not leak context between requests. Noisy-neighbor and per-tenant data export are harder than database-per-tenant. Revisit if a customer requires physical isolation for compliance.