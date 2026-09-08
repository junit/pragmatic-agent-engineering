# Backend Playbook

Use this playbook for backend business logic, APIs, service boundaries, background jobs, and external integrations.

Goal:

> **Keep business boundaries, data ownership, and side effects clear while using the minimum sufficient backend complexity.**

## Scope

APIs, business services, background jobs, external calls, authorization context, data-access boundaries, business state transitions, and service collaboration.

## Hard Constraints

1. **The backend is the final enforcer of business invariants.** Critical rules must not depend only on client validation or UI state.
2. **API contracts must be clear.** Inputs, outputs, error semantics, authorization requirements, and side effects should be understandable.
3. **Side effects must be visible.** Data writes, message sends, external calls, file writes, and background jobs should have identifiable ownership.
4. **Data ownership must be clear.** Avoid multiple services with ambiguous write ownership over the same core fact.

## Default Heuristics

- Organize services around cohesive responsibilities; avoid both giant services and ceremonial micro-services.
- Keep entry layers clear, but do not manufacture layers just to keep controllers artificially tiny.
- Prefer explicit business flow over critical logic scattered through hooks, listeners, AOP, and hidden callbacks.
- Validate at boundaries so internal code can operate on already-valid basic shapes.
- Treat external calls as boundaries with explicit timeout, error, retry, transaction, and trust semantics.
- Do not split services merely because a class is large, microservices are fashionable, or future scaling is imagined.

## Escalation Conditions

Consider more complex backend architecture when there is demonstrated independent deployment need, throughput pressure, team ownership boundary, fault isolation need, large-scale async workload, formal external contract, or a monolithic boundary that is demonstrably blocking maintainability.

## Warning Signs

- A simple request crosses many ceremonial layers.
- Core business logic is spread across listeners/AOP/callbacks.
- Multiple services mutate the same entity without clear ownership.
- Adding one field requires touching many unrelated abstractions.
- Service count grows faster than independent business boundaries.

## Verification

Verify API contracts, critical flows, authorization, state transitions, transaction boundaries, important side effects, external-call failures, and regressions.

Final question:

> **Can an ordinary engineer follow the main business path and state changes from the entry point?**
