# 1520ai — Change Control & Exception Management

## Purpose

This document defines the formal mechanisms by which changes to governance, security, compliance, and AI standards are:

- Proposed
- Reviewed
- Approved
- Versioned
- Audited

It ensures that material changes are intentional, traceable, and reviewable, and that exceptions do not silently become permanent behavior.

**This document is binding across all 1520ai repositories.**

---

## Relationship to Governance

[docs/governance.md](governance.md) defines **what** must be governed and **who** has authority.

This document defines **how** changes and exceptions are executed and controlled.

If there is a conflict, governance authority takes precedence.

---

## What Requires Change Control

Change control **MUST** be applied to:

- Governance artifacts
- Security or data protection policies
- Responsible AI standards
- Authority hierarchies or decision ownership
- Release gates or enforcement mechanisms

Change control **MAY** be applied to:

- Templates and workflows
- Documentation clarifications that affect interpretation

Purely editorial changes that do not alter meaning MAY be fast-tracked.

---

## Change Types

All proposed changes fall into one of the following categories:

| Type | Description | Review Requirement |
|------|-------------|-------------------|
| **Policy Change** | Introduces, removes, or materially alters a rule or constraint. | Always requires full review. |
| **Control Tightening** | Increases enforcement, scope, or rigor without reducing safeguards. | Requires review; typically lower risk. |
| **Clarification** | Improves precision without changing intent. | Requires documentation and approval. |
| **Exception** | Temporarily deviates from an existing rule. | Subject to expiration and renewal. |

---

## Standard Change Process

All governed changes follow this sequence unless explicitly exempted.

### Step 1 — Proposal

- Proposed via pull request
- PR MUST include:
  - Description of change
  - Change type
  - Affected artifact(s)
  - Rationale
  - Impact assessment

### Step 2 — Review

Reviewers are determined by:

- CODEOWNERS
- Decision class defined in [governance.md](governance.md)

Cross-cutting changes (e.g., AI + PHI) require joint review.

**Expected review timing (non-urgent):**
Reviews SHOULD begin within a reasonable planning cycle.
Urgent timing expectations are defined in [governance.md](governance.md).

### Step 3 — Approval

- Approval authority is determined by the highest applicable authority
- Approval MUST be explicit (PR approval is sufficient if authority is correct)

### Step 4 — Documentation

- Approved changes MUST be recorded in `CHANGELOG.md`
- Changelog entry is required before merge

### Step 5 — Enforcement

Changes take effect only after:

- Merge
- Required CI/CD, release gate, or enforcement updates

---

## Changelog Requirements

All governed changes are logged in `CHANGELOG.md`.

### Minimum Entry Structure

Each entry MUST include:

| Field | Description |
|-------|-------------|
| Date | When the change was approved |
| Artifact(s) affected | Which document(s) changed |
| Change type | Policy, control tightening, clarification, or exception |
| Summary | Brief description of the change |
| Impact assessment | Behavioral, security, regulatory, or none |
| Approving authority | Who approved the change |

This enables audit reconstruction and historical traceability.

---

## Exception Management

Exceptions are allowed but constrained.

They exist to manage real-world constraints—not to bypass governance.

### Exception Registry (Source of Truth)

All active and historical exceptions are tracked in:

- **[docs/exceptions.md](exceptions.md)** (append-only registry)

Each exception entry MUST reference:

- The approving pull request
- Expiration date
- Current status (Active / Expired / Renewed)

**Undocumented exceptions are treated as invalid.**

### Exception Requirements

All exceptions:

- Are explicit, never implicit
- Are documented in the registry
- Are approved by appropriate authority
- Are time-bounded

The exception template and required fields are defined in:
→ [docs/governance.md](governance.md) (single source of truth)

### Expiration & Renewal

- Exceptions expire by default
- Renewal requires:
  - Re-review
  - Updated risk assessment
  - Explicit re-approval
  - New expiration date

**Expired exceptions revert to baseline governance automatically.**

---

## Fast-Track Changes

Fast-track handling is permitted only for:

- Typographical fixes
- Formatting corrections
- Clarifications that do not alter interpretation

Fast-tracked changes:

- Still require PRs
- Still require approval
- MAY be grouped in the changelog

**Fast-track is not a bypass mechanism.**

---

## Emergency Changes

Emergency changes may be executed when delay would materially increase risk, such as:

- Active or suspected PHI exposure
- Discovered security control failure
- AI behavior violating documented hard stops
- Regulatory non-compliance identified during live operations

Emergency changes:

- MAY be applied before full review
- MUST be documented retroactively
- MUST undergo post-hoc review
- MUST be logged in `CHANGELOG.md` with justification

**Emergency handling is exceptional, not routine.**

---

## Audit & Review Expectations

Change control artifacts must support:

- Timeline reconstruction
- Authority verification
- Impact analysis

**Undocumented or unapproved changes are treated as governance violations, not procedural errors.**

---

## Enforcement

This process is enforced through:

- CODEOWNERS
- Required reviews
- CI/CD gating
- Release approvals
- Incident and audit reviews

**Failure to follow change control is considered a systemic risk.**

---

## Status

This document is **active and binding**.

It will evolve as:

- Regulatory expectations change
- Products approach clinical deployment
- Governance maturity increases

All changes are versioned, reviewed, and auditable.
