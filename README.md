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

## What Lives Here (Authoritative)

This repository includes the following organization-wide artifacts:

### Governance & Authority

- **[docs/governance.md](docs/governance.md)**
  Organizational authority model, precedence rules, and decision ownership.

- **[docs/change-control.md](docs/change-control.md)**
  How governance, security, and AI standards are proposed, reviewed, approved, and versioned.

### Security & Compliance

- **[SECURITY.md](SECURITY.md)**
  Baseline security expectations aligned with HIPAA and SOC 2.

- **[docs/data-protection.md](docs/data-protection.md)**
  Data handling, PHI boundaries, and privacy-by-design requirements.

### Responsible AI

- **[docs/responsible-ai.md](docs/responsible-ai.md)**
  Guardrails for explainability, determinism, human oversight, and validation.

### Contribution & Review

- **[CONTRIBUTING.md](CONTRIBUTING.md)**
  Expectations for pull requests, documentation, tests, and review discipline.

- **[CODEOWNERS](CODEOWNERS)**
  Binding ownership and approval requirements.

### Templates & Workflows

- [Issue templates](.github/ISSUE_TEMPLATE/)
- [Pull request templates](.github/PULL_REQUEST_TEMPLATE/)
- [Shared GitHub Actions workflows](.github/workflows/)

> **Note:** Some artifacts may initially exist as placeholders.
> Missing artifacts are treated as explicit gaps, not implied behavior.

---

## For New Team Members — Start Here

If you are new to 1520ai, read these in order:

1. **Governance & Authority**
   → [docs/governance.md](docs/governance.md)

2. **Responsible AI Principles**
   → [docs/responsible-ai.md](docs/responsible-ai.md)

3. **Security & Data Protection**
   → [SECURITY.md](SECURITY.md)

4. **Contribution Expectations**
   → [CONTRIBUTING.md](CONTRIBUTING.md)

These documents explain how decisions are made, who has authority, and what "done" means at 1520ai.

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

## AI-Specific Review Gates

AI-enabled systems at 1520ai are subject to additional review and validation gates, including:

- Model behavior validation
- Determinism and stability checks
- Human-in-the-loop enforcement
- Deployment and rollback controls

These requirements are defined in:

- [docs/responsible-ai.md](docs/responsible-ai.md)
- Product-specific governance documentation (e.g., Hospiclarity)

This repository defines the baseline. Product repositories may impose stricter controls.

---

## Change Control & Versioning

Governance artifacts in this repository are versioned and review-controlled.

All material changes require:

- A pull request
- Review by designated CODEOWNERS
- An entry in the governance changelog

Changes are tracked in:

- **[CHANGELOG.md](CHANGELOG.md)**

### Changelog Format

Governance changes are recorded in `CHANGELOG.md` using the following minimum structure:

| Field | Description |
| ----- | ----------- |
| Date | When the change was approved |
| Artifact(s) affected | Which document(s) changed |
| Nature of change | Policy, clarification, control tightening, etc. |
| Impact assessment | Behavioral, security, regulatory, or none |
| Approver(s) | Who approved the change |

This format supports audit reconstruction and avoids ambiguous or narrative-only change logs.

---

## Ownership & Escalation

### Repository Maintainers

- VP, AI Engineering
- VP, Technology & Engineering

(Defined explicitly in [CODEOWNERS](CODEOWNERS).)

In the event of a conflict, **CODEOWNERS is the binding source of truth** for approval and ownership.

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

This repository is foundational and evolving.

Early revisions should be expected as:

- Governance artifacts are locked
- Security and AI controls mature
- Audit-readiness requirements expand

**Silence is not assumed.**
If a rule is not written here, it is not yet governed.
