# Adapters

Adapters help different AI coding agents reuse the root `AGENTS.md` instead of maintaining independent rewritten policies.

Principles:

1. `AGENTS.md` remains the canonical Core Policy.
2. An Adapter describes integration and platform differences only.
3. Do not copy the full Core Policy into an Adapter.
4. When a platform changes, update only its Adapter.
