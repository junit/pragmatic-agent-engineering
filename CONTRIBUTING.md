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

## Promoting Experience into Rules

Use the narrowest layer that prevents the repeated failure without turning one incident into universal policy:

```text
recurring cross-domain invariant -> AGENTS.md
reusable domain lesson          -> Playbook
explanatory real-world pattern  -> Example / Docs
tool- or version-specific fact  -> Adapter / project documentation
transient incident detail       -> do not promote
```

Before promotion:

1. identify the repeated problem or high-impact risk;
2. record the treatment that actually worked;
3. state where that treatment does not apply;
4. check whether an existing rule already expresses the same invariant;
5. choose the narrowest useful layer;
6. add a verification signal, not just a slogan;
7. remove or merge older rules made redundant by the new wording.

A single severe security or data-integrity failure can justify a hard rule when the consequence is material and the preventive invariant is stable. Ordinary one-off preferences, vendor quirks, and temporary version behavior usually should not become Core rules.

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
