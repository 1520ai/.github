# 1520ai — Data Lineage & Provenance

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** All data pipelines and AI systems
**Audience:** Data engineering, AI/ML teams, compliance, auditors

---

## 1. Purpose

This document defines requirements for tracking data lineage and provenance across 1520ai systems.

Data lineage ensures that:

- Data sources are documented and traceable
- Transformations are logged and reproducible
- Training datasets are versioned and attributable
- Audit questions ("where did this data come from?") are answerable
- Data quality issues can be traced to their source

**Systems processing PHI or training AI models MUST maintain data lineage documentation.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/data-protection.md](data-protection.md) — Data handling and PHI requirements
- [docs/model-registry.md](model-registry.md) — Model tracking and governance
- [docs/responsible-ai.md](responsible-ai.md) — AI posture and constraints

Data lineage is a prerequisite for audit defensibility and regulatory compliance.

---

## 3. Definitions

| Term | Definition |
| ---- | ---------- |
| **Data Lineage** | The complete lifecycle of data from origin to consumption |
| **Provenance** | The origin and history of a specific data element |
| **Data Source** | The original system or process that created the data |
| **Transformation** | Any operation that modifies, filters, or derives new data |
| **Dataset** | A versioned collection of data used for a specific purpose |
| **Data Consumer** | A system, model, or process that uses the data |

---

## 4. Lineage Requirements

### 4.1 What Requires Lineage Documentation

Data lineage MUST be documented for:

- All PHI data flows
- All training datasets used for AI models
- All data pipelines producing outputs for regulatory or compliance purposes
- All data transformations affecting audit-relevant records
- All data exports to external systems or third parties

Data lineage SHOULD be documented for:

- Internal analytics and reporting pipelines
- Development and testing data flows
- Operational metrics and monitoring data

### 4.2 Lineage Granularity

Lineage documentation granularity depends on data sensitivity:

| Data Type | Required Granularity |
| --------- | -------------------- |
| PHI | Field-level lineage for sensitive fields |
| Training Data | Dataset-level with sampling methodology |
| Regulatory Outputs | Record-level traceability |
| Operational Data | Pipeline-level documentation |

---

## 5. Data Source Documentation

### 5.1 Required Source Information

Every data source MUST be documented with:

| Field | Description | Example |
| ----- | ----------- | ------- |
| Source ID | Unique identifier | `ehr-system-prod` |
| Source Name | Human-readable name | Hospital EHR System |
| Source Type | Category of source | Database / API / File / Stream |
| Owner | Team or system responsible | Clinical Systems Team |
| Data Classification | Per data-protection.md | Sensitive / Regulated |
| PHI Indicator | Whether source contains PHI | Yes / No / Possible |
| Access Method | How data is retrieved | Direct query / API / Export |
| Refresh Frequency | How often data is updated | Real-time / Daily / Weekly |
| Documentation Link | Link to source documentation | |

### 5.2 Source Registry Template

```text
## [Source ID]

### Overview

| Field | Value |
| ----- | ----- |
| Source Name | |
| Source Type | |
| Owner | |
| Data Classification | |
| PHI Indicator | |

### Access

| Field | Value |
| ----- | ----- |
| Access Method | |
| Refresh Frequency | |
| Access Controls | |
| Credentials Location | |

### Schema

| Field | Type | PHI | Description |
| ----- | ---- | --- | ----------- |
| | | | |

### Consumers

| Consumer | Purpose | Access Granted |
| -------- | ------- | -------------- |
| | | |

### Notes

<!-- Additional context, known issues, or operational notes -->
```

---

## 6. Transformation Documentation

### 6.1 Required Transformation Information

Every data transformation MUST be documented with:

| Field | Description |
| ----- | ----------- |
| Transformation ID | Unique identifier |
| Input Sources | Data sources consumed |
| Output Destination | Where transformed data goes |
| Transformation Type | Filter / Aggregate / Join / Derive / Anonymize |
| Logic Description | What the transformation does |
| Code Reference | Link to transformation code |
| Owner | Team responsible |
| PHI Handling | How PHI is handled (if applicable) |

### 6.2 Transformation Types

| Type | Definition | Lineage Requirement |
| ---- | ---------- | ------------------- |
| **Filter** | Removes records based on criteria | Document filter criteria |
| **Aggregate** | Combines records into summaries | Document aggregation logic |
| **Join** | Combines data from multiple sources | Document join keys and logic |
| **Derive** | Creates new fields from existing data | Document derivation formula |
| **Anonymize** | Removes or masks identifying information | Document anonymization method |
| **Enrich** | Adds data from external sources | Document enrichment source |

### 6.3 Transformation Chain

For complex pipelines, document the transformation chain:

```text
[Source A] → [Transform 1] → [Intermediate Dataset] → [Transform 2] → [Output]
     ↓
[Source B] ────────────────────────┘
```

Each node in the chain MUST have corresponding documentation.

---

## 7. Training Dataset Registry

### 7.1 Purpose

AI models require explicit documentation of training data to:

- Enable reproducibility of model training
- Support bias assessment and fairness analysis
- Provide audit evidence for model decisions
- Enable data issue investigation when model problems arise

### 7.2 Required Dataset Information

Every training dataset MUST be documented with:

| Field | Description |
| ----- | ----------- |
| Dataset ID | Unique identifier |
| Dataset Name | Human-readable name |
| Version | Dataset version |
| Creation Date | When dataset was created |
| Creator | Who created the dataset |
| Purpose | What the dataset is used for |
| Source Lineage | Data sources used to create dataset |
| Size | Number of records / size in storage |
| Time Range | Temporal coverage of data |
| Sampling Method | How data was sampled (if applicable) |
| PHI Status | Contains PHI / De-identified / Synthetic |
| Storage Location | Where dataset is stored |
| Retention Policy | How long dataset is retained |

### 7.3 Dataset-Model Mapping

Every model in the [model registry](model-registry.md) that is trained (not rule-based) MUST reference its training dataset(s):

| Model ID | Training Dataset(s) | Training Date | Notes |
| -------- | ------------------- | ------------- | ----- |
| | | | |

### 7.4 Dataset Version Control

Training datasets MUST be versioned:

- New versions created for any data changes
- Previous versions retained per retention policy
- Version history documented
- Model retraining linked to dataset versions

---

## 8. PHI Lineage Requirements

### 8.1 Enhanced Requirements for PHI

Data flows involving PHI have additional lineage requirements:

| Requirement | Description |
| ----------- | ----------- |
| Field-Level Tracking | Document which fields contain PHI |
| Access Logging | Log all access to PHI data |
| Transformation Audit | Document all transformations applied to PHI |
| De-identification Proof | Document de-identification method and validation |
| Minimum Necessary | Document why each PHI field is required |

### 8.2 PHI Flow Documentation

PHI data flows MUST include:

```text
## PHI Data Flow: [Flow Name]

### Source
- System: [Source system]
- PHI Fields: [List of PHI fields]
- Access Control: [Who can access]

### Transformations
1. [Transformation 1]
   - PHI Handling: [How PHI is handled]
   - Output PHI Fields: [Resulting PHI fields]

### Destination
- System: [Destination system]
- PHI Fields Retained: [List]
- Access Control: [Who can access]

### Justification
- Business Need: [Why this flow exists]
- Minimum Necessary: [Why each field is needed]
```

---

## 9. Lineage Metadata Storage

### 9.1 Documentation Location

Lineage documentation SHOULD be stored in:

- `docs/data-sources/` — Data source documentation
- `docs/datasets/` — Training dataset documentation
- `docs/pipelines/` — Transformation pipeline documentation

### 9.2 Automated Lineage

Where feasible, lineage SHOULD be captured automatically through:

- Pipeline orchestration tools (e.g., Airflow, Prefect)
- Data catalog systems
- Version control for data artifacts
- Transformation logging

Automated lineage supplements but does not replace documentation requirements.

---

## 10. Audit & Compliance

### 10.1 Audit Questions

Data lineage documentation MUST enable answering:

| Question | Answered By |
| -------- | ----------- |
| Where did this data come from? | Source documentation |
| What transformations were applied? | Transformation documentation |
| Who has access to this data? | Access control documentation |
| What models were trained on this data? | Dataset-model mapping |
| When was this data last updated? | Refresh frequency / version history |
| Is this data de-identified? | PHI status / de-identification proof |

### 10.2 Retention

Lineage documentation MUST be retained:

- For the lifetime of the data plus retention period
- Minimum 6 years for PHI-related lineage
- Minimum 3 years for training dataset documentation
- Indefinitely for active production pipelines

### 10.3 Review Cadence

Lineage documentation SHOULD be reviewed:

- Quarterly for active pipelines
- Upon data source changes
- Upon pipeline modifications
- During audit preparation

---

## 11. Data Quality Integration

### 11.1 Quality Checkpoints

Lineage documentation SHOULD include data quality checkpoints:

| Checkpoint | Description |
| ---------- | ----------- |
| Source Validation | Checks applied at data ingestion |
| Transformation Validation | Checks applied during transformation |
| Output Validation | Checks applied before data consumption |

### 11.2 Quality Issue Tracing

When data quality issues are discovered:

1. Use lineage to trace issue to source
2. Document root cause in lineage documentation
3. Update quality checkpoints to prevent recurrence
4. Link to incident record if applicable

---

## 12. Enforcement

Data lineage requirements are enforced through:

- Code review (lineage documentation required for data pipelines)
- Model registry validation (training data reference required)
- Audit and compliance review
- Incident investigation

**Deploying data pipelines or models without lineage documentation is a governance violation for PHI and AI training contexts.**

---

## 13. Exceptions

Exceptions to lineage requirements:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include risk assessment
- MUST be time-bounded
- MUST be approved by Data Engineering or AI Engineering leadership

Development and experimentation environments MAY have reduced lineage requirements but MUST comply fully before production deployment.

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
