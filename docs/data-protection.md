# 1520ai — Data Protection & Privacy Principles

**Status:** Active
**Effective Date:** 2026-01-01
**Scope:** Organization-wide
**Audience:** Internal teams, auditors, partners, enterprise customers

---

## 1. Purpose

This document defines how 1520ai approaches the protection, handling, and governance of sensitive data, including healthcare data.

Data protection at 1520ai is not treated as a legal afterthought or a downstream compliance exercise. It is an engineering and governance constraint that informs system design, operational workflows, and AI behavior.

This document establishes principles and expectations.
Enforceable controls are implemented at the system, infrastructure, and product levels.

---

## 2. Core Principles (Quick Reference)

1520ai's approach to data protection emphasizes:

- **Minimization over accumulation** — Collect only what is required
- **Containment over distribution** — Data does not move unless necessary
- **Accountability over implicit trust** — Every interaction is attributable and reviewable

These principles inform all sections of this document.

---

## 3. Scope

This policy applies to:

- All data processed, stored, or transmitted by 1520ai systems
- All environments (development, staging, production)
- All AI models, agents, prompts, and evaluation pipelines
- All logs, metrics, artifacts, and derived outputs

This includes—but is not limited to—protected health information (PHI) and other sensitive or regulated data.

---

## 4. Core Data Protection Principle

**Data protection is achieved through minimization, containment, and accountability — not trust.**

Accordingly:

- Access is limited by default
- Data flows are explicitly defined
- Sensitive data does not move unless required
- Every interaction is attributable and reviewable

---

## 5. Data Classification

1520ai recognizes the following high-level data classes:

| Classification | Description |
|----------------|-------------|
| **Public / Non-Sensitive** | Information intended for unrestricted use |
| **Internal / Confidential** | Business, operational, or technical information not intended for public disclosure |
| **Sensitive / Regulated** | Includes PHI, personal data, and any data subject to contractual or regulatory constraints |

Handling requirements scale with sensitivity.

---

## 6. Data Minimization

Systems MUST be designed to:

- Collect only data required for a defined purpose
- Avoid unnecessary duplication or persistence
- Prefer derived, structured, or de-identified representations where possible

**Data minimization is a design-time requirement, not a post-hoc cleanup activity.**

---

## 7. Data Locality & Sovereignty

Where sensitive or regulated data is involved:

- Data SHOULD remain within defined security perimeters
- Cross-boundary data movement MUST be explicitly justified
- External transmission or processing requires documented approval

**Local-first or perimeter-bound execution models are strongly preferred for healthcare contexts.**

---

## 8. Access Control & Least Privilege

Access to sensitive data is governed by:

- Role-based access controls
- Principle of least privilege
- Explicit approval for elevated access

**Access grants are treated as revocable privileges, not entitlements.**

---

## 9. Logging, Monitoring & Auditability

Data access and handling MUST be:

- Logged for all access to sensitive or regulated data
- Attributable to a system or individual
- Reviewable during audits or incident investigations

For PHI specifically:

- Access logging is mandatory, not optional
- Logs MUST record who accessed what and when
- Logs MUST be retained for at least six years or as required by law

Logs must balance:

- Audit utility
- Security
- Avoidance of unnecessary sensitive data exposure in the logs themselves

**Do not log the sensitive content—log the access event.**

---

## 10. Data Retention & Disposal

### Retention

- Data SHOULD be retained only as long as required for its defined purpose
- Retention periods for regulated data MUST comply with applicable legal and contractual requirements
- Product-specific retention schedules are defined in product governance documentation

### Disposal

- Data disposal MUST follow secure destruction procedures
- Disposal of PHI or other regulated data MUST be documented
- Backups and replicas MUST be included in disposal planning

**Data that is no longer needed is a liability, not an asset.**

---

## 11. AI-Specific Data Considerations

When data is used in AI systems:

- Training, inference, and evaluation contexts must be explicitly separated
- Sensitive data MUST NOT be reused for training without review and approval
- AI outputs must not leak sensitive inputs through memorization or inference

**AI systems are expected to respect the same data boundaries as human operators.**

---

## 12. PHI & Healthcare Data

For systems involving PHI:

- HIPAA expectations apply by default
- PHI handling is treated as high-risk, high-sensitivity
- Accidental exposure is treated as a security incident

Controls such as PHI detection, scanning, or tripwires are recommended safeguards, not compliance guarantees.

---

## 13. Third-Party & Vendor Considerations

Use of third-party tools or services that interact with sensitive data requires:

- Understanding of data flows
- Clarity on storage, retention, and reuse
- Alignment with contractual and regulatory obligations

For PHI specifically:

- Third parties MUST execute a Business Associate Agreement (BAA) before receiving or processing PHI
- Vendors MUST demonstrate HIPAA compliance

**Vendors must not expand data use beyond the stated purpose.**

---

## 14. Data Subject Rights

Where applicable, 1520ai systems should support:

- **Access requests** — Individuals may request information about data held about them
- **Correction requests** — Individuals may request correction of inaccurate data
- **Deletion requests** — Individuals may request deletion of data, subject to legal retention requirements

Product-specific implementations of data subject rights are documented in product governance.

---

## 15. Incident Handling

Suspected or confirmed data protection failures MUST:

- Be escalated per [SECURITY.md](../SECURITY.md)
- Be treated as incidents, not defects
- Trigger investigation, containment, and remediation

Data protection incidents may require:

- Regulatory notification assessment
- Governance review
- Changes to controls or architecture

---

## 16. Relationship to Governance & Security

- Authority and precedence are defined in [docs/governance.md](governance.md)
- Change and exception handling follow [docs/change-control.md](change-control.md)
- Security escalation follows [SECURITY.md](../SECURITY.md)
- Responsible AI constraints are defined in [docs/responsible-ai.md](responsible-ai.md)

In the event of conflict:

**Implemented security and data protection controls take precedence over convenience or undocumented intent.**

---

## 17. Exceptions

Temporary deviations from this policy:

- Require formal approval
- Must be documented in [docs/EXCEPTIONS.md](EXCEPTIONS.md)
- Must be time-bounded and justified

**Undocumented deviations are considered non-compliant.**

---

## 18. Summary

1520ai's approach to data protection ensures that sensitive data is handled responsibly while enabling innovation in regulated environments.

| Principle | Meaning |
|-----------|---------|
| **Minimization** | Collect only what is required |
| **Containment** | Data does not move unless necessary |
| **Accountability** | Every interaction is attributable |

---

## Status

This policy is **active and binding**.

All material changes follow formal change control and are recorded in `CHANGELOG.md`.
