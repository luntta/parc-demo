---
id: 01KTHP0G0MA4K27JZNXMHSDW08
type: todo
title: 'Add CI guard: every tenant-scoped table must have an RLS policy'
tags:
- security
- database
links:
- 01KTHNYY4P
due: 2026-06-20
priority: critical
status: open
created_at: 2026-06-07T18:37:34Z
updated_at: 2026-06-07T18:37:34Z
---

Write a test/migration check that enumerates tenant-scoped tables and fails the build if any lacks a FORCE ROW LEVEL SECURITY policy. Closes the most likely path to cross-tenant leakage when new tables are added.