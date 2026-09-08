# Compatibility and Canonical Model Playbook

Use this playbook for backward compatibility, schema or format migration, legacy configuration, parser evolution, protocol transitions, and old-client support.

Goal:

> **Keep the target model semantically clean while containing required legacy behavior at explicit boundaries.**

## Scope

API versions, configuration formats, schemas, serialized data, parsers, old clients, protocol migrations, renamed fields, changed units, sentinel values, legacy enums, and transitional adapters.

## Hard Constraints

1. **Compatibility needs a real contract.** Do not preserve legacy behavior merely because it exists; require an explicit compatibility commitment, migration requirement, or demonstrated user impact.
2. **The canonical model represents the target semantics.** Do not make new core data structures permanently ambiguous just to mirror a flawed historical representation.
3. **Normalize at the boundary.** Convert supported legacy inputs into one canonical representation before core processing; downstream consumers should not independently re-parse or reinterpret the same source.
4. **Compatibility mechanisms need an exit condition.** Define the supported legacy range, conversion semantics, observability, and removal or deprecation path where practical.

## Default Heuristics

- Prefer `legacy input -> adapter/normalizer -> canonical model -> core logic`.
- Preserve stable semantic identity across migrations when downstream references depend on it.
- Make changed units, direction, null/sentinel meaning, enum meaning, and precedence explicit during normalization.
- Keep old field names, scalar shortcuts, parser fallbacks, and migration-only state out of the canonical model when the adapter can contain them.
- If the old representation is objectively wrong and no compatibility contract requires it, prefer the clean target model over writing permanent compatibility code.
- When several parsers or consumers need the same structured facts, produce those facts once and share them rather than duplicating extraction logic.
- Prefer versioned compatibility at the edge to hidden dual semantics in the core.

## Escalation Conditions

More elaborate compatibility machinery may be justified for public APIs, external clients that cannot migrate quickly, long-lived stored data, rolling multi-version deployments, regulated formats, or contracts with explicit support windows.

## Warning Signs

- “Temporary” legacy fields become dependencies of new features.
- Multiple canonical-looking representations exist for the same fact.
- Downstream modules independently parse the same raw source.
- Compatibility logic spreads from adapters into domain logic, storage, UI, and reports.
- Nobody can state which representation is authoritative.
- Supporting an old mistake requires more code than migrating or rejecting it.

## Verification

Verify supported legacy inputs, canonical output semantics, precedence rules, invalid/ambiguous input behavior, migration/replay where relevant, and that downstream consumers use the canonical representation rather than reinterpreting raw input.

Final question:

> **Are we supporting a real compatibility contract, or turning historical mistakes into permanent architecture?**
