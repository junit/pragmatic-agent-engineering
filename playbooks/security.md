# Security Playbook

Use this playbook for authentication, authorization, sensitive data, external input, trust boundaries, and security configuration.

Goal:

> **Protect hard security boundaries with mechanisms that are as simple, mature, and verifiable as the risk allows.**

## Scope

Apply when a task involves authentication, authorization, tenant/data isolation, untrusted input, files/URLs/paths/network access, secrets, public APIs, sensitive data, or audit requirements.

## Hard Constraints

1. **Enforce final authorization on the trusted server side.** UI hiding, disabled controls, and client-provided identity or permission fields are not authorization.
2. **Validate untrusted input at trust boundaries.** Validate type, length, format, range, allowed values, and resource ownership as appropriate.
3. **Use least privilege.** Users, services, and credentials receive only the permissions required for their responsibility.
4. **Do not expose sensitive information unnecessarily.** Secrets, passwords, tokens, and sensitive data should not leak into logs, URLs, clients, or ordinary configuration.
5. **Treat security-boundary changes as high risk.** Material changes to authentication, authorization, isolation, secrets, or sensitive-data handling require the High Risk workflow.
6. **Identity, functional permission, and data scope are distinct.** Being authenticated or belonging to a broad identity group does not imply access to every protected resource; missing or invalid scope must not silently widen access.

## Default Heuristics

- Prefer allowlists when the valid set can be defined.
- For paths, URLs, and identifiers, prefer `canonicalize → validate → use` over endless special-case filters.
- Prefer mature framework security capabilities; avoid inventing authentication, password schemes, token formats, or cryptographic protocols without necessity.
- Place authorization close to the actual protected resource boundary.
- Trust forwarded client identity or source-IP headers only from explicitly trusted proxies; normalize or overwrite them at the trusted ingress instead of accepting arbitrary client-supplied values.
- During a suspected compromise, preserve useful evidence before destructive cleanup when safe, while prioritizing containment of active access and revocation/rotation of compromised credentials.
- When identity or permission cannot be established safely, fail closed.

## Escalation Conditions

Add heavier security mechanisms only when justified by regulation, high-value assets, high-risk external exposure, multiple trust boundaries, strict audit requirements, a concrete threat model, real attacks, or evidence that the current mechanism is insufficient.

## Warning Signs

- Security depends on a growing list of string-specific exceptions.
- The same authorization rule is scattered across layers with inconsistent results.
- Every bypass is fixed by adding another filter.
- Client state starts deciding server authorization.
- Security configuration grows faster than the team's ability to explain it.

## Verification

Verify the relevant authorization success cases, privilege violations, cross-user/cross-tenant access, input boundaries, sensitive-data leakage, critical configuration, and security regressions.

Final question:

> **Are the security guarantees clear and explainable, or do they depend on layers of special cases?**
