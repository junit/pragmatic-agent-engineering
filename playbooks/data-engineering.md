# Data Engineering Playbook

Use this playbook for ingestion, synchronization, transformation, batch/stream processing, and data pipelines.

Goal:

> **Protect data semantics, traceability, and recoverability first; add parallelism and distributed state only as real scale requires.**

## Scope

ETL/ELT, CDC, batch/stream pipelines, synchronization, cleaning, transformation, data quality, backfill, and scheduling.

## Hard Constraints

1. **Data semantics must be explicit.** Define source, meaning, key/uniqueness, time semantics, update semantics, and delete semantics.
2. **Do not silently lose data.** Do not hide dropped records, fields, parse failures, or exceptions merely to keep a pipeline running; intentional drops require explicit policy and observability.
3. **The source of truth must be clear.** Distinguish authoritative upstream data, intermediate state, and derived downstream data.
4. **Schema evolution requires semantics.** Add, drop, rename, and type changes need explicit downstream behavior; do not rely on “the framework handles it” as the contract.

## Default Heuristics

- Correctness before throughput.
- Choose the minimum delivery semantics that satisfy real requirements for duplicates, delay, recomputation, deduplication, and loss recovery.
- Prefer recomputable derived pipelines when economically reasonable.
- Make replay/retry/backfill boundaries idempotent where practical.
- Treat event time, processing time, business date, time zone, late data, and out-of-order data explicitly.
- Increase parallelism/partitions/workers/batch size based on measured bottlenecks.
- Separate data quality from pipeline availability; a running pipeline can still have degraded data quality.

## Escalation Conditions

More complex checkpoints, state backends, reconciliation, compensation, or partitioning may be justified by demonstrated data scale limits, strict latency, high-value non-loss requirements, heavy out-of-order data, large replay, multi-source merging, cross-system consistency, or long-lived stateful computation.

## Warning Signs

- Data meaning is unclear while technical state keeps growing.
- Errors are swallowed to keep jobs green.
- The same data has multiple authorities.
- A simple synchronization job has a complex recovery protocol.
- Parallelism grows without performance evidence.
- Data-quality failures are confused with system-availability failures.

## Verification

Verify input/output counts, uniqueness, update/delete semantics, schema changes, replay/retry, restart recovery, late data, data quality, and before/after performance where relevant.

Critical question:

> **If the pipeline ran again today, would the result remain correct and explainable?**
