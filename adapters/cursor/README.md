# Cursor Adapter

Goal: reuse the repository's Canonical Policy from Cursor project rules without creating a parallel ruleset.

Recommended approach:

- Point project-level Cursor rules to root `AGENTS.md`.
- Reference only the Playbooks needed for the current task.
- Do not permanently inject every Playbook.
- Do not copy the complete Core Policy.

Cursor rule formats may change; use the current project-rule mechanism when integrating.
