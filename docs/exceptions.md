# 1520ai — Governance Exceptions Registry

**Status:** Active
**Scope:** Organization-wide
**Maintained by:** Designated CODEOWNERS
**Last Reviewed:** 2026-08-02

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

### EXC-2026-001: Single-Contributor Self-Approval on `1520ai/.github`

| Field | Value |
| ----- | ----- |
| Exception ID | EXC-2026-001 |
| Status | Active |
| Affected Artifact | `1520ai/.github` `main` branch ruleset (require last-push approval + 1 review) |
| Granted | 2026-08-02 |
| Expires | 2026-11-02 |
| Approving PR | #PRNUM |
| Approver | @jeff1520ai (Organization Owner) |

**Rationale:** `1520ai` is currently a single-active-contributor organization; the other repository members are not reliably available to provide the second-party approval the `main` ruleset requires. Blocking all governance-repo maintenance on an unavailable reviewer is impractical during this pre-team phase. This exception invokes the single-contributor-repository provision in [engineering-operating-standards.md](engineering-operating-standards.md).

**Scope:** An `OrganizationAdmin` bypass actor (mode: always) is present on the `1520ai/.github` `main` ruleset, allowing the organization owner to merge their own pull requests without a second approval. The ruleset's other protections remain fully enforced for every actor: required pull request, no direct pushes, no branch deletion, no force-push, and all required status checks. Non-admin contributors still require a second-party approval.

**Risk Assessment:** Residual risk (one person merging their own change to org governance) is mitigated by the compensating controls the standard requires:

1. Comprehensive automated CI gates on every PR — markdown lint, link validation, changelog validation, governance-artifact validation, and CodeQL — all of which must pass before merge.
2. AI-assisted code review on changes.
3. A documented commitment to remove this exception and return to mandatory second-party review once a second active engineer is onboarded.

**Revocation trigger:** This exception MUST be revoked (the bypass actor removed from the ruleset) when the organization reaches two or more active engineers, or at expiry, whichever comes first. Renewal requires re-review and an updated risk assessment.

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
