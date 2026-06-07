---
id: 01KTHP0VPD6A1W4Q39VAV2S07A
type: idea
title: Per-tenant analytics via change-data-capture into an OLAP store
tags:
- database
- analytics
links:
- 01KTHNXY90
status: raw
created_at: 2026-06-07T18:37:46Z
updated_at: 2026-06-07T18:37:46Z
---

Stream Postgres CDC into a columnar warehouse so we can offer customer-facing analytics and run internal reporting without loading the primary. Keeps OLTP and OLAP separate as flagged in the Postgres decision.