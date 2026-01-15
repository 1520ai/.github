# 1520ai — Organization Standards & Governance

This repository is the authoritative control plane for how 1520ai designs, builds, reviews, secures, and governs software—especially AI systems operating in regulated healthcare environments.

All 1520ai repositories are expected to conform to the standards defined here unless an explicit, documented exception exists.

---

## Purpose

1520ai builds AI systems for healthcare environments where trust, accountability, and auditability are non-negotiable.

This repository exists to:

- Establish binding engineering and governance standards
- Define authority, review, and escalation paths
- Ensure regulatory, security, and AI integrity alignment
- Preserve institutional memory as systems and teams scale

**This is not a marketing repository.**
It is an operational and governance artifact.

---

## Documentation Index

For the complete catalog of governance documents, see:

**[docs/index.md](docs/index.md)** — Authoritative index of all governance artifacts

The index provides:

- Document hierarchy and relationships
- Binding vs. informational classification
- Recommended reading order for new team members
- Change impact guidance

---

## Governance Framework Overview

### Authority & Process

| Document | Purpose |
| -------- | ------- |
| [governance.md](docs/governance.md) | Authority hierarchy, decision classes, binding invariants |
| [change-control.md](docs/change-control.md) | Change proposals, approvals, exception management |
| [exceptions.md](docs/exceptions.md) | Registry of active governance exceptions |
| [CHANGELOG.md](CHANGELOG.md) | Append-only record of all governance changes |

### AI Governance

| Document | Purpose |
| -------- | ------- |
| [responsible-ai.md](docs/responsible-ai.md) | AI posture, Sensitivity × Consensus risk model |
| [ai-release-gates.md](docs/ai-release-gates.md) | 6 mandatory validation gates for AI deployment |
| [model-registry.md](docs/model-registry.md) | Production model tracking and lifecycle |
| [ai-security.md](docs/ai-security.md) | LLM threats, prompt injection prevention |
| [data-lineage.md](docs/data-lineage.md) | Data provenance and training dataset documentation |

### Security & Data Protection

| Document | Purpose |
| -------- | ------- |
| [SECURITY.md](SECURITY.md) | Security reporting, escalation, incident handling |
| [data-protection.md](docs/data-protection.md) | PHI boundaries, privacy-by-design requirements |

### Operations

| Document | Purpose |
| -------- | ------- |
| [incident-response.md](docs/incident-response.md) | Incident severity, response process, post-mortems |
| [business-continuity.md](docs/business-continuity.md) | RTO/RPO objectives, disaster recovery procedures |

### Compliance & Audit

| Document | Purpose |
| -------- | ------- |
| [audit-coordination.md](docs/audit-coordination.md) | Audit preparation, finding tracking, attestations |
| [vendor-management.md](docs/vendor-management.md) | Vendor tiers, BAA requirements, third-party governance |
| [governance-metrics.md](docs/governance-metrics.md) | KPIs, dashboards, compliance reporting |

### Personnel

| Document | Purpose |
| -------- | ------- |
| [training-awareness.md](docs/training-awareness.md) | Training matrix, onboarding, compliance tracking |

### Contribution & Enforcement

| Document | Purpose |
| -------- | ------- |
| [CONTRIBUTING.md](CONTRIBUTING.md) | PR expectations, review discipline |
| [CODEOWNERS](CODEOWNERS) | Binding approval requirements |

---

## For New Team Members

If you are new to 1520ai, read these in order:

1. [governance.md](docs/governance.md) — Authority and non-negotiables
2. [change-control.md](docs/change-control.md) — How changes happen
3. [responsible-ai.md](docs/responsible-ai.md) — AI posture and constraints
4. [ai-release-gates.md](docs/ai-release-gates.md) — AI deployment requirements
5. [incident-response.md](docs/incident-response.md) — Incident handling process
6. [SECURITY.md](SECURITY.md) — Security expectations and escalation
7. [training-awareness.md](docs/training-awareness.md) — Required training

For the complete onboarding path, see [docs/index.md](docs/index.md).

---

## Guiding Principles (Binding)

These principles are operational constraints, not aspirational values.

**Human judgment remains primary**
Systems support clinical, regulatory, and professional decision-making. They do not replace it.

**Determinism over ambiguity**
We favor explainable, auditable behavior over opaque optimization.

**Regulatory authority is explicit**
Regulatory hard stops, security boundaries, and compliance constraints cannot be bypassed by scoring or confidence.

**Security and privacy by design**
Safeguards are designed in from the start, not layered on later.

**Operational realism**
Standards reflect how healthcare actually operates under time pressure and audit scrutiny.

---

## AI Release Gates

AI-enabled systems at 1520ai must pass 6 mandatory validation gates before production deployment:

| Gate | Purpose |
| ---- | ------- |
| Determinism & Reproducibility | Consistent outputs for identical inputs |
| Explainability & Transparency | Outputs can be explained to stakeholders |
| Drift Monitoring | Performance degradation detection |
| Bias & Fairness Assessment | Demographic performance validation |
| Rollback Capability | Ability to revert to previous version |
| Human-in-the-Loop | Appropriate human oversight configured |

Gate requirements scale based on Sensitivity × Consensus classification. Full requirements in [ai-release-gates.md](docs/ai-release-gates.md).

---

## Automated Governance

This repository includes automated governance validation:

| Workflow | Purpose |
| -------- | ------- |
| [governance-health.yml](.github/workflows/governance-health.yml) | Validates all required governance files exist, cross-references valid |
| [exception-expiration.yml](.github/workflows/exception-expiration.yml) | Alerts on expiring exceptions, fails CI on expired exceptions |

Governance health checks run:

- Weekly (scheduled)
- On PRs touching governance files
- On manual trigger

---

## Change Control & Versioning

Governance artifacts in this repository are versioned and review-controlled.

All material changes require:

- A pull request
- Review by designated CODEOWNERS
- An entry in the governance changelog

Changes are tracked in [CHANGELOG.md](CHANGELOG.md).

### Changelog Format

| Field | Description |
| ----- | ----------- |
| Date | When the change was approved |
| Artifact(s) affected | Which document(s) changed |
| Nature of change | Policy, clarification, control tightening, etc. |
| Impact assessment | Behavioral, security, regulatory, or none |
| Approver(s) | Who approved the change |

---

## Ownership & Escalation

### Repository Maintainers

- VP, AI Engineering
- VP, Technology & Engineering

Defined explicitly in [CODEOWNERS](CODEOWNERS).

In the event of conflict, **CODEOWNERS is the binding source of truth** for approval and ownership.

### Questions or Clarifications

- GitHub Issues (preferred for non-sensitive discussion)

### Security or Compliance Concerns

Urgent issues include, but are not limited to:

- Suspected PHI exposure
- Security control bypass or failure
- Unauthorized data movement
- Model behavior that violates documented authority or safety constraints

**Urgent issues must follow the escalation procedures defined in [SECURITY.md](SECURITY.md).**
They should not be handled via informal channels or delayed for convenience.

---

## Scope & Limitations

1520ai systems support clinical, compliance, and operational decision-making.

They do not replace:

- Professional clinical judgment
- Regulatory authority
- Legal review

This repository governs how we build systems, not how external parties must use them.

---

## Status

This repository is **active and binding**.

The governance framework includes:

- 19 governance artifacts
- 2 automated governance workflows
- Comprehensive coverage of authority, AI governance, security, operations, compliance, and personnel

All updates follow formal change control and are recorded in [CHANGELOG.md](CHANGELOG.md).

**If a rule is not written here, it is not yet governed.**
