# GitHub Copilot Adapter

Goal: reuse root `AGENTS.md` from project-level Copilot instructions without maintaining a second core policy.

Recommended approach:

- Keep Copilot-specific instructions lightweight.
- Point to `AGENTS.md` as the engineering policy.
- Add task-relevant Playbooks only when needed.
- Do not copy the entire Core Policy.

Use the current GitHub Copilot project-instruction mechanism when integrating.
