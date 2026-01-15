# 1520ai — Governance Documentation Index

**Status:** Active
**Scope:** Organization-wide
**Audience:** Internal teams, auditors, regulators, partners

---

## Purpose

This index provides a single authoritative entry point to 1520ai's governance, security, and Responsible AI documentation.

It answers three questions clearly:

1. What documents exist
2. Which documents are binding
3. How they relate to one another

**This file does not introduce new policy. It describes where authority lives.**

---

## How to Use This Index

- **Auditors & reviewers:** Start at [Authority & Binding Documents](#authority--binding-documents)
- **New team members:** Follow the [Onboarding Path](#onboarding-path-required-reading-order)
- **Contributors:** Use this to determine which documents must be updated for a given change

---

## Authority & Binding Documents

The following documents define binding constraints and must be followed.

### Governance & Authority

- **[governance.md](governance.md)**
  Defines authority hierarchy, decision classes, binding invariants, and enforcement.

- **[change-control.md](change-control.md)**
  Defines how changes, exceptions, and emergency actions are proposed, approved, and documented.

### Registries & History

- **[exceptions.md](exceptions.md)**
  Authoritative registry of all active and expired governance exceptions.

- **[CHANGELOG.md](../CHANGELOG.md)** (repo root)
  Append-only record of all material governance and standards changes.

### Responsible AI

- **[responsible-ai.md](responsible-ai.md)**
  Defines Responsible AI posture, risk framing, and release constraints.

### Security

- **[SECURITY.md](../SECURITY.md)** (repo root)
  Defines security reporting, escalation, and incident handling.

### AI Systems

- **[ai-release-gates.md](ai-release-gates.md)**
  Defines mandatory validation gates for AI system production deployment.

### Operations

- **[incident-response.md](incident-response.md)**
  Defines incident escalation, response process, and post-mortem requirements.

- **[data-protection.md](data-protection.md)**
  Defines data handling, PHI boundaries, and privacy requirements.

- **[engineering-operating-standards.md](engineering-operating-standards.md)**
  Defines technical standards for all contributors.

---

## Enforcement Artifacts (Root-Level)

The following files enforce governance via GitHub mechanisms:

- **[CODEOWNERS](../CODEOWNERS)**
  Defines required approvers for governance and security artifacts.

- **[CONTRIBUTING.md](../CONTRIBUTING.md)**
  Defines how changes are proposed, reviewed, and merged.

These files are considered **operational controls**, not explanatory documentation.

---

## Onboarding Path (Required Reading Order)

New team members working with governance, security, or AI systems SHOULD read:

1. **[governance.md](governance.md)** — authority and non-negotiables
2. **[change-control.md](change-control.md)** — how changes happen
3. **[responsible-ai.md](responsible-ai.md)** — AI posture and constraints
4. **[ai-release-gates.md](ai-release-gates.md)** — AI deployment requirements
5. **[incident-response.md](incident-response.md)** — incident handling process
6. **[SECURITY.md](../SECURITY.md)** — security expectations and escalation
7. **[exceptions.md](exceptions.md)** — current deviations from baseline

---

## Document Classification

| Document | Role |
| -------- | ---- |
| `governance.md` | Authority & precedence |
| `change-control.md` | Process & mechanics |
| `responsible-ai.md` | AI intent & posture |
| `ai-release-gates.md` | AI deployment validation |
| `incident-response.md` | Incident handling & learning |
| `data-protection.md` | Data & privacy requirements |
| `SECURITY.md` | Security escalation |
| `exceptions.md` | Exception registry |
| `CHANGELOG.md` | Historical record |
| `CODEOWNERS` | Enforcement |
| `CONTRIBUTING.md` | Contribution rules |

---

## Change Impact Guidance

If a change affects:

| Change Type | Update Required |
| ----------- | --------------- |
| Authority, obligations, or constraints | `governance.md` |
| Process or exception mechanics | `change-control.md` |
| AI behavior or risk posture | `responsible-ai.md` |
| AI deployment or release process | `ai-release-gates.md` |
| Incident handling or escalation | `incident-response.md` |
| Security handling | `SECURITY.md` |
| Temporary deviations | `exceptions.md` |
| Any binding document | `CHANGELOG.md` |

---

## Conflict Resolution

In the event of conflict:

1. Regulatory requirements prevail
2. `governance.md` prevails over all other documents
3. Enforced controls (CODEOWNERS, CI) prevail over intent documents
4. Clarifications do not override authority

---

## Status

This index is **active and binding**.

It is updated only when:

- New governance artifacts are introduced, or
- Authority relationships change

All updates follow formal change control and are recorded in `CHANGELOG.md`.

---

## Final Note

This documentation set is designed to be:

- Explicit
- Inspectable
- Enforceable

**If something appears ambiguous or missing, that is treated as a governance gap, not a documentation issue.**
