# 1520ai — Governance & Standards Changelog

This changelog records material changes to organization-level governance, security, compliance, and Responsible AI standards.

It is designed to support:

- Audit reconstruction
- Authority verification
- Historical traceability

This changelog does not track product feature changes or code-level releases.

For the full change process, see [docs/change-control.md](docs/change-control.md).

---

## Changelog Conventions

Each entry documents:

- What changed
- Why it changed
- Who approved it
- What impact it has

All entries correspond to an approved pull request under the change-control process.

Entries should be written in past tense (e.g., "Defined..." not "Define...").

---

## [Unreleased]

### Notes

- Reserved for approved changes not yet merged
- Entries must move to a dated section before merge
- This section may contain staged changes pending final review

---

## [2026-11-24] — Required Status Checks Enforced on `main`

### Changed

- **`main` required-checks ruleset (repository setting)** — Added a ruleset targeting the default branch that requires four status checks to pass before merge: Lint Markdown Files, Check Markdown Links, Check Changelog Updated, and Validate Governance Artifacts. The ruleset has no bypass actors.
- **`.github/workflows/markdown-lint.yml`, `link-validation.yml`, `governance-health.yml`** — Removed the pull-request path filters so each required check reports on every pull request.
- **`docs/exceptions.md`** — Appended a renewal-history note to **EXC-2026-001** recording that its compensating controls are now enforced at merge.

### Rationale

The 2026-11-23 renewal review of EXC-2026-001 found that the checks cited as compensating controls were advisory: the ruleset required none of them and one had not been running. Classified as a **Control Tightening**. The path filters were removed because a required check that does not run leaves a pull request unmergeable.

### Impact Assessment

- **Access & identity:** the owner bypass still covers the second-party approval requirement only; it no longer permits merging with a failing or missing check
- **Operations:** a failing external link or lint error now blocks every merge until fixed; changing that requires an explicit ruleset edit by an organization admin
- **Auditability:** the exception's compensating controls are enforced by configuration rather than by practice

### Approving Authority

- Primary Owner / Organization Owner (via pull-request review under change-control)

---

## [2026-11-23] — Renewed Owner-Bypass Governance Exception (EXC-2026-001)

### Changed

