# 1520ai — Incident Response & Learning

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** Organization-wide
**Audience:** All teams, on-call engineers, leadership, auditors

---

## 1. Purpose

This document defines how 1520ai identifies, escalates, responds to, and learns from incidents.

Incidents are treated as system signals, not individual failures. The goal is not blame but systematic improvement.

**Every incident is an opportunity to strengthen governance, controls, and system resilience.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [SECURITY.md](../SECURITY.md) — Security incident reporting and escalation
- [docs/change-control.md](change-control.md) — Change and exception mechanics

Security incidents follow the escalation path defined in SECURITY.md. This document extends that framework to include all incident types and formalizes the learning process.

---

## 3. What Constitutes an Incident

An incident is any event that:

- Causes or risks unauthorized PHI exposure
- Results in system unavailability affecting users
- Causes AI systems to produce incorrect or harmful outputs
- Bypasses or circumvents governance controls
- Violates regulatory or compliance requirements
- Results in data loss or corruption
- Indicates security compromise or attempted breach

### 3.1 Incident vs. Bug vs. Issue

| Type | Definition | Response |
| ---- | ---------- | -------- |
| **Incident** | Event with actual or potential harm, compliance impact, or governance violation | Immediate escalation, formal response |
| **Bug** | Software defect without immediate harm | Standard development process |
| **Issue** | Improvement opportunity or minor concern | Normal triage and prioritization |

**When in doubt, treat it as an incident.** Downgrading is safer than missing escalation.

---

## 4. Incident Severity Levels

| Severity | Definition | Response Time | Escalation |
| -------- | ---------- | ------------- | ---------- |
| **Critical** | Active PHI exposure, security breach, or regulatory violation in progress | Immediate | Leadership within 1 hour |
| **High** | Significant risk of harm, system-wide outage, or governance bypass discovered | Within 1 hour | Leadership within 4 hours |
| **Medium** | Limited impact, contained issue, or near-miss event | Within 4 hours | Team lead within 1 business day |
| **Low** | Minor issue, no immediate harm, learning opportunity | Within 1 business day | Standard review process |

Severity may be upgraded during investigation as impact becomes clearer.

---

## 5. Incident Response Process

### Phase 1: Detection & Triage

**Objective:** Identify the incident and assess initial severity.

Actions:

1. Document initial observation (what was noticed, when, by whom)
2. Assess initial severity using criteria above
3. Notify appropriate responders based on severity
4. Create incident ticket in tracking system

**Timeline:** Within 15 minutes of detection for Critical/High severity.

### Phase 2: Containment

**Objective:** Stop ongoing harm and prevent spread.

Actions:

1. Isolate affected systems if necessary
2. Revoke compromised credentials or access
3. Preserve evidence (logs, artifacts) before remediation
4. Communicate status to affected stakeholders

**Timeline:** Containment actions should begin within 30 minutes for Critical severity.

### Phase 3: Investigation

**Objective:** Understand root cause and full impact.

Actions:

1. Gather timeline of events
2. Identify root cause(s) — technical, process, and human factors
3. Assess full scope of impact (data, users, systems affected)
4. Document findings in incident record

**Timeline:** Initial findings within 24 hours for Critical/High severity.

### Phase 4: Remediation

**Objective:** Fix the immediate issue and restore normal operations.

Actions:

1. Implement technical fix or workaround
2. Verify fix effectiveness
3. Restore normal operations
4. Confirm with stakeholders

**Timeline:** Varies by incident complexity.

### Phase 5: Post-Incident Review

**Objective:** Learn from the incident and improve systems.

Actions:

1. Conduct blameless post-mortem (see Section 7)
2. Identify corrective actions
3. Update governance artifacts if needed
4. Close incident with documented learnings

**Timeline:** Post-mortem within 5 business days of resolution for Critical/High severity.

---

## 6. Escalation Paths

### 6.1 Standard Escalation

| Severity | Initial Responder | Escalation Path |
| -------- | ----------------- | --------------- |
| Critical | On-call engineer | → Engineering Lead → VP Engineering → Executive |
| High | On-call engineer | → Engineering Lead → VP Engineering |
| Medium | Team member | → Team Lead → Engineering Lead |
| Low | Team member | → Team Lead |

### 6.2 Cross-Functional Escalation

Incidents affecting multiple domains require joint escalation:

| Domain Affected | Additional Escalation |
| --------------- | --------------------- |
| PHI / Patient data | → Compliance Lead, Privacy Officer |
| AI behavior / Model output | → AI Engineering Lead, Responsible AI Lead |
| Security / Access control | → Security Lead |
| Regulatory compliance | → Compliance Lead, Legal (if needed) |

### 6.3 External Escalation

Some incidents require external notification:

- **PHI breach:** Assess HIPAA breach notification requirements
- **Security breach:** Consider law enforcement notification
- **Regulatory violation:** Notify compliance for regulatory reporting assessment

**External escalation decisions are made by leadership, not individual responders.**

---

## 7. Post-Incident Review (Blameless Post-Mortem)

