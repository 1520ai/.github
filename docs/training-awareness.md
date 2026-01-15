# 1520ai — Training & Awareness Program

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** Organization-wide
**Audience:** All personnel, HR, compliance, leadership

---

## 1. Purpose

This document defines training and awareness requirements for 1520ai personnel working with AI systems, healthcare data, and governance processes.

Training ensures that:

- Personnel understand their compliance obligations
- Security and privacy practices are consistently applied
- AI-specific risks are understood and mitigated
- Governance processes are followed correctly
- Regulatory requirements are met

**Untrained personnel are a governance risk.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/responsible-ai.md](responsible-ai.md) — AI posture and constraints
- [docs/data-protection.md](data-protection.md) — Data handling and PHI requirements
- [SECURITY.md](../SECURITY.md) — Security reporting and incident handling

Training completion is a prerequisite for system access and certain role assignments.

---

## 3. Training Categories

### 3.1 Required Training Matrix

| Training | Audience | Frequency | Duration | Owner |
| -------- | -------- | --------- | -------- | ----- |
| **Security Awareness** | All personnel | Annual | 1 hour | Security |
| **HIPAA Privacy** | All personnel | Annual | 1 hour | Compliance |
| **HIPAA Security** | Technical staff | Annual | 2 hours | Compliance |
| **Responsible AI** | AI/ML teams | Annual | 2 hours | AI Engineering |
| **AI Security** | AI/ML teams | Annual | 2 hours | Security |
| **Incident Response** | On-call personnel | Annual | 1 hour | Security |
| **Governance Overview** | New hires | Onboarding | 1 hour | Compliance |
| **Data Handling** | Data access roles | Annual | 1 hour | Compliance |

### 3.2 Role-Based Training

| Role | Additional Required Training |
| ---- | ---------------------------- |
| **AI/ML Engineer** | Responsible AI, AI Security, Model Governance |
| **Data Engineer** | Data Lineage, PHI Handling, De-identification |
| **Security Engineer** | AI Security, Incident Response, Penetration Testing Ethics |
| **Compliance Staff** | Audit Coordination, Exception Management, Regulatory Updates |
| **People Manager** | Governance Overview, Incident Escalation, Training Administration |
| **On-Call Engineer** | Incident Response, BC/DR Procedures, Escalation Protocols |

### 3.3 Specialized Training

| Training | Audience | Trigger | Duration |
| -------- | -------- | ------- | -------- |
| **PHI Access Training** | PHI-accessing roles | Before access granted | 2 hours |
| **Production Access** | Production deployers | Before access granted | 1 hour |
| **Vendor Management** | Vendor liaisons | Before vendor engagement | 1 hour |
| **Audit Support** | Evidence owners | Before audit participation | 1 hour |

---

## 4. Onboarding Requirements

### 4.1 New Hire Onboarding

All new hires MUST complete within first 30 days:

| Training | Timeline | Verification |
| -------- | -------- | ------------ |
| Security Awareness | Week 1 | Quiz completion |
| HIPAA Privacy | Week 1 | Quiz completion |
| Governance Overview | Week 2 | Acknowledgment |
| Role-specific training | Week 2-4 | Manager verification |

### 4.2 Onboarding Checklist

```text
## New Hire Training Checklist

Employee: ________________
Start Date: ________________
Manager: ________________

### Week 1
- [ ] Security Awareness training completed
- [ ] HIPAA Privacy training completed
- [ ] Acceptable Use Policy acknowledged
- [ ] Security policies reviewed

### Week 2
- [ ] Governance Overview completed
- [ ] Team-specific orientation completed
- [ ] Access requests submitted (with training prerequisites met)

### Week 3-4
- [ ] Role-specific training completed
- [ ] System access granted (after training verification)
- [ ] Mentor/buddy assigned for ongoing questions

### Manager Sign-off
- [ ] All required training completed
- [ ] Employee understands escalation procedures
- [ ] Employee added to appropriate communication channels

Manager Signature: ________________ Date: ________________
```

### 4.3 Contractor Onboarding

Contractors with system access MUST complete:

- Security Awareness training
- HIPAA training (if PHI access)
- NDA and acceptable use acknowledgment
- Role-specific training as applicable

---

## 5. Training Content Requirements

### 5.1 Security Awareness

| Topic | Coverage |
| ----- | -------- |
| Phishing and social engineering | Recognition and reporting |
| Password and authentication | Strong passwords, MFA, no sharing |
| Physical security | Badge usage, visitor policy, clean desk |
| Data handling | Classification, transmission, disposal |
| Incident reporting | How to report security concerns |
| Acceptable use | Policy overview and acknowledgment |

### 5.2 HIPAA Training

| Topic | Coverage |
| ----- | -------- |
| PHI definition | What constitutes PHI |
| Privacy Rule | Patient rights, minimum necessary |
| Security Rule | Administrative, physical, technical safeguards |
| Breach notification | What constitutes a breach, reporting |
| Penalties | Consequences of non-compliance |
| 1520ai-specific | Our PHI handling procedures |

### 5.3 Responsible AI Training

| Topic | Coverage |
| ----- | -------- |
| AI risks in healthcare | Patient safety, bias, reliability |
| Sensitivity × Consensus | Risk classification framework |
| Human-in-the-loop | When and how humans review AI outputs |
| Bias and fairness | Detection, mitigation, monitoring |
| Transparency | Explainability requirements |
| Release gates | Pre-production validation requirements |

### 5.4 AI Security Training

| Topic | Coverage |
| ----- | -------- |
| AI threat model | Prompt injection, jailbreaking, data extraction |
| The lethal trifecta | Understanding and avoiding dangerous combinations |
| Input validation | Securing AI inputs |
| Output validation | Validating and filtering AI outputs |
| Secure prompt design | Protecting system prompts |
| Security testing | How to test AI systems for security |

---

## 6. Training Delivery

### 6.1 Delivery Methods

| Method | Use Case | Tracking |
| ------ | -------- | -------- |
| **Online modules** | Standard compliance training | LMS completion records |
| **Live sessions** | Complex topics, Q&A needed | Attendance records |
| **Self-paced reading** | Policy acknowledgment | Signed acknowledgment |
| **Hands-on workshops** | Technical skills | Completion certificates |
| **Tabletop exercises** | Incident response | Participation records |

### 6.2 Learning Management

Training is tracked through:

| System | Purpose |
| ------ | ------- |
| LMS (Learning Management System) | Course delivery, completion tracking |
| HR system | Training records, compliance reporting |
| Access management | Training prerequisite enforcement |

### 6.3 Training Materials

All training materials MUST be:

- Version controlled
- Reviewed annually for accuracy
- Updated when policies change
- Accessible to all required personnel
- Available in appropriate formats (accessibility)

---

## 7. Assessment and Verification

### 7.1 Assessment Requirements

| Training Type | Assessment Method | Passing Score |
| ------------- | ----------------- | ------------- |
| Compliance training | Quiz | 80% |
| Technical training | Practical assessment | Competency demonstration |
| Policy acknowledgment | Signature | N/A |
| Hands-on workshop | Completion | Instructor verification |

### 7.2 Failed Assessments

If an employee fails a required assessment:

1. Immediate retake allowed (once)
2. If second failure, manager notified
3. Remedial training assigned
4. Access restricted until training completed
5. Third failure escalated to HR

### 7.3 Verification Process

| Verification | Method | Timing |
| ------------ | ------ | ------ |
| Training completion | LMS records | Real-time |
| Access prerequisites | Automated check | At access request |
| Annual compliance | Compliance report | Monthly |
| Audit evidence | Training records export | As needed |

---

## 8. Compliance Tracking

### 8.1 Training Compliance Report

| Metric | Target | Frequency |
| ------ | ------ | --------- |
| Overall compliance rate | 100% | Monthly |
| Overdue training | 0 | Weekly |
| New hire completion | 100% within 30 days | Weekly |
| Annual training renewal | 100% on time | Monthly |

### 8.2 Non-Compliance Escalation