- **`docs/exceptions.md`** — Renewed **EXC-2026-001** (single-contributor self-approval on the `1520ai/.github` `main` ruleset) to 2027-02-23. Recorded the lapse from 2026-11-02 to 2026-11-23, the one pull request (#20) merged under the bypass during it, a renewal review, an updated risk assessment, and a reworded revocation trigger for the renewed period. Original entry text retained. Updated the Last Reviewed date.

### Rationale

The exception expired on 2026-11-02 while the bypass actor remained on the ruleset, leaving an undocumented override in place. Renewal restores a documented, time-bounded basis for it. The renewal review also corrects the record: the ruleset enforces no required status checks, the Governance Health Check had not run since 2026-05-25, and the Exception Expiration Check had been disabled for inactivity (re-enabled 2026-11-23).

### Impact Assessment

- **Access & identity:** unchanged — the owner may self-merge on `1520ai/.github`; non-admin contributors still require second-party approval
- **Auditability:** the lapse and the merge made during it are recorded; the exception is again time-bounded
- **Revocation trigger:** changed from "two or more active engineers in the organization" to "a second engineer assigned to maintain or review this repository"; the organization now has a second active engineer on a separate product repository, so the original wording is met as written

### Approving Authority

- Primary Owner / Organization Owner (via pull-request review under change-control)

---

## [2026-11-23] — Separated the Organization Default CONTRIBUTING from the Governance-Repository Process

### Changed

- **`CONTRIBUTING.md`** — Replaced with a short organization default. It states that each repository sets its own workflow, that a repository's own `CONTRIBUTING.md` replaces the default, and that `SECURITY.md` and `docs/engineering-operating-standards.md` apply everywhere.
- **`docs/governance-contributing.md`** — New location of the previous `CONTRIBUTING.md` text (the contribution process for `1520ai/.github`). Content unchanged apart from relative links and a scope line stating it does not apply to product repositories.
- **`README.md`, `docs/index.md`, governance-change PR and issue templates, `changelog-validation.yml`, `governance-health.yml`** — References repointed to the new location; the health check now requires both files.

### Rationale

GitHub displays this repository's `CONTRIBUTING.md` on every organization repository that lacks its own. The previous file was scoped to this repository and described control-plane change handling (change classification, exception registry), so it appeared on a new product repository as if it were that team's required development process. Classified as a **Clarification**: no rule, authority, or enforcement behavior changed.

### Impact Assessment

- **Behavioral:** none for this repository — the same process governs it, at a new path
- **Other repositories:** repositories without their own `CONTRIBUTING.md` now display the generic default instead of the governance process
- **Security / Regulatory:** none — `SECURITY.md` is unchanged and remains organization-wide

### Approving Authority

- Primary Owner / Organization Owner (via pull-request review under change-control)

---

## [2026-08-02] — Documented Owner-Bypass Governance Exception (EXC-2026-001)

### Changed

- **`docs/exceptions.md`** — Registered **EXC-2026-001**: single-contributor self-approval on the `1520ai/.github` `main` branch ruleset (an `OrganizationAdmin` bypass actor), invoking the single-contributor-repository provision of `engineering-operating-standards.md`. Recorded a Last Reviewed date.

### Rationale

The `main` ruleset requires an approving review from someone other than the last pusher. With `1520ai` effectively single-contributor and other members unavailable, the organization owner added an `OrganizationAdmin` bypass to keep governance-repo maintenance unblocked. Per the engineering standard, such a self-approval exception MUST be documented with compensating controls — this entry does so, converting an otherwise-undocumented override into a sanctioned, time-bounded, auditable exception.

### Impact Assessment

- **Access & identity:** the owner may self-merge on `1520ai/.github`; every other ruleset protection and required check remains enforced, and non-admin contributors still require second-party approval
- **Auditability:** the bypass is now registered, time-bounded (expires 2026-11-02), and carries an explicit revocation trigger (active engineers ≥ 2)

### Approving Authority

- Primary Owner / Organization Owner (via pull-request review under change-control)

---

## [2026-08-02] — Refreshed Engineering Standards & Model Registry for Currency

### Changed

- **docs/engineering-operating-standards.md**
  - Added the organizing principle "a standard that can't fail a build is a preference"
  - Added an **Enforcement Classes** table (Correctness, Types & quality, PHI & privacy,
    Security supply chain, Compliance & traceability, Resilience & operations, Access &
    identity) with product-agnostic baseline bars
  - Added a **No silent debt** binding invariant (visible shortcuts with owner + CI-enforced deadline)
  - Added an **Adopting This in a New Repository** section (stand up enforcement classes before feature code)
  - Recorded a Last Reviewed date
- **docs/model-registry.md**
  - Replaced the product-specific placeholder example (`hospiclarity-summarizer-v2`) with a generic one (`<product>-deid-ner-v1`) so the org schema bakes in no single product's model
  - Added **Decision Role** (Enforcing / Advisory / Auxiliary) as a required field and to the entry template
  - Added §4.4 **Decision Role and Model Independence** — enforcement-adjacent models must record whether the binding output is model-independent by construction
  - Recorded a Last Reviewed date

### Rationale

Both documents had drifted from current practice (frozen 2026-01-15) while the flagship
product's engineering standards advanced. This refresh pulls the flagship's mechanized
"enforced, not stated" framing up to the org baseline and removes a fictional product
model from the registry schema, ahead of sibling products inheriting these standards.
The Decision Role / model-independence addition captures a load-bearing lesson: a model
may be registered yet sit outside the binding regulatory decision path, which should be
stated so swaps validate structurally.

### Impact Assessment

- **Standards:** org baseline now expresses enforcement classes and bars explicitly; no bar was weakened
- **Model governance:** registries must classify each model's decision role; no existing entry is invalidated
- **Onboarding:** new repositories get a concrete adoption checklist

### Approving Authority

- Primary Owner / Platform Engineering (via pull-request review under change-control)

---

## [2026-03-19] — Alignment Update from Hospiclarity Platform Audit

### Changed

- **`docs/engineering-operating-standards.md`** — Added single-contributor repository exception for PR review requirements, with compensating controls (CI gates, AI-assisted review, documented transition plan). Addresses pre-team phase where multi-reviewer approval is not feasible.
- **`docs/governance.md`** — Added guidance that product repositories may refine the 5-level authority hierarchy into a more granular model, provided precedence order is preserved. Reflects Hospiclarity's 7-layer authority graph as a valid refinement.

### Rationale

Cross-referencing the org standards against the Hospiclarity platform codebase (commit `bd7a3d55`) revealed two areas where the org standards didn't accommodate the realities of a pre-team, single-founder product repository. The standards assumed multi-engineer teams and a single authority hierarchy depth. These updates acknowledge valid patterns while preserving governance intent.

### Classification

- Type: Clarification
- Impact: Low — no existing controls weakened
- Affected repositories: All (standards are org-wide)

---

## [2026-01-15] — README Comprehensive Update

### Changed

- **README.md Overhaul**
  - Added reference to docs/index.md as authoritative document catalog
  - Updated document listing to include all 19 governance artifacts
  - Added governance framework overview with categorized document tables
  - Updated onboarding path to include ai-release-gates, incident-response, training
  - Added AI Release Gates summary with 6 mandatory gates
  - Added Automated Governance section documenting CI workflows
  - Updated status from "evolving" to "active and binding"
  - Removed outdated placeholder language

### Rationale

README was out of date with the comprehensive governance framework. Updated to accurately reflect current state and provide clear entry points to documentation.

### Impact Assessment

- **Documentation:** README now accurately represents governance framework
- **Onboarding:** Clear path for new team members to governance documentation

### Approving Authority

- VP, AI Engineering
- VP, Technology & Engineering

---

## [2026-01-15] — Business Continuity, Training & Governance Metrics

### Added

- **Business Continuity & Disaster Recovery Framework**
  - Defined RTO/RPO objectives by system tier
  - Established AI system classification for BC/DR requirements
  - Created failover and failback procedures
  - Defined DR testing requirements and schedules
  - Document: `docs/business-continuity.md`

- **Training & Awareness Program**
  - Defined required training matrix by role
  - Established onboarding requirements and checklists
  - Created training compliance tracking requirements
  - Defined awareness program activities (newsletters, phishing simulations)
  - Document: `docs/training-awareness.md`

- **Governance Metrics & KPIs Framework**
  - Defined compliance, security, AI, and operational metrics
  - Established dashboard requirements for different audiences
  - Created threshold and alerting requirements
  - Defined reporting cadence and distribution
  - Document: `docs/governance-metrics.md`

- **Documentation Index Updates**
  - Added business-continuity.md, training-awareness.md, and governance-metrics.md to index
  - Expanded document classification and change impact tables

### Rationale

Completed governance control plane documentation to address remaining gaps in business continuity, personnel readiness, and governance visibility. These additions achieve comprehensive coverage for enterprise-grade healthcare AI governance.

### Impact Assessment

- **Behavioral:** Establishes BC/DR and training requirements for all personnel
- **Operational:** Provides metrics framework for continuous governance monitoring
- **Regulatory:** Strengthens HIPAA contingency plan and workforce training compliance

### Approving Authority

- VP, AI Engineering
- VP, Technology & Engineering

---

## [2026-01-15] — Vendor Management, Audit Coordination & AI Security

### Added

- **Vendor Management Framework**
  - Defined vendor classification tiers based on data access
  - Established vendor qualification process and security assessment requirements
  - Formalized BAA and DPA requirements for third-party relationships
  - Created vendor registry schema and ongoing monitoring requirements
  - Document: `docs/vendor-management.md`

- **Audit Coordination Framework**
  - Defined audit artifact management and versioning requirements
  - Established audit preparation checklist and evidence collection process
  - Created finding classification, tracking, and remediation workflows
  - Formalized compliance attestation requirements and templates
  - Defined regulatory correspondence management
  - Document: `docs/audit-coordination.md`

- **AI Security & LLM Threat Defense**
  - Defined AI-specific threat model including prompt injection and jailbreaking
  - Established the "lethal trifecta" prohibition (untrusted input + sensitive data + action)
  - Created input validation and prompt injection prevention requirements
  - Defined output validation, sanitization, and filtering requirements
  - Established prompt security and system prompt protection standards
  - Defined AI security testing requirements and adversarial testing
  - Document: `docs/ai-security.md`

- **Documentation Index Updates**
  - Added vendor-management.md, audit-coordination.md, and ai-security.md to index
  - Expanded document classification and change impact tables

### Rationale

Completed governance control plane with vendor oversight, audit coordination, and AI-specific security requirements. These additions address remaining gaps for enterprise-grade healthcare AI governance.

### Impact Assessment

- **Behavioral:** Establishes vendor qualification and audit preparation requirements
- **Security:** Formalizes AI/LLM-specific threat defense requirements
- **Regulatory:** Strengthens audit coordination and compliance attestation capabilities

### Approving Authority

- VP, AI Engineering
- VP, Technology & Engineering

---

## [2026-01-15] — Model Registry, Data Lineage & Exception Automation

### Added

- **AI Model Registry Framework**
  - Defined schema for tracking deployed AI models
  - Established model lifecycle states and governance requirements
  - Integrated with Sensitivity × Consensus classification
  - Document: `docs/model-registry.md`

- **Data Lineage & Provenance Requirements**
  - Defined data source documentation requirements
  - Established transformation tracking standards
  - Created training dataset registry schema
  - Defined PHI-specific lineage requirements
  - Document: `docs/data-lineage.md`

- **Exception Expiration Automation**
  - Added workflow to check for expiring exceptions
  - Automatic issue creation for exceptions expiring within 30 days
  - CI failure on expired exceptions in registry
  - Updated exception registry with structured entry template
  - Workflow: `.github/workflows/exception-expiration.yml`

- **Documentation Index Updates**
  - Added model-registry.md and data-lineage.md to index
  - Expanded document classification and change impact tables

### Rationale

Extended governance control plane to address gaps in AI model tracking, data provenance, and exception lifecycle management. These additions strengthen audit defensibility and enable automated governance health monitoring.

### Impact Assessment

- **Behavioral:** Establishes mandatory model and data documentation
- **Security:** Improves traceability for PHI data flows
- **Regulatory:** Strengthens audit trail for AI model governance and data lineage

### Approving Authority

- VP, AI Engineering
- VP, Technology & Engineering

---

## [2026-01-15] — AI Release Gates & Incident Response

### Added

- **AI Release Gates Framework**
  - Defined 6 mandatory validation gates for AI production deployment
  - Established gate applicability based on Sensitivity × Consensus classification
  - Formalized emergency release procedures with accountability
  - Document: `docs/ai-release-gates.md`

- **Incident Response & Learning Framework**
  - Formalized incident severity levels and response timelines
  - Established 5-phase incident response process
  - Defined blameless post-mortem requirements
  - Created governance feedback loop from incidents to improvements
  - Document: `docs/incident-response.md`

- **Governance Health Automation**
  - Added CI workflow to validate governance artifact integrity
  - Automated checks for required files, CODEOWNERS, and cross-references
  - Weekly scheduled validation with PR-triggered checks
  - Workflow: `.github/workflows/governance-health.yml`

- **Documentation Index Updates**
  - Added new documents to index.md
  - Updated onboarding path to include new artifacts
  - Expanded document classification table

### Rationale

Extended governance control plane to address gaps in AI deployment validation and incident learning. These additions strengthen audit defensibility and create formal feedback loops from operational incidents to governance improvements.

### Impact Assessment

- **Behavioral:** Establishes mandatory pre-production gates for AI systems
- **Security:** Formalizes incident escalation and containment requirements
- **Regulatory:** Improves audit trail for AI deployment decisions and incident handling

### Approving Authority

- VP, AI Engineering
- VP, Technology & Engineering

---

## [2026-01-01] — Initial Governance Baseline

### Added

- **Organization Governance & Authority Model**
  - Defined authority hierarchy and decision precedence
  - Established binding invariants and enforcement mechanisms
  - Document: `docs/governance.md`

- **Change Control & Exception Management**
  - Formalized change proposal, review, approval, and documentation flow
  - Defined exception lifecycle and registry requirements
  - Document: `docs/change-control.md`

- **Responsible AI Framework**
  - Established Sensitivity × Consensus risk model
  - Defined Responsible AI posture, lifecycle scope, and release constraints
  - Document: `docs/responsible-ai.md`

- **Security & Data Protection Baselines**
  - Referenced AI Security and data protection expectations
  - Integrated misuse resistance and human-in-the-loop principles
  - Documents: `SECURITY.md`, related governance artifacts

### Rationale

Established foundational governance infrastructure to support audit defensibility, regulatory alignment, and operational clarity as 1520ai scales.

### Impact Assessment

- **Behavioral:** Establishes binding expectations for design, review, and release
- **Security:** Strengthens preventive controls and escalation clarity
- **Regulatory:** Improves audit defensibility and authority traceability

### Approving Authority

- VP, AI Engineering
- VP, Technology & Engineering

---

## Exception Tracking

Active and historical exceptions are tracked separately in:

- [docs/exceptions.md](docs/exceptions.md)

Each exception entry references:

- The approving pull request
- Expiration date
- Renewal history (if applicable)

---

## Governance Notes

- Undocumented changes are treated as non-compliant
- Retroactive changelog entries are not permitted except for documented emergency changes
- This file is append-only

---

## Status

This changelog is **active and binding**.

All governance, security, and Responsible AI changes must be reflected here before taking effect.
