# 1520ai — AI Model Registry

**Status:** Active
**Effective Date:** 2026-01-15
**Last Reviewed:** 2026-08-02
**Scope:** All AI-enabled systems
**Audience:** AI/ML teams, engineering, compliance, auditors

---

## 1. Purpose

This document defines the requirements for tracking AI models deployed across 1520ai systems.

The model registry ensures that:

- All production models are documented and discoverable
- Governance status is explicit and traceable
- Sensitivity classification drives appropriate controls
- Approval history supports audit reconstruction
- Drift and incidents are linked to specific model versions

**No AI model may operate in production without a registry entry.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/responsible-ai.md](responsible-ai.md) — Sensitivity × Consensus framework
- [docs/ai-release-gates.md](ai-release-gates.md) — Pre-deployment validation requirements
- [docs/change-control.md](change-control.md) — Change and exception mechanics

Model registry entries are governance artifacts subject to change control.

---

## 3. Registry Requirements

### 3.1 What Must Be Registered

All models meeting any of the following criteria MUST be registered:

- Deployed to production environments
- Processing PHI or sensitive data
- Producing outputs consumed by users or downstream systems
- Making or influencing decisions subject to regulatory requirements
- Operating in high-sensitivity domains per [responsible-ai.md](responsible-ai.md)

### 3.2 When to Register

Models MUST be registered:

- Before production deployment (as part of release gates)
- Upon significant version changes
- When sensitivity classification changes
- When ownership or authority changes

### 3.3 Registry Location

Product repositories SHOULD maintain their model registries in:

- `docs/model-registry.md` (for product-specific models)

This organization-level document defines the schema and requirements. Product repositories implement the actual registries.

---

## 4. Registry Schema

Each model entry MUST include the following fields:

### 4.1 Required Fields

The examples below use a generic placeholder model, not any specific product's
model — product registries fill these with their own entries.

| Field | Description | Example |
| ----- | ----------- | ------- |
| Model ID | Unique identifier | `<product>-deid-ner-v1` |
| Model Name | Human-readable name | Document De-identification NER |
| Version | Current production version | `1.4.0` |
| Purpose | What the model does | Detects and redacts PHI identifiers in free-text fields |
| Decision Role | Enforcing / Advisory / Auxiliary — see §4.4 | Auxiliary |
| Sensitivity | Per responsible-ai.md matrix | High |
| Consensus | Per responsible-ai.md matrix | High |
| Classification | Matrix outcome | Handle With Care |
| Owner | Team or individual responsible | Platform Engineering |
| Approver | Who approved production deployment | Security Lead |
| Approval Date | When deployment was approved | YYYY-MM-DD |
| Status | Current operational status | Active / Deprecated / Suspended |

### 4.2 Conditional Fields

| Field | When Required | Description |
| ----- | ------------- | ----------- |
| PHI Access | If model processes PHI | Yes / No / Indirect |
| Human Review Gate | If High Sensitivity | Required review touchpoint |
| Drift Monitoring | If in production | Link to monitoring config |
| Bias Assessment | If applicable | Link to assessment report |
| Training Data Reference | If model is trained | Link to data lineage |
| Rollback Version | If not first version | Previous stable version |

### 4.3 Optional Fields

| Field | Description |
| ----- | ----------- |
| Model Architecture | Technical description (e.g., transformer, ensemble) |
| Framework | Implementation framework (e.g., PyTorch, TensorFlow) |
| Inference Latency | Expected response time |
| Resource Requirements | Compute/memory requirements |
| Dependencies | External services or models |
| Expiration | If model has planned deprecation |

### 4.4 Decision Role and Model Independence

Every registered model MUST declare its **Decision Role**, and the registry MUST
record whether the product's binding regulatory or safety decision depends on it:

| Decision Role | Definition | Registry obligation |
| ------------- | ---------- | ------------------- |
| **Enforcing** | The model's output determines or gates a binding regulatory/safety outcome | Prohibited unless a deterministic control sits between the model and the outcome. Per [governance.md](governance.md), probabilistic models MUST NOT autonomously enforce decisions. |
| **Advisory** | The model's output is presented to a human or a downstream report, but a human or deterministic layer owns the decision | Record the **Decision Dependence**: does the binding output change if this model changes? Prefer *No* (model-independent) by construction. |
| **Auxiliary** | The model supports internal tooling (de-identification, monitoring, extraction, summarization) and is not in any decision path | Record data access and PHI handling; no decision-dependence claim needed. |

