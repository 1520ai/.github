# 1520ai — Vendor Management & Third-Party Governance

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** All third-party vendors and integrations
**Audience:** Engineering, procurement, security, compliance, legal

---

## 1. Purpose

This document defines requirements for evaluating, onboarding, and managing third-party vendors whose products or services interact with 1520ai systems or data.

Vendor management ensures that:

- Third-party risks are assessed before engagement
- PHI and sensitive data are protected in vendor relationships
- Business Associate Agreements are executed where required
- Vendor changes are communicated and managed
- Ongoing compliance is monitored

**No vendor may access PHI or integrate with production systems without completing the vendor qualification process.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/data-protection.md](data-protection.md) — Data handling and PHI requirements
- [SECURITY.md](../SECURITY.md) — Security reporting and incident handling
- [docs/change-control.md](change-control.md) — Change and exception mechanics

Vendor relationships involving PHI require compliance leadership approval.

---

## 3. Vendor Classification

### 3.1 Classification Tiers

Vendors are classified based on data access and system integration:

| Tier | Definition | Examples | Requirements |
| ---- | ---------- | -------- | ------------ |
| **Tier 1** | Direct PHI access or processing | EHR integrations, cloud hosting with PHI | Full assessment, BAA required |
| **Tier 2** | Indirect PHI exposure or sensitive data | Analytics tools, monitoring services | Security assessment, DPA required |
| **Tier 3** | No sensitive data access | Development tools, office software | Basic assessment |
| **Tier 4** | Public/open source | Open source libraries, public APIs | License review only |

### 3.2 Classification Criteria

| Factor | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
| ------ | ------ | ------ | ------ | ------ |
| PHI Access | Yes | Possible/Indirect | No | No |
| Production Integration | Yes | Yes | Limited | No |
| Data Storage | Stores our data | May process data | No data | No data |
| Authentication Integration | Yes | Possible | No | No |

---

## 4. Vendor Qualification Process

### 4.1 Process Overview

```text
[Request] → [Classification] → [Assessment] → [Legal Review] → [Approval] → [Onboarding]
                                     ↓
                              [Risk Assessment]
```

### 4.2 Step 1: Vendor Request

Requestor MUST provide:

| Field | Description |
| ----- | ----------- |
| Vendor Name | Company name |
| Product/Service | What we're procuring |
| Business Need | Why this vendor is needed |
| Data Involved | What data the vendor will access |
| Integration Scope | How the vendor integrates with our systems |
| Requestor | Who is requesting |
| Sponsor | Business owner for the relationship |

### 4.3 Step 2: Classification

Security and compliance determine vendor tier based on:

- Data access requirements
- System integration scope
- Regulatory implications

### 4.4 Step 3: Security Assessment

Assessment requirements by tier:

| Tier | Assessment Requirements |
| ---- | ----------------------- |
| Tier 1 | Full security questionnaire, SOC 2 review, penetration test results, architecture review |
| Tier 2 | Security questionnaire, SOC 2 or equivalent, privacy policy review |
| Tier 3 | Basic security questionnaire, privacy policy review |
| Tier 4 | License compatibility check |

### 4.5 Step 4: Legal Review

| Tier | Legal Requirements |
| ---- | ------------------ |
| Tier 1 | BAA execution, MSA review, liability assessment |
| Tier 2 | DPA execution, MSA review |
| Tier 3 | Terms of service review |
| Tier 4 | License review |

### 4.6 Step 5: Approval

| Tier | Approval Authority |
| ---- | ------------------ |
| Tier 1 | Security Lead + Compliance Lead + Legal |
| Tier 2 | Security Lead + Engineering Lead |
| Tier 3 | Engineering Lead |
| Tier 4 | Team Lead |

### 4.7 Step 6: Onboarding

Post-approval onboarding includes:

- Access provisioning (least privilege)
- Integration configuration
- Monitoring setup
- Documentation in vendor registry

---

## 5. Security Assessment

### 5.1 Security Questionnaire Topics

The security questionnaire covers:

| Category | Topics |
| -------- | ------ |
| **Organization** | Company background, certifications, insurance |
| **Data Security** | Encryption (at rest, in transit), key management |
| **Access Control** | Authentication, authorization, audit logging |
| **Infrastructure** | Hosting, network security, physical security |
| **Application Security** | SDLC, vulnerability management, penetration testing |
| **Incident Response** | Breach notification, incident handling |
| **Business Continuity** | Backup, disaster recovery, availability SLAs |
| **Compliance** | HIPAA, SOC 2, GDPR, other certifications |

### 5.2 Required Documentation

| Tier | Required Documents |
| ---- | ------------------ |
| Tier 1 | SOC 2 Type II report, penetration test summary, security whitepaper, BAA |
| Tier 2 | SOC 2 report (Type I or II), security documentation, DPA |
| Tier 3 | Privacy policy, security overview |
| Tier 4 | License file |

### 5.3 Assessment Outcomes

| Outcome | Definition | Action |
| ------- | ---------- | ------ |
| **Approved** | Meets all requirements | Proceed to legal review |
| **Conditional** | Meets requirements with mitigations | Document mitigations, proceed with conditions |
| **Deferred** | Requires additional information | Request information, reassess |
| **Rejected** | Does not meet requirements | Do not proceed, document rationale |

---

## 6. Business Associate Agreements (BAA)

### 6.1 When BAA is Required

A BAA is REQUIRED when a vendor:

