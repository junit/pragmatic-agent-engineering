# Distributed Systems Playbook

Use this playbook for coordination across processes, nodes, services, networks, or storage systems.

Goal:

> **Accept distributed-system complexity only when real requirements require it, and make partial failure explicit.**

## Scope

Service calls, messaging, distributed jobs, multi-node execution, distributed locks, replication, cross-system writes, cluster coordination, asynchronous events, and backpressure.

## Hard Constraints

1. **Network calls can fail.** Model timeout, connection failure, duplicate delivery, delayed response, and partial success.
2. **Multi-component operations must consider partial failure.** Do not design only the all-success path.
3. **Duplicate execution needs defined semantics.** Messaging, jobs, and retries must define whether duplicates are acceptable and how correctness is preserved.
4. **Backpressure needs explicit business semantics.** When capacity is exhausted, choose intentionally among wait, reject, drop, degrade, persist, or retry.

## Default Heuristics

- Prefer local/single-node/single-store solutions while they meet real requirements.
- Minimize shared state and coordination before introducing more locks and protocols.
- Prefer idempotent operations where network retries are unavoidable.
- Avoid distributed transactions by default; first examine business boundaries, eventual consistency, and local compensation.
- Make ownership explicit: which system has final authority over a state?

## Escalation Conditions

Introduce distributed locks, leader election, consensus, cross-system reconciliation, complex compensation, or multi-region coordination only with concrete evidence such as unavoidable competition for an indivisible resource, hard availability requirements, high failure cost, or proof that simpler partitioning/ownership does not solve the problem.

## Warning Signs

- A distributed lock requires renewal, watchdogs, and compensation.
- Several systems all maintain the same shared state.
- Simple business behavior needs a complex coordination protocol.
- Every additional node creates new synchronization rules.
- Recovery/governance code dwarfs business logic.

## Verification

Based on risk, verify timeouts, duplicates, delayed responses, node restarts, partial failures, retries, redelivery, backpressure, capacity exhaustion, and recovery. Prioritize high-probability, high-impact, or irreversible failures.

Final question:

> **Does the distributed mechanism solve a problem that a simpler ownership or execution model genuinely cannot?**
