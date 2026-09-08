# Frontend Playbook

Use this playbook for UI interaction, component design, client state, data fetching, and user feedback.

Goal:

> **Keep UI state proportional to real user interaction complexity and aligned with authoritative server facts.**

## Scope

Pages, components, forms, client state, data fetching, routing, real-time updates, optimistic updates, and UI error handling.

## Hard Constraints

1. **The client is not a security boundary.** UI behavior may improve UX but cannot provide final authorization, isolation, or sensitive-resource protection.
2. **Important user actions need clear feedback.** Users should know when work is pending, successful, failed, or requires retry.
3. **Do not create unexplained data ambiguity.** If optimistic state, cache, real-time updates, or drafts may differ from server truth, define the semantics.

## Default Heuristics

- Keep state local to the smallest reasonable scope by default.
- Prefer derived state over mirrored state when derivation is reliable.
- Distinguish server state from UI state instead of mixing both into one large state model.
- Use optimistic updates when success is common, rollback is simple, and UX benefit is real.
- `idle/loading/success/error` is often enough; add state-machine detail only when real interaction complexity requires it.
- Split components by responsibility and comprehensibility, not by arbitrary file size.
- Prefer mature framework/platform routing, forms, fetching, and lifecycle capabilities over custom mini-frameworks.

## Escalation Conditions

More complex client-state systems may be justified by high interaction frequency, broad shared state, offline editing, real-time collaboration, heavy concurrent updates, undo/redo, or measured client performance constraints.

## Warning Signs

- A simple page has extensive global state.
- The same data is independently maintained in multiple stores.
- One button action requires several revision/sequence counters.
- The UI state machine is harder to explain than the business process.
- Components communicate primarily through a global event bus.

## Verification

Verify normal interaction, loading, error handling, duplicate clicks, navigation, refresh, server failure, relevant permission display, and regressions.

Final question:

> **Does frontend-state complexity match actual interaction complexity?**
