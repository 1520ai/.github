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

## Exception Entry Template

When adding an exception, use the following format:

```markdown
### EXC-YYYY-NNN: [Brief Title]

| Field | Value |
| ----- | ----- |
| Exception ID | EXC-YYYY-NNN |
| Status | Active / Pending Renewal / Expired |
| Affected Artifact | [Document or system affected] |
| Granted | YYYY-MM-DD |
| Expires | YYYY-MM-DD |
| Approving PR | #NNN |
| Approver | [Name/Role] |

**Rationale:** [Why this exception is needed]

**Scope:** [What is covered by this exception]

**Risk Assessment:** [Risks and mitigations]

**Renewal History:** (if applicable)
- YYYY-MM-DD: [Renewal notes]
```

---

## Active Exceptions

<!-- Active exceptions are listed below. When an exception expires, move it to the Expired section. -->

_No active exceptions at this time._

---

## Pending Renewal

Exceptions approaching expiration within 30 days.

(Add entries as needed.)

---

## Expired Exceptions

Expired exceptions are retained for audit and historical review.

**No expired exceptions at this time.**

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