- Will access, receive, or store PHI
- Will create, maintain, or transmit PHI on our behalf
- Provides services that involve PHI exposure

### 6.2 BAA Requirements

All BAAs MUST include:

| Requirement | Description |
| ----------- | ----------- |
| Permitted Uses | Specific permitted uses of PHI |
| Safeguards | Required administrative, physical, and technical safeguards |
| Reporting | Breach notification requirements and timelines |
| Subcontractors | Requirements for downstream business associates |
| Return/Destruction | PHI return or destruction upon termination |
| Audit Rights | Right to audit compliance |
| Term and Termination | Duration and termination conditions |

### 6.3 BAA Execution

BAAs MUST be:

- Executed before any PHI access
- Reviewed by legal counsel
- Signed by authorized signatories
- Stored in the vendor registry

### 6.4 BAA Tracking

| Field | Description |
| ----- | ----------- |
| Vendor | Vendor name |
| BAA Date | Execution date |
| Expiration | Expiration date (if applicable) |
| Signatory | Who signed for 1520ai |
| Document Location | Where BAA is stored |
| Review Date | Next review date |

---

## 7. Data Processing Agreements (DPA)

### 7.1 When DPA is Required

A DPA is REQUIRED when a vendor:

- Processes personal data on our behalf
- Is subject to GDPR or similar privacy regulations
- Handles sensitive data that doesn't qualify as PHI

### 7.2 DPA Requirements

All DPAs MUST include:

| Requirement | Description |
| ----------- | ----------- |
| Processing Purpose | Specific purposes for data processing |
| Data Categories | Types of data being processed |
| Security Measures | Required security controls |
| Subprocessors | Requirements for downstream processors |
| Data Subject Rights | Support for access, correction, deletion requests |
| Data Transfer | Cross-border transfer mechanisms |
| Audit Rights | Right to audit compliance |

---

## 8. Vendor Registry

### 8.1 Registry Requirements

All approved vendors MUST be documented in a vendor registry with:

| Field | Description |
| ----- | ----------- |
| Vendor ID | Unique identifier |
| Vendor Name | Company name |
| Tier | Classification tier |
| Product/Service | What we use them for |
| Data Access | What data they access |
| Status | Active / Suspended / Terminated |
| Owner | Internal relationship owner |
| BAA/DPA Status | Agreement status and dates |
| Assessment Date | Last security assessment |
| Review Due | Next review date |
| Contacts | Vendor security/privacy contacts |

### 8.2 Registry Location

Product repositories SHOULD maintain vendor registries in:

- `docs/vendors.md` or equivalent

This organization-level document defines requirements. Product repositories implement registries.

---

## 9. Ongoing Monitoring

### 9.1 Periodic Review

Vendors MUST be reviewed:

| Tier | Review Frequency |
| ---- | ---------------- |
| Tier 1 | Annually |
| Tier 2 | Every 18 months |
| Tier 3 | Every 2 years |
| Tier 4 | As needed |

### 9.2 Review Triggers

Unscheduled reviews are triggered by:

- Security incident involving the vendor
- Significant changes to vendor services
- Changes to data access requirements
- Vendor acquisition or ownership change
- Regulatory changes affecting the relationship
- Contract renewal

### 9.3 Monitoring Activities

| Activity | Frequency | Responsible |
| -------- | --------- | ----------- |
| SOC 2 report review | Annually (Tier 1-2) | Security |
| Access audit | Quarterly (Tier 1) | Security |
| Contract review | At renewal | Legal |
| Performance review | Annually | Business owner |

---

## 10. Vendor Changes

### 10.1 Change Notification Requirements

Vendors MUST notify 1520ai of:

| Change Type | Notification Timeline |
| ----------- | --------------------- |
| Security incidents | Immediately (per BAA) |
| Subprocessor changes | 30 days advance notice |
| Service changes affecting data | 30 days advance notice |
| Ownership/acquisition | As soon as practical |
| Certification changes | 30 days |

### 10.2 Internal Change Management

Changes to vendor relationships require:

| Change | Process |
| ------ | ------- |
| New vendor | Full qualification process |
| Scope expansion | Security reassessment, legal review |
| Tier change | Reclassification and appropriate assessment |
| Termination | Offboarding process |

---

## 11. Vendor Termination

### 11.1 Termination Process

When terminating a vendor relationship:

1. **Notification** — Provide required notice per contract
2. **Data Return/Destruction** — Obtain PHI/data return or destruction certification
3. **Access Revocation** — Revoke all system access
4. **Documentation** — Update vendor registry
5. **Verification** — Confirm all data handling requirements met

### 11.2 Data Handling at Termination

| Tier | Data Handling Requirement |
| ---- | ------------------------- |
| Tier 1 | Written certification of PHI destruction or return |
| Tier 2 | Confirmation of data deletion |
| Tier 3 | Access removal confirmation |
| Tier 4 | No specific requirement |

---

## 12. Exceptions

Exceptions to vendor management requirements:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include risk assessment and mitigations
- MUST be time-bounded
- MUST be approved by Security and Compliance leadership

Emergency vendor engagements MAY proceed with abbreviated assessment but MUST complete full qualification within 30 days.

---

## 13. Enforcement

Vendor management requirements are enforced through:

- Procurement process gates
- Security review requirements
- Legal contract review
- Audit and compliance review

**Engaging vendors without proper qualification is a governance violation.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
