# Reliability Playbook

Use this playbook for failure handling, retries, idempotency, asynchronous execution, compensation, degradation, and recovery.

Goal:

> **Match reliability engineering to real failure cost instead of maximizing reliability everywhere.**

## Scope

External calls, background jobs, message handling, async workflows, retries, idempotency, timeouts, degradation, compensation, and recovery.

## Hard Constraints

1. **Critical failures need explicit semantics.** Define resulting state, partial success, user visibility, and recovery.
2. **Define duplicate-execution semantics before retrying.** Do not mechanically retry non-idempotent operations.
3. **External waits need bounds.** Remote or potentially long-blocking work requires reasonable timeout semantics.
4. **Do not turn every recoverable transient failure into system-wide termination.** If the business permits wait, retry, or local failure, use those semantics; security boundaries may require fail-closed behavior.

## Default Heuristics

- Escalate progressively: `direct execution → bounded retry → persistent failure state → explicit recovery → advanced compensation`.
- Retry only failures that are actually recoverable.
- Bound retries by attempts and/or total time, use backoff as appropriate, and consider downstream capacity.
- Prefer failures that are observable, diagnosable, and recoverable over opaque self-healing machinery.
- Manual recovery is valid for rare, low-impact, easy-to-diagnose failures.

## Escalation Conditions

Add heavier reliability mechanisms for high failure cost, unacceptable manual recovery, explicit SLA, frequent failures at scale, irreversible side effects, proven data loss, or evidence that bounded retry is insufficient.

## Warning Signs

- Retries create more retries.
- Every exception gets a separate recovery state.
- Rare edge cases require large compensation workflows.
- Recovery machinery is more complex than the primary business path.
- Engineers cannot explain the state path after one failure.

## Verification

Focus on important timeout, retryable/non-retryable failure, duplicate execution, partial failure, restart, recovery, and degradation paths rather than every theoretical combination.

Final question:

> **Is the failure path more complex than the problem warrants?**