### 7.1 Purpose

Post-incident reviews identify systemic improvements, not individual blame.

The goal is to answer:

- What happened?
- Why did it happen?
- How do we prevent recurrence?
- What governance improvements are needed?

### 7.2 Required for All High/Critical Incidents

Post-incident reviews are MANDATORY for:

- All Critical severity incidents
- All High severity incidents
- Any incident involving PHI
- Any incident involving governance bypass

Reviews are RECOMMENDED for Medium severity incidents and encouraged for all incidents.

### 7.3 Post-Mortem Document Structure

Every post-mortem MUST include:

```text
Incident ID:
Date of Incident:
Date of Review:
Severity:
Participants:

1. Summary
   - One paragraph description of what happened

2. Timeline
   - Chronological sequence of events with timestamps

3. Impact
   - Users/systems affected
   - Data impact (if any)
   - Duration of impact

4. Root Cause Analysis
   - Technical root cause
   - Process factors
   - Human factors (without blame)

5. What Went Well
   - Effective responses
   - Controls that worked

6. What Could Be Improved
   - Detection gaps
   - Response delays
   - Communication issues

7. Corrective Actions
   - Action item, owner, due date, status

8. Governance Implications
   - Does this incident indicate a governance gap?
   - Are policy updates needed?
   - Should this trigger an exception review?

9. Lessons Learned
   - Key takeaways for the organization
```

### 7.4 Corrective Action Tracking

Corrective actions identified in post-mortems:

- MUST be assigned an owner
- MUST have a due date
- MUST be tracked to completion
- SHOULD be linked to the incident record

Overdue corrective actions are escalated to leadership.

---

## 8. Incident Registry

### 8.1 Purpose

1520ai maintains an incident registry to:

- Track all incidents and their resolution
- Enable pattern analysis across incidents
- Support audit and compliance requirements
- Drive governance improvements

### 8.2 Registry Requirements

All incidents MUST be logged with:

| Field | Description |
| ----- | ----------- |
| Incident ID | Unique identifier |
| Date/Time | When the incident occurred |
| Severity | Critical / High / Medium / Low |
| Category | Security / Data / AI Behavior / Availability / Governance |
| Summary | Brief description |
| Impact | Scope of impact |
| Root Cause | Primary cause identified |
| Resolution | How it was resolved |
| Post-Mortem Link | Link to post-mortem document (if applicable) |
| Corrective Actions | List of actions with status |
| Governance Impact | Any governance changes triggered |

### 8.3 Retention

Incident records MUST be retained for:

- Minimum 6 years for PHI-related incidents (HIPAA requirement)
- Minimum 3 years for all other incidents
- Indefinitely for incidents triggering governance changes

---

## 9. Governance Feedback Loop

Incidents inform governance improvements through a formal feedback loop.

### 9.1 Triggers for Governance Review

The following incident outcomes MUST trigger governance review:

- Incident caused by governance gap or ambiguity
- Incident caused by exception that should not have been granted
- Incident revealed control that was insufficient
- Pattern of similar incidents (3+ in 90 days)
- Incident required emergency governance change

### 9.2 Governance Update Process

When an incident triggers governance review:

1. Document the governance implication in post-mortem
2. Open a governance change proposal per [change-control.md](change-control.md)
3. Reference the incident in the change rationale
4. Track the governance change as a corrective action

### 9.3 Exception Review

Incidents may trigger review of existing exceptions:

- If an incident was enabled by an active exception, review the exception
- If the exception's risk assessment was inaccurate, update or revoke
- If the exception has expired but behavior persisted, investigate

---

## 10. Metrics & Reporting

### 10.1 Incident Metrics

The following metrics SHOULD be tracked quarterly:

| Metric | Description | Target |
| ------ | ----------- | ------ |
| Mean Time to Detect (MTTD) | Time from incident start to detection | Minimize |
| Mean Time to Contain (MTTC) | Time from detection to containment | < 1 hour for Critical |
| Mean Time to Resolve (MTTR) | Time from detection to resolution | Varies by severity |
| Post-Mortem Completion Rate | % of required post-mortems completed | 100% |
| Corrective Action Completion | % of actions completed by due date | > 90% |
| Repeat Incident Rate | % of incidents with same root cause | < 10% |

### 10.2 Reporting

Incident metrics are reported to:

- Engineering leadership: Monthly
- Executive leadership: Quarterly
- Audit/Compliance: As required

---

## 11. Training & Preparedness

### 11.1 Incident Response Training

All engineers SHOULD receive incident response training covering:

- Incident identification and severity assessment
- Escalation procedures
- Evidence preservation
- Communication protocols

### 11.2 Incident Drills

Critical systems SHOULD conduct incident response drills:

- Quarterly tabletop exercises
- Annual simulated incident response
- Post-drill review and improvement

---

## 12. Enforcement

Incident response requirements are enforced through:

- On-call responsibilities and escalation expectations
- Post-mortem completion requirements
- Corrective action tracking
- Audit review of incident handling

**Failure to report or escalate incidents appropriately is a governance violation.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
