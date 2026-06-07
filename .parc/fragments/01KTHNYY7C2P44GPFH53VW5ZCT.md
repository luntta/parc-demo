---
id: 01KTHNYY7C2P44GPFH53VW5ZCT
type: risk
title: Single-region outage takes the whole product down
tags:
- infra
links:
- 01KTHNYBTC
- 01KTHP0VNREX6J7NKDC65Y95H0
- 01KTHP0VP3Y6K2FRHT8Q05FH8G
impact: high
likelihood: low
mitigation: Accepted for launch. Multi-AZ DB with automated failover; documented RTO/RPO; tested restore procedure; revisit multi-region when an SLA or data-residency contract requires it.
status: accepted
created_at: 2026-06-07T18:36:43Z
updated_at: 2026-06-07T18:38:43Z
---

Launch is single-region. A regional cloud outage, or a bad DB failover, means full downtime for every tenant with no failover region. RTO depends on manual intervention.