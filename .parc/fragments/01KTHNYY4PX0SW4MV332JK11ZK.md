---
id: 01KTHNYY4PX0SW4MV332JK11ZK
type: risk
title: Cross-tenant data leakage if RLS context is not set
tags:
- security
- database
links:
- 01KTHNXY7H
- 01KTHP0G5A9014YB39GXCNGQHX
impact: high
likelihood: medium
mitigation: Centralize all runtime DB access behind a connection wrapper that sets the tenant GUC and never uses superuser; default-deny RLS with a CI test that fails if any tenant-scoped table lacks a policy; cross-tenant integration test in the suite.
status: mitigating
created_at: 2026-06-07T18:36:43Z
updated_at: 2026-06-07T18:38:43Z
---

In the shared-schema model, isolation depends entirely on the per-request tenant_id GUC and RLS policies. A pooled connection that reuses a previous request's session context, a query path that bypasses RLS (e.g. a superuser/migration connection used at runtime), or a missing policy on a new table would leak one tenant's data to another. This is the single highest-severity failure mode of the architecture.