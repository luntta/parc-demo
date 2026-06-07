---
id: 01KTHNYBTCN7VJCB7857P8JVZB
type: decision
title: Single-region deployment for launch, multi-AZ for HA
tags:
- infra
links: []
status: accepted
created_at: 2026-06-07T18:36:24Z
updated_at: 2026-06-07T18:36:24Z
---

Context: must balance latency, cost, and operational simplicity at launch against future global customers.

Decision: launch in a single cloud region with multi-AZ redundancy for the database and stateless services behind a load balancer. Defer multi-region active-active until customer demand or data-residency requirements justify the complexity.

Consequences: customers far from the launch region see higher latency; a regional outage takes us down. Data-residency (EU-only) requests cannot be honoured yet.