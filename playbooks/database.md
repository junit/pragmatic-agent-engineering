# Database Playbook

Use this playbook for schemas, queries, indexes, migrations, transactions, and persistence models.

Goal:

> **Preserve data meaning and authority, and require real evidence before increasing database complexity.**

## Scope

Schemas, tables, fields, indexes, SQL, migrations, data repair, transactions, compatibility, archival, and database performance.

## Hard Constraints

1. **Data semantics come first.** Core persistence should model durable business facts, not accumulate temporary runtime coordination state without necessity.
2. **Destructive changes require explicit risk analysis.** Dropping tables/columns, changing meaning or incompatible types, large rewrites, and irreversible deletion are high-risk changes.
3. **Transaction boundaries must match business atomicity.** Do not remove necessary transactions merely for simplicity.
4. **Do not silently corrupt data.** Avoid swallowed errors, arbitrary defaults, silent truncation, and ambiguous field semantics.

## Default Heuristics

- Prefer one authoritative source for one business fact.
- Prefer simple, explicit schemas and constraints.
- Create indexes for real queries; inspect plans, cardinality/selectivity, data volume, and measured latency first.
- Prefer explicit migrations over hidden production schema mutation during application startup.
- Give compatibility windows an exit plan instead of allowing compatibility fields to become permanent by accident.

## Escalation Conditions

Consider sharding, read/write splitting, specialized stores, or complex redundancy only for demonstrated scale/performance limits, high write concurrency, massive data lifecycle needs, strict audit needs, cross-system consistency constraints, or evidence that a simpler database architecture is insufficient.

## Warning Signs

- A simple entity carries many technical coordination fields.
- The same fact is maintained independently in several tables.
- Every performance problem is addressed by adding another index.
- Compatibility fields grow without removal plans.
- Sharding or new databases are introduced without measurement.

## Verification

As relevant, verify schema shape, migration behavior, row counts, transaction failure behavior, query plans, before/after performance, data integrity, rollback, and recovery.

Final question:

> **Does the database model business truth, or historical workarounds?**
