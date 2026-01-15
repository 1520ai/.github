# 1520ai — Governance Metrics & KPIs

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** Organization-wide
**Audience:** Leadership, compliance, security, AI engineering

---

## 1. Purpose

This document defines metrics, key performance indicators (KPIs), and reporting requirements for governance health at 1520ai.

Governance metrics ensure that:

- Compliance posture is measurable and reportable
- Governance health is continuously monitored
- Trends are identified before they become problems
- Leadership has visibility into risk posture
- Audit evidence is readily available

**What gets measured gets managed.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/audit-coordination.md](audit-coordination.md) — Audit and compliance processes
- [docs/change-control.md](change-control.md) — Change and exception mechanics

Metrics inform governance decisions but do not override binding requirements.

---

## 3. Metric Categories

### 3.1 Category Overview

| Category | Purpose | Primary Owner |
| -------- | ------- | ------------- |
| **Compliance** | Regulatory and policy adherence | Compliance |
| **Security** | Security posture and incident trends | Security |
| **AI Governance** | AI-specific risk and control metrics | AI Engineering |
| **Operational** | Process health and efficiency | Operations |
| **Training** | Personnel readiness | HR/Compliance |

### 3.2 Metric Attributes

Each metric includes:

| Attribute | Description |
| --------- | ----------- |
| Name | Metric identifier |
| Definition | What is being measured |
| Formula | How metric is calculated |
| Target | Expected/acceptable value |
| Threshold | Warning and critical levels |
| Frequency | How often measured |
| Owner | Who is responsible |
| Data source | Where data comes from |

---

## 4. Compliance Metrics

### 4.1 Core Compliance KPIs

| Metric | Definition | Target | Threshold | Frequency |
| ------ | ---------- | ------ | --------- | --------- |
| **Policy Compliance Rate** | % of policies with documented compliance | 100% | Yellow: <95%, Red: <90% | Monthly |
| **Open Audit Findings** | Count of unresolved audit findings | 0 critical, <5 total | Red: Any critical open | Weekly |
| **Finding Remediation Rate** | % of findings remediated on time | >90% | Yellow: <90%, Red: <80% | Monthly |
| **Exception Count** | Number of active governance exceptions | Trending down | Red: >10 active | Monthly |
| **Exception Expiration** | Exceptions expiring in next 30 days | All planned for | Red: Any unplanned | Weekly |

### 4.2 Regulatory Compliance

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **HIPAA Training Compliance** | % of personnel with current HIPAA training | 100% | Monthly |
| **BAA Coverage** | % of PHI-accessing vendors with BAAs | 100% | Quarterly |
| **Privacy Complaints** | Number of privacy complaints received | 0 | Monthly |
| **Breach Incidents** | Number of reportable breaches | 0 | Monthly |

### 4.3 Documentation Health

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Document Currency** | % of governance docs reviewed in past year | 100% | Quarterly |
| **Changelog Completeness** | All changes documented in CHANGELOG | 100% | Per change |
| **Cross-Reference Integrity** | % of doc links that resolve correctly | 100% | Weekly (automated) |

---

## 5. Security Metrics

### 5.1 Core Security KPIs

| Metric | Definition | Target | Threshold | Frequency |
| ------ | ---------- | ------ | --------- | --------- |
| **Security Incidents** | Count of security incidents | Trending down | Context-dependent | Monthly |
| **MTTR (Security)** | Mean time to remediate vulnerabilities | <30 days (critical) | Red: >30 days critical | Monthly |
| **Vulnerability Backlog** | Count of open vulnerabilities by severity | 0 critical | Red: Any critical >7 days | Weekly |
| **Phishing Click Rate** | % of users clicking simulated phishing | <5% | Yellow: >5%, Red: >10% | Quarterly |
| **MFA Adoption** | % of accounts with MFA enabled | 100% | Red: <100% | Monthly |

### 5.2 Access Control Metrics

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Access Reviews Completed** | % of scheduled access reviews completed | 100% | Quarterly |
| **Orphaned Accounts** | Accounts without valid owner | 0 | Monthly |
| **Privileged Access Count** | Number of privileged accounts | Minimized | Monthly |
| **Access Removal Timeliness** | % of terminated users removed within SLA | 100% | Monthly |

### 5.3 Incident Metrics

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Incident Response Time** | Time from detection to response | Within SLA | Per incident |
| **Incident Resolution Time** | Time from detection to resolution | Within SLA | Per incident |
| **Post-Mortem Completion** | % of qualifying incidents with post-mortem | 100% | Monthly |
| **Recurring Incidents** | Incidents with same root cause | 0 | Quarterly |

---

## 6. AI Governance Metrics

