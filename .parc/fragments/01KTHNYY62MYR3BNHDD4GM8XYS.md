---
id: 01KTHNYY62MYR3BNHDD4GM8XYS
type: risk
title: Signing-key compromise breaks the tenant boundary
tags:
- auth
- security
links:
- 01KTHNXY9V
impact: high
likelihood: low
mitigation: Store signing key in a managed KMS/secret manager, never in code or env files; scheduled key rotation with overlapping kid-based verification; short access-token TTL to bound a leaked key's window.
status: mitigating
created_at: 2026-06-07T18:36:43Z
updated_at: 2026-06-07T18:37:00Z
---

tenant_id is carried inside the JWT and drives RLS. If the access-token signing key leaks, an attacker can mint tokens for any tenant and read all data. The token IS the security boundary, so key management is critical and there is no second line of defence.