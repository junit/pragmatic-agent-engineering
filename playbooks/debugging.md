# Debugging Playbook

Use this playbook for defects, incidents, unexpected behavior, production failures, configuration mismatches, and difficult regressions.

Goal:

> **Establish facts, narrow the failure boundary, test falsifiable hypotheses, and verify the fix before changing more of the system.**

## Scope

Application bugs, infrastructure incidents, data failures, performance anomalies, integration failures, configuration problems, intermittent behavior, and regressions.

## Hard Constraints

1. **Separate symptom from root cause.** An error message, warning, timeout, log failure, or downstream symptom is not automatically the cause of the user-visible failure.
2. **Do not present an untested hypothesis as the root cause.** A root-cause claim needs evidence that explains the observed behavior and rules out material alternatives.
3. **Change one meaningful variable at a time when isolating cause.** Avoid multi-change experiments that make the result uninterpretable.
4. **Verify the fix against the original failure.** A plausible code change is not completion without evidence that the observed problem is resolved.

## Default Heuristics

- Establish the baseline first: actual version, environment, effective configuration, relevant data, time, recent changes, and reproducible symptoms.
- Prefer the shortest reliable reproducer over a large end-to-end scenario.
- Compare working and failing cases: version, account/data, configuration, request path, timing, node, protocol, and state.
- Form falsifiable hypotheses. For each one, state why it is plausible, what evidence supports it, what observation would disprove it, and the smallest test that can discriminate it.
- Prefer direct evidence from runtime state, source code, traces, metrics, thread dumps, query plans, or protocol captures over assumptions based on naming or intended design.
- Distinguish primary-operation failure from observability failure. A logging, metrics, notification, or serialization error is not proof that the underlying business operation failed.
- If several speculative fixes fail, stop patching and revisit the original assumptions, ownership boundaries, shared state, and data model.

## Escalation Conditions

Use deeper incident analysis when failures are intermittent, concurrent, cross-system, security-sensitive, destructive, data-corrupting, difficult to reproduce, or capable of leaving partial state.

## Warning Signs

- “Probably cache/network/database” without a discriminating experiment.
- A fix is proposed before the actual version or effective configuration is known.
- Several variables are changed at once and success is treated as proof of cause.
- The diagnosis relies mainly on design documents while the runtime behaves differently.
- Previous test results are quoted as current verification after relevant changes.
- Each failed patch adds another fallback, watchdog, or recovery state.

## Verification

Verify, as relevant:

1. the original reproducer now passes;
2. the root-cause hypothesis correctly predicts the before/after behavior;
3. adjacent states and important failure paths still work;
4. the effective runtime/configuration matches the intended fix;
5. verification evidence is fresh enough for the completion claim.

Final question:

> **What evidence would prove this diagnosis wrong, and did we actually test it?**
