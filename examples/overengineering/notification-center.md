# Notification Center: When Reliability Engineering Outgrew the Business Problem

## Background

An internal business application needed a unified notification center for approval reminders, tasks, announcements, inbox messages, and asynchronous email/enterprise-messaging delivery.

The real requirement was modest: important notifications should be durable and eventually visible; non-critical external channels could tolerate eventual consistency and bounded delay.

## Initial Design

The initial system already had:

- durable notification records;
- per-user inbox state;
- one real-time delivery transport;
- simple bounded retry for failed external delivery.

## How Complexity Grew

### Dual Real-Time Transports

A second transport was added for theoretical network environments where the primary one might fail.

### Transport Coordination

Dual transports introduced races, so generation counters, sequence numbers, retry counters, and transition rules appeared.

### Liveness Protection

A watchdog was added for the case where a connection looked open but stopped delivering useful data.

### Delivery Governance

Persisting delivery state for external sends was reasonable. But concerns about worker crashes, leases, recipient mismatch, and repair then added lock tokens, cursors, hashing, reconciliation, and resumable recovery.

## Warning Signs

1. User capability was still “receive notifications,” while coordination subsystems multiplied.
2. Fallback needed generation control; connection needed a watchdog; delivery state needed leases and reconciliation.
3. Governance code approached or exceeded the actual notification logic.
4. Tests started protecting retry ordering, generation counters, and watchdog timing rather than user contracts.

## Necessary Complexity

The important invariants were smaller:

- users must not read another user's notifications;
- tenant isolation must hold;
- durable notifications must not disappear silently;
- failed external delivery must be recoverable;
- large message bodies must not make list views unusable.

## Simplification

Retain:

- durable notification storage;
- user/tenant isolation;
- one real-time transport;
- bounded retry;
- targeted or manual recovery for rare failures;
- efficient summary queries and privacy-preserving delivery.

Remove or avoid without evidence:

- dual real-time transports;
- dynamic transport state machines;
- excessive revision/generation counters;
- full-dataset reconciliation when no real divergence has been demonstrated.

## Lesson

The problem was not sophisticated reliability engineering itself. The problem was that:

> **the reliability machinery became larger than the reliability requirement.**

Before escalating, ask:

> **What real failure has demonstrated that the current simpler mechanism is insufficient?**
