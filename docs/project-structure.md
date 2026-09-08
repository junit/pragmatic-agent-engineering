# Project Structure and Single Source of Truth

This project deliberately uses one canonical core policy to prevent rule drift.

## Canonical Core

```text
AGENTS.md
└── Canonical Core Engineering Policy
```

Only `AGENTS.md` defines cross-domain core rules.

## Responsibilities

### README files
Introduce the project, philosophy, usage, and community entry points.

### playbooks/
Add domain-specific guidance. Playbooks must not override the Core Policy. This includes reusable operational domains such as debugging, compatibility/migration, and agent-system coordination when they are relevant to a task.

### examples/
Provide evidence: how complexity grew, how it was simplified, and what necessary protections were retained.

### adapters/
Explain how to connect the Canonical Policy to different coding agents. Adapters do not copy Core Rules.

### docs/
Explain design and maintenance without redefining executable rules.

## Precedence

If guidance conflicts:

```text
explicit user/project hard constraints
→ AGENTS.md
→ relevant Playbook
→ Adapter / Docs / Examples
```

Adapters, Docs, and Examples are never a second Core Policy.
