# parc-demo

A demonstration of [parc](https://luntta.fi/parc) — a personal archive of structured "fragments of thought" (decisions, risks, todos, ideas, notes) that lives alongside your code in a `.parc/` vault.

This repo doesn't ship an application. Instead, its `.parc/` vault has been filled with the kind of engineering knowledge a real **multi-tenant B2B SaaS** team would accumulate during its first months: architecture decisions, the risks those decisions create, the follow-up work to mitigate them, and ideas for later. The fragments are cross-linked so you can navigate from a decision to the risks it introduced to the todos that address them.

## What's inside

The vault contains **31 fragments**:

| Type | Count | What they capture |
|------|------:|-------------------|
| **decision** (ADR) | 7 | Architecture & tooling choices — shared-DB multi-tenancy with Postgres RLS, PostgreSQL, Stripe billing, JWT auth, async queue/workers, Next.js, single-region launch |
| **risk** | 7 | What could go wrong — cross-tenant data leakage, Stripe webhook/billing drift, connection-pool exhaustion, signing-key compromise, GDPR/PII gaps, secrets sprawl, single-region outage (each with likelihood, impact, and a mitigation) |
| **todo** | 12 | Concrete follow-up work — RLS CI guard, webhook idempotency, Stripe reconciliation, PgBouncer, rate limiting, backup/restore drills, audit logging, SOC 2, data-subject-request flow, secret centralization, tracing, DLQ handling |
| **idea** | 5 | Opportunities for later — metered billing, self-serve SSO, feature flags, public status page, CDC→OLAP analytics |

Most risks link back to the decision that created them, and most todos link to the risk they mitigate, so the vault reads as a connected graph rather than a flat list.

## Prerequisites

Install the `parc` CLI — see the [website](https://luntta.fi/parc) or the [GitHub repo](https://github.com/luntta/parc) for installation instructions. Then run the commands below from the repo root (the vault is discovered automatically from `.parc/`).

## Setup after cloning

The vault's fragments (`.parc/fragments/*.md`) and config are committed to git, but the search index (`.parc/index.db`) is **not** — it's a derived SQLite file and is gitignored. After cloning, build the index from the committed fragments:

```bash
parc reindex          # rebuilds .parc/index.db — reports "fragments_indexed: 31"
```

You don't run `parc init` here: that command scaffolds a brand-new, empty vault, whereas this repo already ships one — you just need its index. After reindexing, confirm everything is wired up:

```bash
parc doctor           # should report: no issues found
```

## Exploring the demo

### Browse interactively

```bash
parc tui            # full terminal UI — the best way to wander the vault
```

### Get the big picture

```bash
parc list                     # every fragment
parc review                   # multi-section digest: recent, by type, accepted decisions, open risks
parc types                    # the fragment types and their fields
parc tags                     # all tags with usage counts (infra, security, database, billing, ...)
parc doctor                   # vault health check (broken links, orphans) — should report no issues
```

### Look at one kind of thing

```bash
parc list decision            # the ADRs
parc list risk                # the risk register
parc list todo                # the backlog
parc list idea                # the idea parking lot
parc list todo --status open  # filter further by status or --tag
```

### Search (supports a small query DSL)

```bash
parc search "row-level security"          # fuzzy full-text
parc search "type:risk" --json            # all risks, machine-readable
parc search "type:todo status:open"       # open work
parc search "type:decision stripe"        # decisions mentioning Stripe
parc search "#security"                   # everything tagged security
parc search "type:risk #database"         # risks in the database area
```

### Read and follow a single fragment

```bash
parc show <id-prefix>                      # full body + metadata (8-char prefix is enough)
parc backlinks <id-prefix>                 # what links to this fragment
```

A good trail to follow: open the **"Multi-tenant architecture: shared DB with row-level security"** decision, then `parc backlinks` it to find the **cross-tenant data leakage** risk, then follow that risk's link to the **"Add CI guard: every tenant-scoped table must have an RLS policy"** todo.

### Track work over time

```bash
parc due                       # todos with due dates, soonest first
parc stale                     # open work that's gone quiet
parc today                     # the daily resurfacing digest
```

## Try editing it yourself

The vault is meant to be lived in. A few things to try:

```bash
# Add your own fragment
parc new idea "My improvement" --body "..." --tag platform

# Move a todo along
parc set <id-prefix> status in-progress

# Promote a raw idea into a decision once you've committed to it
parc promote <id-prefix> decision

# Link two related fragments
parc link <id-a> <id-b>
```

Every fragment is a plain Markdown file with YAML frontmatter under `.parc/fragments/`, so you can also read or diff them directly in git.
