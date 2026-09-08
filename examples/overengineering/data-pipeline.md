# Data Pipeline: When “Exactly Once Everywhere” Became the Wrong Goal

## Background

A data pipeline synchronized operational records into an analytical store.

The real requirements were:

- no silent data loss;
- eventual arrival;
- bounded delay was acceptable;
- the source remained authoritative;
- the sink supported idempotent upsert, so duplicate writes did not corrupt final state.

## Initial Design

```text
source
→ change capture
→ transform
→ idempotent sink
→ checkpoint/restart recovery
```

## How Complexity Grew

The team upgraded the goal to “exactly once at every internal stage,” adding transaction coordination, more checkpoint/transaction state, and recovery metadata. Concern about possible cross-system divergence then led toward full source/sink reconciliation, repair cursors, ownership, and repair state.

## The Missed Question

The decisive fact was:

> **The sink was idempotent, the source was authoritative, and replay was acceptable.**

The real boundary contract was closer to:

> **At-least-once delivery with correct final state**

than:

> **Every internal action executes exactly once.**

## Simplification

Design around the real invariant:

- explicit source position;
- restartable checkpoints;
- idempotent sink writes;
- bounded, observable retries;
- targeted repair or validation when evidence shows divergence.

Do not require by default:

- cross-system distributed transactions;
- continuous full reconciliation;
- permanent repair state machines.

## Verification

Focus on:

- replay safety;
- correct source position after restart;
- duplicate delivery yielding the same final state;
- observable failed records;
- absence of silent loss;
- ability to compare final source/sink state when necessary.

## Lesson

Stronger internal execution guarantees do not automatically mean stronger business correctness.

> **Define the guarantee that matters at the boundary, then choose the minimum sufficient execution semantics.**
