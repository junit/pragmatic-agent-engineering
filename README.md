# Pragmatic Agent Engineering

[English](./README.md) | [简体中文](./README.zh-CN.md) | [中文完整版](./README.full.zh-CN.md)

> **AI can generate code cheaply. Humans still pay for complexity.**

Pragmatic Agent Engineering is a practical engineering policy, risk-based workflow, and set of opt-in domain playbooks for **AI coding agents**.

It is not about making AI write less code. It is about helping AI make better engineering trade-offs:

> **Solve real problems reliably with complexity proportional to actual risk and business value.**

The project is model-, IDE-, language-, and framework-agnostic.

## Why This Project Exists

AI has reduced the cost of generating code. It has not equally reduced the cost of:

- understanding complex systems;
- reviewing architecture;
- debugging production failures;
- maintaining state machines and compatibility layers;
- migrating and recovering data;
- operating infrastructure;
- onboarding future maintainers.

This creates a new failure mode:

```text
edge case
→ fallback
→ watchdog
→ state/revision control
→ reconciliation
→ tests that preserve all of the above
```

Each step may look technically reasonable. The final system may still be wrong for the problem.

## Core Idea: Minimum Sufficient Complexity

We do not optimize for the simplest possible software, nor for the most sophisticated architecture.

We optimize for:

> **The least complexity that fully satisfies correctness, security, data integrity, explicit reliability requirements, and real performance needs.**

Necessary complexity is good. Unproven complexity carries the burden of proof.

## Core Principles

- Correctness before cleverness
- Facts before assumptions
- Solve the real requirement
- Complexity requires evidence
- Fix causes before adding layers
- Boundaries matter more than layers
- Design for known change
- Security and data integrity are hard constraints
- Tests protect contracts, not accidental complexity
- Measure before optimizing
- Prefer reversible decisions under uncertainty
- Deleting code is engineering
- Stop when the problem is solved

The canonical executable policy is [`AGENTS.md`](./AGENTS.md).

## Risk-Based Workflow

### Low Risk

```text
Understand → Implement → Verify → Deliver
```

For local, reversible, easy-to-verify changes with no critical contract, security, or data impact.

### Medium Risk

```text
Understand → Lightweight Design → Implement → Verify
→ Complexity Check → Deliver
```

For cross-module work or meaningful design choices that remain reasonably reversible.

### High Risk

```text
Analyze → Recommend → Assess Risks/Migration → Confirm
→ Implement → Fully Verify → Complexity/Deletion Review → Deliver
```

For irreversible operations, destructive data changes, security-boundary changes, breaking contracts, major architecture replacements, large migrations, or high-impact infrastructure work.

## Playbooks

Keep the core small and load domain knowledge only when relevant:

- [`security.md`](./playbooks/security.md)
- [`backend.md`](./playbooks/backend.md)
- [`frontend.md`](./playbooks/frontend.md)
- [`database.md`](./playbooks/database.md)
- [`reliability.md`](./playbooks/reliability.md)
- [`distributed-systems.md`](./playbooks/distributed-systems.md)
- [`data-engineering.md`](./playbooks/data-engineering.md)
- [`debugging.md`](./playbooks/debugging.md)
- [`compatibility.md`](./playbooks/compatibility.md)
- [`agent-systems.md`](./playbooks/agent-systems.md)
- [`testing.md`](./playbooks/testing.md)

> **Minimum Sufficient Context: load only what the current task needs.**

## Case Studies

The initial case studies under [`examples/overengineering/`](./examples/overengineering/) cover:

1. a notification center whose reliability machinery outgrew the business problem;
2. a data pipeline where “exactly once everywhere” became the wrong optimization target;
3. an admin frontend whose state model started resembling a collaborative editor.

The point is not that complex technology is bad. The point is to identify:

> **when complexity stops paying for its long-term cost.**

## Repository Structure

```text
pragmatic-agent-engineering/
├── README.md
├── README.zh-CN.md
├── README.full.zh-CN.md
├── AGENTS.md               # canonical Core SSOT
├── CONTRIBUTING.md
├── LICENSE
│
├── playbooks/
├── docs/
├── examples/
└── adapters/
```

`AGENTS.md` is the single source of truth for core rules. README files, docs, examples, and adapters may explain or demonstrate the policy, but must not redefine a second core policy.

## What This Project Is Not

This project is not:

- a best-practices encyclopedia;
- a mandatory ADR/checklist process;
- an architecture scoring system;
- a design-pattern collection;
- a governance framework that blocks every small change.

If this project turns into hundreds of rules and layers of governance, it has violated its own philosophy.

## Contributing

Contributions are welcome, especially:

- real AI overengineering cases;
- simplification case studies;
- domain playbook improvements;
- lightweight adapters for coding agents;
- proposals to remove redundant rules.

Before adding a new core rule, ask:

1. What repeated real problem does it solve?
2. What evidence shows the problem exists?
3. Why do existing principles not cover it?
4. What cognitive and execution cost does the new rule add?

See [`CONTRIBUTING.md`](./CONTRIBUTING.md).

## License

MIT License. See [`LICENSE`](./LICENSE).

---

> **AI can generate code cheaply. Humans still pay for complexity.**

Final criterion:

> **Did we solve the real problem reliably with complexity proportional to actual risk and business value?**
