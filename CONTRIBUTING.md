# Contributing to 1520ai Governance Repositories

**Status:** Active
**Scope:** This repository (.github)
**Audience:** Authorized contributors and maintainers

---

## Purpose

This document defines how changes are proposed, reviewed, approved, and merged for 1520ai governance, security, and Responsible AI artifacts.

This repository governs how other repositories operate.
As such, contributions here are treated as **control-plane changes**, not ordinary documentation edits.

---

## Who May Contribute

- This repository is not open to external contributions
- Only authorized contributors within the 1520ai organization may propose changes
- All changes require review and approval per CODEOWNERS

---

## Types of Changes

All changes MUST be classified into one of the following categories, as defined in [docs/change-control.md](docs/change-control.md):

| Type | Description |
|------|-------------|
| **Policy Change** | Alters authority, obligations, or constraints |
| **Control Tightening** | Adds or strengthens safeguards without expanding scope |
| **Clarification** | Improves wording without changing meaning or authority |
| **Exception** | Temporary, time-bounded deviation from baseline governance |

**Unclassified changes will not be merged.**

---

## Required Contribution Process

All contributions follow the same high-level flow:

1. Propose
2. Review
3. Approve
4. Document
5. Enforce

Each step is mandatory.

---

## Before Opening a Pull Request

Before submitting a PR, contributors MUST:

- Identify the change type
- Identify the affected artifacts
- Determine whether the change:
  - Introduces new authority
  - Alters enforcement behavior
  - Requires an exception
- Draft any required:
  - Changelog entry
  - Exception registry entry (if applicable)

**Security or Responsible AI implications must be called out explicitly.**

For complex or high-impact changes, contributors are encouraged to open a draft PR or discuss with CODEOWNERS early, before investing in a full proposal.

---

## Pull Request Requirements

Every PR MUST include:

- A clear description of:
  - What is changing
  - Why it is changing
- Explicit change classification (Policy / Tightening / Clarification / Exception)
- Links to affected documents
- Required documentation updates:
  - `CHANGELOG.md` (mandatory for all non-trivial changes)
  - `docs/exceptions.md` (if an exception is introduced or modified)

A pull request template is available at [.github/PULL_REQUEST_TEMPLATE/](.github/PULL_REQUEST_TEMPLATE/) to guide contributors through these requirements.

**PRs lacking required documentation will not be merged.**

---

## Review & Approval

- Reviewers are determined by CODEOWNERS
- Approval signifies:
  - Understanding of the change
  - Acceptance of downstream impact
  - Willingness to defend the change in audit or incident review

**Silence is not approval.**

---

## Responsible AI Review

Changes that affect:

- AI behavior
- Model scope
- Decision authority
- Output framing
- Monitoring or escalation logic

MUST be reviewed for alignment with [docs/responsible-ai.md](docs/responsible-ai.md).

**If Responsible AI constraints are violated, the PR will be blocked or redesigned.**

---

## Security Review

Changes that affect:

- Data handling
- Access control
- Logging or audit trails
- Model execution boundaries
- Prompt or input handling

MUST be reviewed under [SECURITY.md](SECURITY.md).

**Security issues MUST be escalated, not patched quietly.**

---

## Exceptions

Exceptions are not shortcuts.

If a PR introduces an exception:

- It MUST be documented in [docs/exceptions.md](docs/exceptions.md)
- It MUST include:
  - Rationale
  - Scope
  - Risk assessment
  - Mitigations
  - Expiration date
- Exceptions expire by default unless explicitly renewed

**Undocumented exceptions are invalid.**

---

## Emergency Changes

Emergency changes may be applied when delay would materially increase risk.

Emergency changes:

- MAY bypass standard sequencing temporarily
- MUST be documented retroactively
- MUST undergo post-hoc review
- MUST be recorded in `CHANGELOG.md`

**Emergency status does not exempt changes from review.**

---

## Commit Message Conventions

No specific commit message format is required.

However, commit messages should be clear, concise, and describe the intent of the change. When in doubt, prefer clarity over brevity.

---

## Merge Criteria

A PR may be merged only when:

- All required reviews are complete
- Documentation is updated
- Conflicts with governance are resolved
- Enforcement implications are understood

**Merged changes are considered binding immediately, unless otherwise stated.**

---

## Enforcement

This process is enforced via:

- CODEOWNERS
- CI checks (where configured)
- Audit and incident review

**Failure to follow this process is treated as a system risk, not a procedural error.**

---

## Final Note

This repository exists to protect:

- System integrity
- Regulatory defensibility
- Organizational trust

Contributions here should optimize for **clarity, discipline, and long-term resilience** over speed or convenience.