### 6.1 Core AI KPIs

| Metric | Definition | Target | Threshold | Frequency |
| ------ | ---------- | ------ | --------- | --------- |
| **Model Registry Coverage** | % of production models in registry | 100% | Red: <100% | Monthly |
| **Gate Compliance** | % of AI releases passing all gates | 100% | Red: Any bypass without exception | Per release |
| **AI Incident Rate** | AI-related incidents per model | Trending down | Context-dependent | Monthly |
| **Bias Assessment Coverage** | % of models with current bias assessment | 100% | Yellow: <100% | Quarterly |

### 6.2 Model Health Metrics

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Model Drift Rate** | Models showing performance drift | 0 unaddressed | Weekly |
| **Model Age** | Age of production models | <12 months without review | Monthly |
| **Rollback Events** | Model rollbacks due to issues | Trending down | Monthly |
| **Human Override Rate** | % of AI decisions overridden by humans | Context-dependent | Monthly |

### 6.3 AI Security Metrics

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Prompt Injection Tests** | % of AI systems with current injection testing | 100% | Quarterly |
| **AI Security Incidents** | Security incidents involving AI systems | 0 | Monthly |
| **Output Filtering Triggers** | Count of blocked/filtered outputs | Tracked for trending | Weekly |
| **Jailbreak Attempts** | Detected jailbreak attempts | Tracked for trending | Weekly |

---

## 7. Operational Metrics

### 7.1 Change Management

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Change Success Rate** | % of changes without rollback | >95% | Monthly |
| **Emergency Change Rate** | % of changes using emergency process | <5% | Monthly |
| **Change Documentation** | % of changes with complete documentation | 100% | Per change |
| **Approval Compliance** | % of changes with required approvals | 100% | Per change |

### 7.2 Vendor Management

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Vendor Assessment Currency** | % of vendors with current assessment | 100% | Quarterly |
| **Vendor Incident Rate** | Incidents caused by vendor issues | Trending down | Monthly |
| **Contract Compliance** | % of vendor contracts current | 100% | Monthly |

### 7.3 Business Continuity

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **DR Test Completion** | % of scheduled DR tests completed | 100% | Quarterly |
| **RTO Achievement** | % of systems meeting RTO in tests | 100% | Per test |
| **Backup Success Rate** | % of successful backups | >99.9% | Daily |
| **Recovery Test Success** | % of successful restore tests | 100% | Monthly |

---

## 8. Training Metrics

### 8.1 Training Compliance

| Metric | Definition | Target | Threshold | Frequency |
| ------ | ---------- | ------ | --------- | --------- |
| **Overall Training Compliance** | % of personnel current on required training | 100% | Yellow: <95%, Red: <90% | Monthly |
| **Onboarding Completion** | % of new hires completing training on time | 100% | Red: <100% | Monthly |
| **Overdue Training** | Count of overdue training assignments | 0 | Red: Any >30 days overdue | Weekly |

### 8.2 Training Effectiveness

| Metric | Definition | Target | Frequency |
| ------ | ---------- | ------ | --------- |
| **Assessment Pass Rate** | % passing on first attempt | >90% | Quarterly |
| **Training-Related Incidents** | Incidents with training gap as root cause | 0 | Quarterly |
| **Phishing Improvement** | Trend in phishing simulation results | Improving | Quarterly |

---

## 9. Dashboard Requirements

### 9.1 Executive Dashboard

High-level governance health for leadership:

| Section | Content |
| ------- | ------- |
| **Overall Health** | Red/Yellow/Green status summary |
| **Key Risks** | Top 3-5 governance risks |
| **Compliance Status** | Audit findings, exceptions, training |
| **Trends** | Key metric trends over time |
| **Action Items** | Items requiring leadership attention |

### 9.2 Compliance Dashboard

Detailed compliance metrics:

| Section | Content |
| ------- | ------- |
| **Regulatory Status** | HIPAA, SOC 2, other frameworks |
| **Audit Findings** | Open findings by severity and age |
| **Exceptions** | Active exceptions and expirations |
| **Documentation** | Document review status |
| **Training** | Compliance by department |

### 9.3 Security Dashboard

Security posture overview:

| Section | Content |
| ------- | ------- |
| **Incident Status** | Open incidents, recent trends |
| **Vulnerability Status** | Open vulnerabilities by severity |
| **Access Health** | Access review status, privileged accounts |
| **Threat Activity** | Phishing, attack attempts |
| **Control Health** | Key control status |

### 9.4 AI Governance Dashboard

AI-specific governance health:

