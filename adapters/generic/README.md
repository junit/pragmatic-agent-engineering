# Generic Adapter

For coding agents that support project-level instructions, rules, or context files.

Recommended approach:

1. Treat root `AGENTS.md` as the project engineering policy.
2. Load only the Playbooks relevant to the current task.
3. Do not permanently inject every Playbook.
4. Allow more specific project constraints to override non-hard heuristics where appropriate.

> **Canonical Core + Minimum Sufficient Context.**
