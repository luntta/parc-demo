---
id: 01KTHNYY6YY6J30YJS8E7H7P45
type: risk
title: Secrets sprawl across env files, CI, and cloud
tags:
- security
- infra
links: []
impact: high
likelihood: medium
mitigation: Single source of truth in cloud secret manager injected at deploy; remove secrets from .env in repos; secret scanning in CI and pre-commit; documented rotation runbook and ownership.
status: identified
created_at: 2026-06-07T18:36:43Z
updated_at: 2026-06-07T18:37:00Z
---

DB credentials, Stripe keys, and the JWT signing key live in multiple places (local .env, CI secrets, cloud secret manager). No rotation policy and unclear ownership. A leak via a misconfigured log, a committed .env, or a CI artifact would be high-impact and hard to detect.