# Contributing to Pragmatic Agent Engineering

Thank you for contributing.

This project exists to improve engineering judgment for AI coding agents, not to grow an ever-larger rule system.

> **Complexity must pay rent.**

## What to Contribute

Welcome contributions include:

- corrections or simplifications to the canonical policy;
- real overengineering cases;
- simplification case studies;
- architecture review examples;
- domain playbook improvements;
- lightweight coding-agent adapters;
- proposals to remove or merge redundant rules.

Removing unnecessary rules is a valid contribution.

## Changing the Core Policy

Before changing `AGENTS.md`, answer:

### Problem
What repeated real problem does the change solve?

### Evidence
What real cases, reproducible behavior, or material risks support it?

### Existing Coverage
Why cannot the current Core Policy or an existing Playbook cover the issue?

### Cost
What reading, context, conflict, and execution cost does the new rule add?

If existing rules already cover the problem, prefer improving examples, docs, or a Playbook instead of adding another core rule.

## What Usually Does Not Belong in Core

Usually keep these out of `AGENTS.md`:

- language/framework-specific style rules;
- SQL migration details;
- retry parameters;
- specific vulnerability checklists;
- Kubernetes deployment rules;
- frontend framework tricks;
- vendor/tool-specific behavior.

Ask:

> **Does this apply to almost every software engineering task?**

If not, prefer a Playbook or Adapter.

## Playbook Structure

```text
# Domain

## Scope
## Hard Constraints
## Default Heuristics
## Escalation Conditions
## Warning Signs
## Verification
```

Keep Playbooks focused and distinguish hard constraints from heuristics.

## Case Study Structure

```text
## Background
## Initial Design
## How Complexity Grew
## Warning Signs
## Necessary Complexity
## Simplification
## Verification
## Reusable Lessons
```

Distinguish facts, deductions, assumptions, and opinions.

## Pull Requests

Keep a PR focused on one clear problem. Avoid mixing new rules, broad formatting, unrelated refactors, file reorganizations, and unrelated wording changes.

Suggested description:

```text
## Problem
## Evidence
## Change
## Why Existing Rules Are Insufficient
## Complexity Cost
## What Can Be Removed or Merged
```

## “Best Practices”

Do not add a rule merely because something is conventional, enterprise-grade, more complete, or useful someday.

A practice belongs here only when its real benefit exceeds its long-term rule cost.

## Rule Removal

Rules are not permanent. Remove or merge a rule when it is redundant, already covered by a higher-level principle, prone to mechanical misuse, or more expensive in context than it is valuable.

## Single Source of Truth

`AGENTS.md` is the only canonical Core Policy.

Other files may explain, demonstrate, or adapt it, but must not define a parallel core policy.

## Final Test

> **Does this contribution help AI coding agents solve real problems more reliably without adding complexity disproportionate to its value?**

If the answer is unclear, prefer the status quo.
