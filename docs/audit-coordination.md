# 1520ai — Audit Coordination & Compliance

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** Organization-wide
**Audience:** Compliance, security, engineering, leadership, auditors

---

## 1. Purpose

This document defines how 1520ai coordinates with external auditors, maintains audit-ready documentation, and tracks compliance attestations.

Audit coordination ensures that:

- Governance artifacts are versioned and audit-ready
- External audits are efficiently supported
- Findings are tracked to resolution
- Compliance status is attestable at any point in time
- Regulatory correspondence is preserved

**Audit readiness is an ongoing discipline, not an event-driven scramble.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/change-control.md](change-control.md) — Change and exception mechanics
- [SECURITY.md](../SECURITY.md) — Security reporting and incident handling
- [docs/data-protection.md](data-protection.md) — Data handling and PHI requirements

Audit coordination is a compliance function with authority over audit-related processes.

---

## 3. Audit Types

### 3.1 External Audits

| Audit Type | Frequency | Scope | Primary Owner |
| ---------- | --------- | ----- | ------------- |
| SOC 2 Type II | Annual | Security controls, availability, confidentiality | Security + Compliance |
| HIPAA Assessment | Annual | PHI handling, privacy, security | Compliance |
| Penetration Test | Annual | Technical security vulnerabilities | Security |
| Vendor Audits | As requested | Customer-specific requirements | Compliance |
| Regulatory Examination | As required | Regulatory compliance | Compliance + Legal |

### 3.2 Internal Audits

| Audit Type | Frequency | Scope | Primary Owner |
| ---------- | --------- | ----- | ------------- |
| Governance Review | Quarterly | Governance artifact compliance | Compliance |
| Access Review | Quarterly | User access appropriateness | Security |
| Exception Review | Quarterly | Active exception validity | Compliance |
| Incident Review | After incidents | Incident response effectiveness | Security |

---

## 4. Audit Artifact Management

### 4.1 Artifact Categories

| Category | Examples | Retention |
| -------- | -------- | --------- |
| **Governance** | Policies, standards, procedures | Permanent (versioned) |
| **Evidence** | Logs, screenshots, configurations | 6 years minimum |
| **Assessments** | Risk assessments, security reviews | 6 years minimum |
| **Certifications** | SOC 2 reports, attestations | 6 years minimum |
| **Correspondence** | Regulatory letters, audit communications | 6 years minimum |

### 4.2 Artifact Versioning

All governance artifacts MUST be versioned to support audit reconstruction:

| Requirement | Implementation |
| ----------- | -------------- |
| Version control | Git-based versioning for all documents |
| Change history | CHANGELOG.md for material changes |
| Point-in-time access | Git tags for audit snapshots |
| Attribution | Commit history and PR approvals |

### 4.3 Audit Snapshots

Before major audits, create a versioned snapshot:

```text
Snapshot Format: audit-YYYY-MM-DD-[audit-type]

Example: audit-2026-03-15-soc2
```

Snapshots include:

- Git tag of repository state
- Export of relevant documentation
- Evidence collection status
- Open findings status

---

## 5. Audit Preparation

### 5.1 Pre-Audit Checklist

| Task | Timeline | Owner |
| ---- | -------- | ----- |
| Confirm audit scope and timeline | 8 weeks before | Compliance |
| Identify evidence requirements | 6 weeks before | Compliance |
| Assign evidence owners | 6 weeks before | Compliance |
| Collect and organize evidence | 4 weeks before | Evidence owners |
| Review open findings status | 4 weeks before | Finding owners |
| Conduct readiness review | 2 weeks before | Compliance |
| Create audit snapshot | 1 week before | Compliance |
| Brief participating teams | 1 week before | Compliance |

### 5.2 Evidence Collection

Evidence collection requirements:

| Requirement | Description |
| ----------- | ----------- |
| Completeness | All requested evidence provided |
| Currency | Evidence reflects current state |
| Accuracy | Evidence accurately represents controls |
| Attribution | Evidence source is documented |
| Confidentiality | Sensitive evidence handled appropriately |