**Model independence is the target state for anything near a regulated decision.**
Where a product's binding output (a categorical status, a hard stop, an eligibility
determination) is computed by deterministic logic and a model only produces advisory
or auxiliary output, the decision is **model-independent by construction** — a model
version change cannot alter the regulated outcome. Registries SHOULD state this
explicitly for enforcement-adjacent models so a swap can be validated structurally
rather than by experiment. *(Flagship reference: the categorical DEH decision is
computed from deterministic gates and is independent of the generative model, which is
advisory only — see the product's ADR-074.)*

---

## 5. Registry Entry Template

```text
## [Model ID]

### Overview

| Field | Value |
| ----- | ----- |
| Model Name | |
| Version | |
| Purpose | |
| Status | Active / Deprecated / Suspended |

### Classification

| Field | Value |
| ----- | ----- |
| Sensitivity | Low / High |
| Consensus | Low / High |
| Classification | Standardize / Explore / Handle With Care / Avoid |
| PHI Access | Yes / No / Indirect |
| Decision Role | Enforcing / Advisory / Auxiliary |
| Decision Dependence | Does the binding output change if this model changes? Yes / No (model-independent) / N/A |

### Governance

| Field | Value |
| ----- | ----- |
| Owner | |
| Approver | |
| Approval Date | |
| Approval PR | |

### Gates Completed

| Gate | Status | Date | Reviewer |
| ---- | ------ | ---- | -------- |
| Determinism | Pass / Waived | | |
| Explainability | Pass / Waived | | |
| Drift Monitoring | Pass / Waived | | |
| Bias Assessment | Pass / Waived / N/A | | |
| Rollback Procedure | Pass / Waived | | |
| Human-in-the-Loop | Pass / Waived / N/A | | |

### References

| Reference | Link |
| --------- | ---- |
| Training Data | |
| Drift Monitoring | |
| Bias Assessment | |
| Rollback Procedure | |

### History

| Version | Date | Change | Approver |
| ------- | ---- | ------ | -------- |
| | | Initial deployment | |

### Notes

<!-- Any additional context, known limitations, or operational notes -->
```

---

## 6. Classification Guidelines

Models are classified using the Sensitivity × Consensus matrix from [responsible-ai.md](responsible-ai.md):

### 6.1 Sensitivity Assessment

**High Sensitivity** indicators:

- Processes or influences PHI handling
- Outputs affect clinical, legal, or regulatory decisions
- Errors could cause patient harm or regulatory violation
- Outputs are presented to end users as authoritative
- Model operates in life-safety or high-stakes domains

**Low Sensitivity** indicators:

- Internal tooling with no external impact
- Outputs are advisory with explicit human review
- Errors have minimal operational impact
- No PHI or sensitive data involvement

### 6.2 Consensus Assessment

**High Consensus** indicators:

- Clear regulatory guidance exists
- Industry best practices are established
- Stakeholder expectations are aligned
- Similar systems are widely deployed

**Low Consensus** indicators:

- Regulatory interpretation is uncertain
- Industry norms are still forming
- Stakeholder expectations vary
- Novel application with limited precedent

### 6.3 Classification Outcomes

| Sensitivity | Consensus | Classification | Implications |
| ----------- | --------- | -------------- | ------------ |
| Low | High | Standardize | Standard gates, routine monitoring |
| Low | Low | Explore | Enhanced documentation, careful rollout |
| High | High | Handle With Care | All gates required, heightened monitoring |
| High | Low | Avoid or Redesign | Executive review required, consider alternatives |

---

## 7. Lifecycle Management

### 7.1 Model States

| Status | Definition | Requirements |
| ------ | ---------- | ------------ |
| **Draft** | Under development, not deployed | No registry entry required |
| **Staging** | Deployed to non-production | Registry entry recommended |
| **Active** | Deployed to production | Registry entry required |
| **Deprecated** | Scheduled for removal | Deprecation date documented |
| **Suspended** | Temporarily disabled | Incident reference required |
| **Retired** | Removed from production | Retirement date documented |

### 7.2 Version Changes

When updating a model version:

1. Update registry entry with new version
2. Document change rationale
3. Re-validate applicable gates
4. Update approval date and approver
5. Preserve version history

### 7.3 Deprecation

When deprecating a model:

1. Set status to Deprecated
2. Document deprecation date
3. Identify replacement (if applicable)
4. Communicate to stakeholders
5. Plan removal timeline

### 7.4 Suspension

Models may be suspended when:

- Security incident involving the model
- Unexpected behavior detected
- Regulatory concern raised
- Drift exceeds acceptable thresholds

Suspension:

- MUST reference the triggering incident
- MUST be communicated to stakeholders
- Requires remediation before reinstatement
- Follows incident response process per [incident-response.md](incident-response.md)

---

## 8. Audit & Compliance

### 8.1 Audit Trail

The model registry provides audit evidence for:

- What models are deployed
- Who approved each deployment
- When approvals occurred
- What gates were completed
- How models are classified

### 8.2 Retention

Registry entries MUST be retained:

- Active models: Current entry maintained
- Deprecated models: Entry retained for 1 year after retirement
- PHI-processing models: Entry retained for minimum 6 years

### 8.3 Review Cadence

Model registry entries SHOULD be reviewed:

- Quarterly for Active models
- Upon any incident involving the model
- Upon regulatory or governance changes
- Upon significant model updates

---

## 9. Enforcement

Registry requirements are enforced through:

- Release gate validation (Gate 0: Registry entry exists)
- PR review requirements
- Audit and compliance review
- Incident investigation

**Deploying a model without a registry entry is a governance violation.**

---

## 10. Exceptions

Exceptions to registry requirements:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include risk assessment
- MUST be time-bounded
- MUST be approved by AI Engineering leadership

Experimental or research models in isolated environments MAY be exempt from full registry requirements but MUST be registered before any production deployment.

---

## 11. Organization Registry

The following section tracks organization-wide models that are not product-specific.

> **Note:** Product repositories maintain their own model registries following this schema. This section is reserved for shared or organization-level models.

### Active Models

*No organization-level models currently registered.*

### Deprecated Models

*No deprecated models.*

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
