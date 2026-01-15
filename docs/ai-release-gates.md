# 1520ai — AI Release Gates

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** All AI-enabled systems
**Audience:** Engineering, AI/ML teams, product owners, reviewers

---

## 1. Purpose

This document defines mandatory validation gates that AI systems MUST pass before production deployment.

Release gates ensure that AI systems are:

- Deterministic and reproducible
- Explainable to relevant reviewers
- Monitored for drift and degradation
- Assessed for bias and fairness
- Recoverable via documented rollback procedures

**No AI system may be deployed to production without passing all applicable gates.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/responsible-ai.md](responsible-ai.md) — Sensitivity × Consensus framework
- [docs/change-control.md](change-control.md) — Change and exception mechanics

Release gate failures are treated as release blockers, not advisories.

---

## 3. Gate Applicability

Gates apply based on the system's classification per the Sensitivity × Consensus matrix defined in [responsible-ai.md](responsible-ai.md).

| Classification | Required Gates |
| -------------- | -------------- |
| Low Sensitivity / High Consensus | Gates 1, 3, 5 |
| Low Sensitivity / Low Consensus | Gates 1, 3, 4, 5 |
| High Sensitivity / High Consensus | All Gates (1-6) |
| High Sensitivity / Low Consensus | All Gates + Executive Review |

Systems processing PHI MUST pass all gates regardless of classification.

---

## 4. Release Gates

### Gate 1: Determinism Validation

**Requirement:** Identical inputs MUST produce identical outputs.

**Validation Criteria:**

- Fixed random seeds for all stochastic components
- No time-dependent behavior in decision paths
- No unbounded concurrency affecting output order
- External API calls return consistent results or are mocked

**Evidence Required:**

- Test suite demonstrating deterministic behavior
- Documentation of any controlled randomness (seeds recorded)
- CI job showing repeated runs produce identical outputs

**Reviewer:** Engineering lead or designated technical reviewer

---

### Gate 2: Explainability Review

**Requirement:** AI outputs MUST be interpretable by a reasonable human reviewer in context.

**Validation Criteria:**

- Outputs include traceable rationale or evidence references
- Confidence levels are communicated without implying authority
- Limitations and uncertainty are clearly stated
- No outputs imply clinical, regulatory, or legal judgment

**Evidence Required:**

- Sample outputs reviewed by appropriate domain expert
- Documentation of explanation format and content
- User-facing documentation describing output interpretation

**Reviewer:** Domain expert per decision class:

- Clinical interpretation → Clinician
- Regulatory defensibility → Compliance professional
- System behavior → Technical reviewer

---

### Gate 3: Drift Monitoring Setup

**Requirement:** Production systems MUST have monitoring configured before deployment.

**Validation Criteria:**

- Input distribution monitoring enabled
- Output distribution monitoring enabled
- Alerting thresholds defined and documented
- Escalation path configured for drift alerts

**Evidence Required:**

- Monitoring configuration committed to repository
- Alert routing verified (test alert received by on-call)
- Runbook for drift response documented

**Reviewer:** Operations or SRE lead

---

### Gate 4: Bias Assessment

**Requirement:** Systems MUST be evaluated for potential bias across relevant demographic dimensions.

**Validation Criteria:**

- Evaluation dataset includes representative demographic distribution
- Output quality measured across demographic groups
- Disparities documented with mitigation plan if applicable
- Assessment repeated for significant model changes

**Evidence Required:**

- Bias evaluation report with methodology
- Disparity metrics and thresholds
- Mitigation plan (if disparities exceed thresholds)

**Reviewer:** Responsible AI lead or designated reviewer

**Applicability:** Required for systems where outputs may differentially affect individuals or groups. May be waived with documented justification for purely operational systems.

---

### Gate 5: Rollback Procedure

**Requirement:** Every deployment MUST have a documented, tested rollback procedure.

**Validation Criteria:**

- Rollback can be executed within defined SLA
- Previous version artifacts are preserved and accessible
- Rollback procedure tested in staging environment
- Data migration considerations documented (if applicable)

**Evidence Required:**

- Rollback runbook in operations documentation
- Staging rollback test results
- Artifact retention policy compliance

**Reviewer:** Operations or deployment lead

---

### Gate 6: Human-in-the-Loop Verification

**Requirement:** High-sensitivity systems MUST demonstrate human review integration.

**Validation Criteria:**

- Human review touchpoints identified and documented
- System cannot bypass human review for defined decision classes
- Escalation paths tested and functional
- Audit trail captures human review decisions

**Evidence Required:**

- Workflow documentation showing human review gates
- Test results demonstrating review cannot be bypassed
- Sample audit trail entries

**Reviewer:** Product owner and compliance lead (joint)

---

## 5. Gate Review Process

### 5.1 Scheduling

Gate reviews SHOULD be scheduled during development, not at release time.

Recommended timing:

- Gate 1 (Determinism): During development, before integration testing
- Gate 2 (Explainability): During design, validated before release
- Gate 3 (Monitoring): Before staging deployment
- Gate 4 (Bias): After model training, before production
- Gate 5 (Rollback): Before any deployment
- Gate 6 (Human-in-the-loop): During design, validated before release

### 5.2 Documentation

Gate reviews MUST be documented in the release artifact (PR, release notes, or deployment ticket).

Required documentation:

| Field | Description |
| ----- | ----------- |
| Gate | Which gate was reviewed |
| Reviewer | Who conducted the review |
| Date | When the review occurred |
| Outcome | Pass / Fail / Waived (with exception reference) |
| Evidence | Link to supporting artifacts |

### 5.3 Failures

Gate failures block release until resolved.

Resolution options:

1. **Remediate** — Fix the issue and re-review
2. **Exception** — Document exception per [change-control.md](change-control.md) (time-bounded)
3. **Redesign** — Modify system design to address fundamental issues

**Gate failures are not negotiable. Exceptions require formal approval and are time-bounded.**

---

## 6. Emergency Releases

Emergency releases may proceed with abbreviated gate review when delay would materially increase risk.

Emergency releases:

- MUST still document which gates were abbreviated
- MUST undergo full gate review within 5 business days post-deployment
- MUST be logged in incident tracking
- MUST be reported to governance leadership

**Emergency release is not a bypass mechanism. It is a deferred review with accountability.**

---

## 7. Continuous Validation

Gate compliance is not one-time. Systems MUST maintain compliance throughout their lifecycle.

Ongoing requirements:

- Determinism validated on each release
- Monitoring reviewed quarterly
- Bias assessment repeated for significant model changes
- Rollback procedures tested quarterly

Non-compliance discovered post-release triggers incident response per [incident-response.md](incident-response.md).

---

## 8. Enforcement

Release gates are enforced through:

- PR review requirements (CODEOWNERS)
- CI/CD pipeline gates (where automated)
- Release approval checklists
- Audit and incident review

**Deploying without required gate approval is a governance violation.**

---

## 9. Exceptions

Exceptions to release gates:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include risk assessment and mitigations
- MUST be time-bounded with expiration date
- MUST be approved by appropriate authority per decision class

Permanent exceptions are not permitted. Recurring exceptions indicate a need for process or system redesign.

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