| Section | Content |
| ------- | ------- |
| **Model Inventory** | Production models by classification |
| **Gate Compliance** | Recent releases and gate status |
| **Model Health** | Drift, performance, age |
| **AI Security** | AI-specific security metrics |
| **Bias/Fairness** | Assessment status and findings |

---

## 10. Reporting Requirements

### 10.1 Report Types

| Report | Audience | Frequency | Owner |
| ------ | -------- | --------- | ----- |
| **Executive Summary** | Leadership | Monthly | Compliance |
| **Compliance Report** | Compliance committee | Monthly | Compliance |
| **Security Report** | Security committee | Monthly | Security |
| **AI Governance Report** | AI leadership | Monthly | AI Engineering |
| **Audit Status** | Audit committee | Quarterly | Compliance |
| **Board Report** | Board of directors | Quarterly | Executive |

### 10.2 Report Contents

Each governance report MUST include:

| Section | Content |
| ------- | ------- |
| **Period** | Reporting period covered |
| **Summary** | Executive summary of status |
| **Metrics** | Key metrics with trends |
| **Issues** | Open issues requiring attention |
| **Progress** | Progress on previous action items |
| **Recommendations** | Recommended actions |

### 10.3 Report Distribution

- Reports distributed to defined recipients
- Sensitive reports marked appropriately
- Historical reports archived for audit
- Acknowledgment tracking for critical reports

---

## 11. Thresholds and Alerts

### 11.1 Threshold Definitions

| Level | Definition | Action |
| ----- | ---------- | ------ |
| **Green** | Within target, healthy | Continue monitoring |
| **Yellow** | Warning threshold breached | Investigation required |
| **Red** | Critical threshold breached | Immediate action required |

### 11.2 Alert Configuration

| Alert Type | Trigger | Recipients | Escalation |
| ---------- | ------- | ---------- | ---------- |
| **Critical** | Red threshold | Owner + leadership | Immediate |
| **Warning** | Yellow threshold | Owner | Within 24 hours |
| **Trend** | Negative trend detected | Owner | Weekly review |

### 11.3 Alert Response

When alerts trigger:

1. Acknowledge alert within SLA
2. Investigate root cause
3. Implement remediation
4. Update metric/status
5. Document in appropriate system

---

## 12. Data Collection

### 12.1 Data Sources

| Source | Metrics Provided |
| ------ | ---------------- |
| **GitHub** | Change metrics, PR compliance, workflow status |
| **LMS** | Training completion, assessment scores |
| **Ticketing system** | Incidents, findings, exceptions |
| **Access management** | Access reviews, account status |
| **Security tools** | Vulnerabilities, threats, incidents |
| **Model registry** | Model inventory, deployment status |

### 12.2 Data Quality

| Requirement | Description |
| ----------- | ----------- |
| Accuracy | Data accurately reflects actual state |
| Completeness | All required data points collected |
| Timeliness | Data current within defined freshness |
| Consistency | Metrics calculated consistently over time |

### 12.3 Automation

Prefer automated data collection:

- CI/CD integration for change metrics
- API integration for tool data
- Scheduled jobs for aggregation
- Automated dashboard updates

---

## 13. Metric Review Process

### 13.1 Regular Reviews

| Review | Frequency | Participants | Outcomes |
| ------ | --------- | ------------ | -------- |
| **Metric review** | Monthly | Metric owners | Validate accuracy, address issues |
| **Threshold review** | Quarterly | Leadership | Adjust thresholds as needed |
| **Metric relevance** | Annual | All stakeholders | Add/remove/modify metrics |

### 13.2 Metric Lifecycle

| Phase | Activities |
| ----- | ---------- |
| **Propose** | Identify need, define metric, get approval |
| **Implement** | Build data collection, configure dashboard |
| **Operate** | Collect data, report, respond to alerts |
| **Review** | Assess relevance and effectiveness |
| **Retire** | Remove metrics no longer needed |

---

## 14. Continuous Improvement

### 14.1 Improvement Sources

Use metrics to drive improvement:

- Negative trends indicate process issues
- Recurring threshold breaches indicate systemic problems
- Audit findings indicate control gaps
- Incident root causes indicate training/process needs

### 14.2 Improvement Process

1. Identify issue through metrics
2. Analyze root cause
3. Propose improvement
4. Implement through change control
5. Measure impact through metrics

---

## 15. Exceptions

Exceptions to metric reporting:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include alternative visibility mechanism
- MUST be time-bounded
- MUST be approved by Compliance leadership

Temporary metric collection issues should be documented and resolved promptly.

---

## 16. Enforcement

Metric and reporting requirements are enforced through:

- Automated collection where possible
- Dashboard visibility to leadership
- Report distribution tracking
- Escalation for missing/late reports

**Operating without governance visibility is a governance violation.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
