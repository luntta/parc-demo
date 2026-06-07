---
id: 01KTHNXY9G5MRHA2HHH076JN1J
type: decision
title: Stripe for billing and subscription management
tags:
- billing
links: []
status: accepted
created_at: 2026-06-07T18:36:10Z
updated_at: 2026-06-07T18:36:10Z
---

Context: we need subscriptions, proration, invoicing, tax handling, and dunning without building a billing engine.

Decision: use Stripe Billing as the source of truth for subscription state. Map Stripe customer/subscription objects to internal tenant/plan records, synced via webhooks. Stripe Checkout for self-serve signup, Customer Portal for plan changes.

Consequences: billing state lives outside our DB and is eventually consistent via webhooks; we must reconcile. Hard dependency on Stripe availability for signup/upgrade flows.