---
id: 01KTHP0G6Q7251QE2FM7CZX06M
type: todo
title: Centralize secrets in cloud secret manager + add CI secret scanning
tags:
- security
- infra
links:
- 01KTHNYY6Y
priority: high
status: open
created_at: 2026-06-07T18:37:34Z
updated_at: 2026-06-07T18:37:34Z
---

Move all secrets to the secret manager injected at deploy, strip secrets from repo .env files, add gitleaks/secret scanning to CI and pre-commit, document rotation.