# Claude Code Adapter

Goal: reuse the repository's Canonical Policy rather than maintain a separate rewrite.

Recommended approach:

- Keep root `AGENTS.md` authoritative.
- If the project uses Claude Code-specific instruction files, use them only to point to `AGENTS.md` and relevant task Playbooks.
- Do not duplicate the complete Core Policy.

Platform-specific loading behavior may change over time; follow the current Claude Code project-instruction mechanism when integrating.