| Overdue | Action |
| ------- | ------ |
| 7 days | Automated reminder to employee |
| 14 days | Manager notification |
| 30 days | Access suspension warning |
| 45 days | Access suspended, HR escalation |

### 8.3 Compliance Dashboard

Track and display:

- Training completion by department
- Overdue training by category
- Upcoming training deadlines
- Compliance trends over time

---

## 9. Awareness Program

### 9.1 Ongoing Awareness Activities

| Activity | Frequency | Owner |
| -------- | --------- | ----- |
| Security newsletter | Monthly | Security |
| Phishing simulations | Quarterly | Security |
| AI ethics discussions | Quarterly | AI Engineering |
| Policy update communications | As needed | Compliance |
| Incident lessons learned | After incidents | Security |

### 9.2 Awareness Topics

Rotate awareness communications through:

- Current threat landscape
- Recent incidents (anonymized)
- Policy reminders
- Best practices
- New tool/process introductions
- Regulatory updates

### 9.3 Phishing Simulation Program

| Element | Requirement |
| ------- | ----------- |
| Frequency | Quarterly minimum |
| Scenarios | Varied, realistic |
| Reporting | Click rates, report rates |
| Follow-up | Immediate training for clickers |
| Trending | Track improvement over time |

---

## 10. Training Records

### 10.1 Record Retention

| Record Type | Retention Period |
| ----------- | ---------------- |
| Training completion records | Duration of employment + 6 years |
| Assessment results | Duration of employment + 6 years |
| Training materials (versions) | 6 years after superseded |
| Acknowledgments | Duration of employment + 6 years |

### 10.2 Record Contents

Training records MUST include:

| Field | Description |
| ----- | ----------- |
| Employee ID | Unique identifier |
| Training name | Course or module name |
| Training version | Version of training material |
| Completion date | When training completed |
| Assessment score | If applicable |
| Expiration date | When renewal required |
| Delivery method | How training was delivered |

### 10.3 Audit Access

Training records available for:

- Internal compliance audits
- External regulatory audits
- HR employment verification
- Manager compliance reviews

---

## 11. Special Populations

### 11.1 Executives and Leadership

Leadership MUST complete:

- All standard required training
- Governance authority training
- Regulatory responsibility overview
- Incident command training (as applicable)

### 11.2 Temporary and Contract Workers

| Duration | Training Requirements |
| -------- | --------------------- |
| < 30 days | Security basics, NDA |
| 30-90 days | Full security awareness, role-specific |
| > 90 days | All training same as employees |

### 11.3 Third-Party Personnel

Third parties with system access:

- Must provide evidence of equivalent training, OR
- Must complete 1520ai training before access

---

## 12. Training Program Governance

### 12.1 Roles and Responsibilities

| Role | Responsibilities |
| ---- | ---------------- |
| **Compliance** | Training program oversight, compliance reporting |
| **HR** | Onboarding coordination, record management |
| **Security** | Security training content, phishing program |
| **AI Engineering** | AI-specific training content |
| **Managers** | Team training compliance, remediation support |
| **Employees** | Complete training on time, apply learning |

### 12.2 Training Review

| Activity | Frequency | Owner |
| -------- | --------- | ----- |
| Content accuracy review | Annual | Content owners |
| Effectiveness assessment | Annual | Compliance |
| Regulatory alignment check | Annual | Compliance |
| Feedback incorporation | Ongoing | Content owners |

### 12.3 Training Effectiveness

Measure effectiveness through:

- Assessment scores and trends
- Phishing simulation results
- Incident root cause analysis (training gaps)
- Employee feedback
- Compliance audit findings

---

## 13. Exceptions

Exceptions to training requirements:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include compensating controls
- MUST be time-bounded
- MUST be approved by Compliance and HR leadership

Extended leave or accommodation situations handled case-by-case with HR.

---

## 14. Enforcement

Training requirements are enforced through:

- Access management integration (training prerequisites)
- Manager accountability for team compliance
- Compliance reporting to leadership
- Performance review integration
- Access suspension for non-compliance

**Access to systems without required training is a governance violation.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