### 5.3 Auditor Communication

| Communication Type | Channel | Timing |
| ------------------ | ------- | ------ |
| Formal requests | Email with tracking | As received |
| Clarifications | Email or scheduled calls | Within 2 business days |
| Evidence delivery | Secure file transfer | Per agreed schedule |
| Issue escalation | Scheduled meeting | As needed |

---

## 6. During Audit

### 6.1 Audit Support

| Role | Responsibilities |
| ---- | ---------------- |
| **Audit Coordinator** | Primary auditor contact, scheduling, logistics |
| **Evidence Owners** | Provide evidence, answer questions for their domain |
| **Subject Matter Experts** | Technical explanations, walkthroughs |
| **Executive Sponsor** | Escalation, strategic decisions |

### 6.2 Communication Protocol

- All auditor requests logged and tracked
- Response deadlines monitored
- Daily status updates during active audit periods
- Escalation path for delayed responses

### 6.3 Issue Management

Issues identified during audit:

1. Document issue immediately
2. Assess severity and scope
3. Determine if immediate remediation possible
4. Communicate status to auditor
5. Add to finding tracker

---

## 7. Finding Management

### 7.1 Finding Classification

| Severity | Definition | Response Timeline |
| -------- | ---------- | ----------------- |
| **Critical** | Significant control failure, immediate risk | Immediate remediation plan, 30-day resolution |
| **High** | Material control weakness | 60-day remediation |
| **Medium** | Control improvement needed | 90-day remediation |
| **Low** | Minor improvement opportunity | Next audit cycle |
| **Observation** | Best practice recommendation | Consider for future |

### 7.2 Finding Tracking

All findings MUST be tracked with:

| Field | Description |
| ----- | ----------- |
| Finding ID | Unique identifier |
| Source | Which audit identified the finding |
| Date Identified | When finding was raised |
| Severity | Critical / High / Medium / Low / Observation |
| Description | What the finding is |
| Root Cause | Why the finding exists |
| Remediation Plan | How it will be addressed |
| Owner | Who is responsible for remediation |
| Due Date | When remediation is due |
| Status | Open / In Progress / Remediated / Verified / Closed |
| Evidence | Proof of remediation |
| Closure Date | When finding was closed |

### 7.3 Finding Registry Template

```text
## Finding: [Finding ID]

### Overview

| Field | Value |
| ----- | ----- |
| Source | [Audit name and date] |
| Severity | Critical / High / Medium / Low |
| Status | Open / In Progress / Remediated / Verified / Closed |
| Owner | |
| Due Date | |

### Description

[What the finding is]

### Root Cause

[Why this finding exists]

### Remediation Plan

[Steps to address the finding]

### Progress Notes

| Date | Update |
| ---- | ------ |
| | |

### Closure

- [ ] Remediation implemented
- [ ] Evidence collected
- [ ] Verified by compliance
- [ ] Accepted by auditor (if applicable)
```

### 7.4 Remediation Process

1. **Acknowledge** — Accept finding and assign owner
2. **Analyze** — Determine root cause and remediation approach
3. **Plan** — Document remediation steps and timeline
4. **Execute** — Implement remediation
5. **Evidence** — Collect proof of remediation
6. **Verify** — Internal verification of effectiveness
7. **Close** — Obtain auditor acceptance (if required)

---

## 8. Compliance Attestation

### 8.1 Attestation Types

| Type | Purpose | Frequency | Authority |
| ---- | ------- | --------- | --------- |
| **SOC 2 Attestation** | Control effectiveness | Annual | External auditor |
| **HIPAA Attestation** | PHI compliance | Annual | Compliance leadership |
| **Security Attestation** | Security posture | Quarterly | Security leadership |
| **Governance Attestation** | Governance compliance | Quarterly | Compliance leadership |

### 8.2 Attestation Requirements

Each attestation MUST include:

