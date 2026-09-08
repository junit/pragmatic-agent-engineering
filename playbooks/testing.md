# Testing Playbook

Use this playbook to decide what to test, how deeply to test it, and how to avoid tests that preserve accidental complexity.

Goal:

> **Use the smallest high-value test set that protects real contracts and material risk.**

## Scope

New features, bug fixes, refactoring, APIs, data processing, security logic, migrations, and critical failure paths.

## Hard Constraints

1. **Critical behavior must be verifiable.** “The code looks right” is not completion.
2. **Bug fixes should include regression verification when the bug can reasonably be reproduced.**
3. **High-risk contracts require appropriate tests.** Authorization, data integrity, public APIs, migrations, and high-risk failure paths need direct verification.

## Default Heuristics

- Test behavior, not structure: prioritize inputs, outputs, state changes, invariants, and external contracts.
- Typical priority: core invariants → critical business paths → high-risk failures → external contracts → ordinary behavior → low-value implementation details.
- Match test depth to risk.
- If simple business behavior requires extensive mocking, inspect whether the architecture is over-fragmented.
- Treat coverage as a diagnostic signal, not the final quality target.

## Escalation Conditions

Integration, contract, and end-to-end tests are most valuable when there are real module contracts, critical database behavior, complex third-party integration, multi-component coordination, migrations, concurrency, or high-risk security logic.

## Warning Signs

- Test code is far more complex than the behavior it protects.
- Internal refactoring breaks many tests despite unchanged behavior.
- Tests focus heavily on private methods.
- Mock count grows rapidly.
- Coverage is high while important incidents remain unprotected.

## Verification

Ask:

1. Which real contracts are protected?
2. Which important failures would be detected?
3. If the implementation were rewritten but behavior stayed the same, would most tests still pass?
4. Are any tests preserving historical complexity rather than business value?
