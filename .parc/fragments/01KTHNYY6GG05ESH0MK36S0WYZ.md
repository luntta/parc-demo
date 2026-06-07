---
id: 01KTHNYY6GG05ESH0MK36S0WYZ
type: risk
title: GDPR/PII compliance gaps (data export, deletion, residency)
tags:
- compliance
- security
links:
- 01KTHNYBTC
impact: high
likelihood: medium
mitigation: Build a data-subject-request workflow (export + cascading hard delete incl. backups/logs/Stripe); document retention; sign DPAs; plan an EU region for residency-sensitive customers.
status: identified
created_at: 2026-06-07T18:36:43Z
updated_at: 2026-06-07T18:37:00Z
---

We store customer PII without a complete data-subject-request workflow (export + hard delete across primary, backups, logs, and Stripe), no documented retention policy, and no EU data-residency option (single-region launch). Exposure to regulatory and contractual (DPA) risk as we move upmarket.