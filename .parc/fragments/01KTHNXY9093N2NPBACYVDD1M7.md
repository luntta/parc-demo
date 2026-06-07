---
id: 01KTHNXY9093N2NPBACYVDD1M7
type: decision
title: PostgreSQL as the primary datastore
tags:
- architecture
- database
links: []
status: accepted
created_at: 2026-06-07T18:36:10Z
updated_at: 2026-06-07T18:36:10Z
---

Context: need a relational store with strong consistency, JSON support, and mature RLS for our multi-tenant model.

Decision: PostgreSQL (managed, e.g. RDS/Cloud SQL) as the system of record. Use jsonb for flexible per-tenant settings, and lean on RLS for isolation.

Consequences: ties us to Postgres-specific features (RLS, jsonb operators), which is an acceptable trade for the isolation guarantees. Analytical workloads will later need a separate OLAP path rather than hammering the primary.