| Element | Description |
| ------- | ----------- |
| Scope | What is being attested |
| Period | Time period covered |
| Standards | Criteria used for assessment |
| Findings | Summary of open findings |
| Exceptions | Active governance exceptions |
| Attestor | Who is making the attestation |
| Date | When attestation was made |
| Evidence | Supporting documentation |

### 8.3 Attestation Template

```text
## Compliance Attestation

**Attestation Type:** [Type]
**Period:** [Start Date] to [End Date]
**Date:** [Attestation Date]
**Attestor:** [Name and Title]

### Scope

[What this attestation covers]

### Standards

[Criteria used for assessment]

### Assessment Summary

[Summary of compliance status]

### Open Findings

| Finding ID | Severity | Status | Due Date |
| ---------- | -------- | ------ | -------- |
| | | | |

### Active Exceptions

| Exception ID | Scope | Expiration |
| ------------ | ----- | ---------- |
| | | |

### Attestation Statement

I attest that, to the best of my knowledge, the systems and processes
within the scope of this attestation comply with the stated standards,
subject to the findings and exceptions noted above.

**Signature:** _______________
**Date:** _______________
```

---

## 9. Regulatory Correspondence

### 9.1 Correspondence Types

| Type | Examples | Handling |
| ---- | -------- | -------- |
| **Regulatory Inquiries** | Information requests, clarifications | Legal + Compliance review |
| **Examination Notices** | Audit notifications, examination letters | Executive notification |
| **Enforcement Actions** | Warnings, citations, penalties | Legal + Executive |
| **Guidance Updates** | New regulations, guidance changes | Compliance review |

### 9.2 Correspondence Management

All regulatory correspondence MUST be:

- Logged upon receipt
- Routed to appropriate parties within 24 hours
- Responded to within required timelines
- Archived with full documentation

### 9.3 Response Process

1. **Receipt** — Log and acknowledge correspondence
2. **Triage** — Assess urgency and route appropriately
3. **Review** — Legal and compliance review of content
4. **Response** — Draft response with appropriate approvals
5. **Submission** — Submit response via required channel
6. **Archive** — Store correspondence and response

### 9.4 Correspondence Log

| Field | Description |
| ----- | ----------- |
| Reference | Unique identifier |
| Received Date | When correspondence received |
| Source | Regulatory body |
| Type | Inquiry / Notice / Action / Guidance |
| Subject | Brief description |
| Response Due | Deadline for response |
| Owner | Who is handling |
| Status | Open / In Progress / Responded / Closed |
| Response Date | When response submitted |
| Archive Location | Where documents stored |

---

## 10. Audit Calendar

### 10.1 Annual Audit Schedule

Maintain an annual audit calendar with:

| Audit | Q1 | Q2 | Q3 | Q4 |
| ----- | -- | -- | -- | -- |
| SOC 2 Type II | | Fieldwork | | Report |
| HIPAA Assessment | | | Assessment | |
| Penetration Test | | Test | | |
| Internal Governance | Review | Review | Review | Review |
| Access Review | Review | Review | Review | Review |

### 10.2 Calendar Maintenance

- Review calendar quarterly
- Update for new audit requirements
- Coordinate with external auditor schedules
- Account for remediation timelines

---

## 11. Continuous Compliance

### 11.1 Ongoing Activities

| Activity | Frequency | Owner |
| -------- | --------- | ----- |
| Control monitoring | Continuous | Security |
| Evidence refresh | Monthly | Evidence owners |
| Finding status review | Weekly | Finding owners |
| Governance health check | Weekly (automated) | Compliance |
| Exception review | Monthly | Compliance |

### 11.2 Compliance Metrics

Track and report:

| Metric | Target | Frequency |
| ------ | ------ | --------- |
| Open critical findings | 0 | Weekly |
| Finding remediation on-time | >90% | Monthly |
| Evidence collection completeness | 100% | Pre-audit |
| Audit preparation readiness | Green | Pre-audit |

---

## 12. Enforcement

Audit coordination requirements are enforced through:

- Audit preparation checklists
- Finding tracking and escalation
- Compliance reporting to leadership
- Governance review processes

**Failure to support audits or remediate findings is a governance violation.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
