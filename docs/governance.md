# 1520ai — Governance & Authority Model

## Purpose

This document defines the authority structure, decision precedence, and governance model for all software and AI systems developed at 1520ai.

Its purpose is to ensure that decisions related to safety, security, regulatory compliance, and AI behavior are made explicitly, consistently, and traceably, even as teams, products, and systems scale.

**This document is binding across all 1520ai repositories unless an explicit exception is documented and approved.**

---

## Scope

This governance model applies to:

- All 1520ai software repositories
- All AI-enabled systems and models
- All environments (development, staging, production)
- All contributors (engineering, data science, clinical, operations, leadership)

It governs how decisions are made, not just how code is written.

---

## Authority Hierarchy

When conflicts arise, authority is resolved according to the following precedence order, from highest to lowest:

| Level | Authority |
| ----- | --------- |
| 1 | **External Regulatory Authority** — Federal and state healthcare regulations, binding guidance, and audit requirements. |
| 2 | **1520ai Governance Artifacts** — This document (`docs/governance.md`), security, data protection, and Responsible AI standards. |
| 3 | **Product-Level Governance** — Product-specific authority documents and explicitly documented invariants (e.g., Hospiclarity). |
| 4 | **Repository-Level Controls** — CODEOWNERS, contribution rules, and repository-specific enforcement. |
| 5 | **Implementation Details** — Code, configuration, tooling, and infrastructure choices. |

**Lower levels may not override higher levels.**
If a conflict exists, the higher authority wins by default.

---

## Decision Classes & Ownership

Decisions are grouped into explicit classes with defined ownership.
Where decisions span multiple classes, joint authority applies (see [Cross-Cutting Decisions](#cross-cutting-decisions)).

### 1. Regulatory & Compliance Decisions

#### Examples

- Interpretation of regulatory requirements
- Definition of regulatory hard stops
- Audit defensibility thresholds

#### Authority

- Compliance leadership
- Clinical governance leadership

#### Rules

- MUST be documented
- MUST be traceable to regulatory source
- MUST NOT be overridden by model output or scoring

### 2. Security & Data Protection Decisions

#### Examples

- PHI boundaries
- Encryption, access control, and audit logging
- Data movement and retention rules

#### Authority

- Security leadership
- Engineering leadership (joint)

#### Rules

- Security controls are non-optional
- Convenience is not a valid exception criterion
- Exceptions MUST be documented and time-bounded

### 3. AI Behavior & Model Governance

#### Examples

- Model deployment approval
- Determinism and stability requirements
- Human-in-the-loop enforcement
- Drift detection and response

#### Authority

- AI Engineering leadership
- Product governance (where applicable)

#### Rules

- Models MUST be explainable at decision time
- Silent adaptation is prohibited
- Model confidence MUST NOT override authority constraints

### 4. Engineering & Implementation Decisions

#### Examples

- Language and framework selection
- Architecture patterns
- Internal APIs and tooling

#### Authority

- Engineering leadership
- Repository owners (CODEOWNERS)

#### Rules

- MUST conform to higher-level constraints
- MAY vary by product or repository

---

## Cross-Cutting Decisions

Some decisions span multiple classes (e.g., an AI model that processes PHI).

In such cases:

- **Primary authority** is determined by the highest applicable risk domain
- **Joint review** is required when decisions affect:
  - Regulatory + AI behavior
  - Security + AI behavior
  - Regulatory + security

If authorities disagree, the decision escalates to the higher authority in the hierarchy.

---

## Binding Invariants

The following invariants apply across all systems unless explicitly superseded by external regulation:

**Human judgment remains primary**
AI systems support decisions; they do not replace professional authority.

**Determinism over probability**
Explainable, stable behavior is preferred over opaque optimization.

**Authority cannot be bypassed**
Regulatory or security hard stops cannot be overridden by scoring, confidence, or model output.

**No silent failure or adaptation**
Behavior changes must be observable, reviewable, and logged.

**Auditability is a first-class requirement**
Systems must be explainable after the fact, not just at runtime.

---

## Change Control & Exceptions

### Relationship to change-control.md

This document defines **what** must be governed.
[docs/change-control.md](change-control.md) defines **how** changes and exceptions are proposed, reviewed, approved, and tracked.

### Governance Changes

Changes to governance artifacts:

- MUST be proposed via pull request
- MUST be reviewed by designated CODEOWNERS
- MUST be logged in CHANGELOG.md
- MUST include an impact assessment

### Exceptions

Exceptions to governance rules:

- Are explicit, never implicit
- MUST be documented
- MUST include:
  - Rationale
  - Scope
  - Duration
  - Approving authority

**Temporary exceptions expire by default unless explicitly renewed.**

### Exception Template (Minimum)

```text
Exception ID:
Affected Artifact(s):
Decision Class(es):
Rationale:
Scope:
Duration / Expiration:
Risk Assessment:
Approving Authority:
Date Approved:
```

---

## Conflict Resolution & Escalation

When disputes arise:

1. Identify the decision class(es)
2. Determine the highest applicable authority
3. Escalate to that authority if unresolved
4. Document the outcome

### Escalation Timing

| Type                                            | Expectation                                                |
| ----------------------------------------------- | ---------------------------------------------------------- |
| **Urgent** (security, PHI, regulatory exposure) | Initial review SHOULD occur within one business day.       |
| **Non-urgent**                                  | Review SHOULD occur within a reasonable planning cycle.    |

If the designated authority is unavailable, escalation proceeds up the authority hierarchy.

**Undocumented decisions are treated as non-binding.**

---

## Relationship to Product Governance

This document defines organization-wide governance.

Product repositories MAY define stricter rules, but they:

- MUST reference this document
- MUST NOT weaken or contradict it
- SHOULD explicitly list additional constraints

---

## Enforcement

Governance is enforced through:

- CODEOWNERS approval requirements
- CI/CD checks
- Release gating
- Audit reviews
- Incident review processes

**Failure to follow governance is treated as a system risk, not a stylistic issue.**

---

## Definitions (Selected)

| Term | Definition |
| ---- | ---------- |
| **Hard Stop** | A regulatory or security condition that cannot be overridden by scoring or judgment. |
| **Silent Adaptation** | A system behavior change that occurs without explicit review, logging, or approval. |
| **Drift Detection** | Monitoring mechanisms that surface changes in model or system behavior for human review. |

(Additional definitions may live in product-specific governance.)

---

## Status

This document is **active and binding**.

It will evolve as:

- Regulatory environments change
- AI risk management matures
- Products approach clinical deployment

All revisions are tracked, reviewed, and auditable.
