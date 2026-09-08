# Frontend State: When an Admin UI Started Behaving Like a Collaborative Editor

## Background

An internal admin application had a notification panel: open the list, switch tabs, mark items read, refresh unread counts, and navigate to related pages. Interaction frequency was low.

## Initial Design

- fetch list;
- fetch unread count;
- mark item read;
- update local UI;
- refresh after meaningful server events.

## How Complexity Grew

A request sequence was added to prevent stale responses. A count revision followed. Tab switching added another revision. Optimistic rollback needed to detect newer state, so more versions appeared. Real-time push introduced additional ordering concerns.

The store eventually contained concepts such as:

```text
context generation
fetch sequence
count revision
count sequence
tab revision
item revisions
```

## Warning Sign

The product was a low-frequency admin UI, but its state model started resembling real-time collaborative editing and offline conflict resolution.

## Real Contract

What the user actually needed was simpler:

1. a reasonably fresh notification list;
2. immediate feedback for marking an item read;
3. visible failures;
4. eventual convergence to server truth;
5. clearly stale responses should not overwrite a newer context.

## Simplification

- Treat server state as authoritative business state.
- Keep tabs/loading as local UI state.
- Use one necessary context/request guard.
- Use optimistic updates only where rollback remains simple.
- On ambiguous failure, refresh authoritative state.

Instead of:

```text
compare revision
→ merge push generation
→ conditional rollback
→ repair count
```

a low-frequency admin UI can often use:

```text
show error
→ refresh authoritative state
```

## Necessary Complexity

Keep protection against obviously stale responses, duplicate submissions, broken loading/error behavior, and incorrect navigation/authorization behavior.

## Lesson

> **Frontend-state complexity should match actual interaction complexity, not every race condition we can imagine.**
