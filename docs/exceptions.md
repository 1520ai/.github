# 1520ai — Governance Exceptions Registry

**Status:** Active
**Scope:** Organization-wide
**Maintained by:** Designated CODEOWNERS
**Last Reviewed:** 2026-01-01

---

## Purpose

This document is the authoritative registry of all governance exceptions granted across 1520ai.

It exists to ensure that exceptions are:

- Explicit
- Traceable
- Time-bounded
- Auditable

Exceptions are not policy changes. They are controlled deviations granted to manage real-world constraints.

**Undocumented exceptions are treated as invalid.**

---

## Relationship to Governance

- Authority and eligibility for exceptions are defined in [docs/governance.md](governance.md)
- Exception mechanics and lifecycle are defined in [docs/change-control.md](change-control.md)
- All exceptions must reference an approved pull request and changelog entry

**This registry is the single source of truth for exception status.**

---

## How to Use This Registry

- Every exception must have an entry in this file
- Entries are append-only
- Exceptions move between sections (Active → Expired) but are never deleted
- Expired exceptions automatically revert to baseline governance

---

## Active Exceptions

**No active exceptions at this time.**

(Add new entries below this line.)

---

### Exception ID: EX-YYYY-001

**Status:** Active

**Affected Artifact(s):**
- e.g., `docs/responsible-ai.md`, Product XYZ release gate

**Decision Class(es):**
- e.g., AI Behavior & Model Governance

**Rationale:**
Clear, concrete explanation of why the exception is necessary.

**Scope:**
What is affected and what is explicitly not affected.

**Risk Assessment:**
Summary of introduced risk and why it is acceptable temporarily.

**Mitigations:**
Controls or compensating safeguards in place during the exception.

**Approval:**
- Approving Authority: Role(s)
- Approval PR: `#123`
- Date Approved: YYYY-MM-DD

**Expiration:**
- Expiration Date: YYYY-MM-DD
- Renewal Required: Yes / No

---

## Pending Renewal

Exceptions approaching expiration within 30 days.

(Add entries as needed.)

---

## Expired Exceptions

Expired exceptions are retained for audit and historical review.

---

### Exception ID: EX-YYYY-000

**Status:** Expired

**Affected Artifact(s):**
- e.g., Security policy XYZ

**Decision Class(es):**
- e.g., Security & Data Protection

**Rationale:**
Brief summary of why the exception existed.

**Duration:**
- Approved: YYYY-MM-DD
- Expired: YYYY-MM-DD

**Outcome:**
- Baseline governance restored
- Exception replaced by policy change / control tightening / system fix

**Approval:**
- Approving Authority: Role(s)
- Approval PR: `#XYZ`

---

## Review & Maintenance

This registry is reviewed:

- During audits
- During incident reviews
- As part of governance health checks
- Quarterly, or more frequently as needed

Expired exceptions must not be reactivated without a new approval cycle.

**Repeated exceptions in the same area signal a governance or system design gap.**

---

## Enforcement Notes

- Exceptions not listed here are non-compliant
- Silent extensions or informal agreements are prohibited
- CI or governance checks may validate:
  - Presence of registry entry
  - Expiration dates
  - Renewal status

---

## Status

This registry is **active and binding**.

It evolves only through the formal change-control process.

**Exceptions exist to manage reality — not to erode standards.**
