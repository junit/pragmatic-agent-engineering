# Agent Systems Playbook

Use this playbook for coding-agent policies, multi-agent workflows, specialist agents, skills, automations, schedules, shared state, and tool-mediated handoffs.

Goal:

> **Keep policy, responsibility, workflow, authority, and live state separate so agent systems remain explainable and auditable.**

## Scope

AI coding agents, specialist roles, shared policy/skills, orchestration, scheduled jobs, blackboards, tool calls, handoffs, derived dashboards, persistent state, and write permissions.

## Hard Constraints

1. **Separate shared policy from local role instructions.** Cross-cutting invariants should have one owner; role instructions should define role-specific inputs, outputs, permissions, tools, and workflow rather than duplicate the entire shared policy.
2. **Live authoritative state outranks memory and projections.** When a current source of truth exists, old chats, memory, handoff snapshots, dashboards, and generated summaries must not silently replace it.
3. **Do not claim execution that was not observed.** Never say another agent, skill, tool, schedule, or external system was called unless the execution actually occurred and its outcome is available.
4. **Write ownership must be explicit.** Distinguish observation, recommendation, decision, and executed side effect; a recommendation must not silently become an actual state change.
5. **Derived views are not automatically control inputs.** Dashboards, reports, projections, and summaries should remain derived unless the architecture explicitly designates them as authoritative.

## Default Heuristics

- Store cross-agent invariants once; keep specialist methodology in the specialist capability rather than copying it into every agent.
- Give each important state domain a clear write owner; prefer many readers and one writer over competing writers.
- Keep schedules and isolated automations self-contained enough to execute without relying on invisible conversational state.
- Use stable run/cycle identifiers and deduplicate repeated execution when multiple execution channels can reach the same work.
- Capability detection should report what is available; capability selection should follow explicit workflow, policy, or user intent rather than happen implicitly.
- Preserve the distinction between authoritative state and a human-friendly projection of that state.
- Prefer fewer roles with cohesive responsibilities over many agents that repeatedly synthesize, route, or rewrite the same facts.

## Escalation Conditions

More orchestration is justified when independent specialist ownership, separate permissions, asynchronous work, high-value auditability, different tools, or real concurrency make one-agent execution insufficient.

## Warning Signs

- Shared rules are copied into every agent and begin to drift.
- Several agents write the same business field.
- A dashboard or handoff document is parsed back as if it were the authoritative state.
- Schedules and agents perform the same work without deduplication.
- The system claims “agent-to-agent” collaboration that the platform cannot actually execute.
- Adding a new role mainly creates another synthesis or routing step.
- Historical chat state is used despite a live source of truth being available.

## Verification

Test, as relevant:

- stale-state behavior;
- write-permission boundaries;
- duplicate runs;
- unavailable capabilities;
- tool/agent execution claims;
- recommendation versus executed state;
- derived-view versus authoritative-state behavior.

Final question:

> **Can we state, for every important fact and action, who owns it, where the live truth is, and whether the action actually happened?**
