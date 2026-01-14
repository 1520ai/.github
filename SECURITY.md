# 1520ai — Security Policy & Disclosure

**Status:** Active
**Effective Date:** 2026-01-01
**Scope:** Organization-wide
**Audience:** Internal teams, auditors, partners, security researchers

---

## Purpose

1520ai builds systems for regulated, audit-sensitive environments. Security is treated as a first-class system constraint, not an implementation detail.

This document defines how security issues are:

- Identified
- Reported
- Escalated
- Resolved

without altering governing authority or safety semantics.

---

## Scope

This policy applies to:

- All 1520ai repositories and services
- All models, agents, and prompts
- All data inputs, outputs, and logs
- All monitoring and evaluation systems
- All documentation governing system behavior

---

## Security Authority Boundary

Security controls at 1520ai are protective, not governing.

**Security mechanisms may:**

- Restrict access
- Block unsafe execution
- Trigger escalation
- Require remediation

**Security mechanisms may not:**

- Define regulatory requirements
- Alter governing decision criteria
- Override binding safety or authority constraints
- "Score past" enforcement rules via convenience-driven exceptions

**If a security control conflicts with a governing document, governance prevails.**

---

## What Constitutes a Security Issue

Security issues include, but are not limited to:

- Unauthorized access to data or systems
- Exposure of protected health information (PHI)
- Prompt or model injection vulnerabilities
- Unintended data exfiltration
- Privilege escalation
- Circumvention of governance or authority controls
- Nondeterministic behavior introduced into enforcement paths
- Silent modification of logs, gates, or outputs

**Security issues are treated as incidents, not bugs.**

---

## Reporting a Security Issue

### Internal Reporting (Preferred)

All internal security concerns MUST be reported via one of the following:

- GitHub Security Advisory (preferred, when enabled)
- A repository issue labeled `Security` (when advisory workflow is unavailable)
- Direct escalation to the repository CODEOWNERS / maintainers
- Incident escalation per product operations runbooks (if applicable)

**Do not attempt to quietly fix or work around a security issue.**

### External Reporting

**Email:** security@1520.ai

Please include:

- Description of the issue
- Steps to reproduce (if applicable)
- Affected repository or system
- Any proof-of-concept artifacts

**Do not publicly disclose issues prior to coordination.**

We aim to acknowledge external reports within three business days.

---

## Triage & Escalation Timing

### Urgent Issues

Urgent issues include (non-exhaustive):

- Suspected PHI exposure
- Active exploitation or compromise
- Discovered security control failure
- AI behavior violating documented hard stops or safety constraints

**Expectation:** Initial triage SHOULD occur within one business day.

### Non-Urgent Issues

Non-urgent issues are triaged within a reasonable planning cycle based on impact and risk.

### Escalation Path

1. Security owner / designated maintainer (per CODEOWNERS)
2. Engineering leadership
3. Governance leadership (if regulatory or systemic risk exists)

If the designated authority is unavailable, escalation proceeds up the authority hierarchy.

---

## Incident Handling

All confirmed security incidents MUST:

- Be logged as an incident
- Be assessed for impact and scope
- Trigger containment actions if necessary
- Result in remediation and, where appropriate, documentation updates

Security incidents may require:

- Temporary feature suspension
- Access revocation
- Rollback of affected components

### Incident Learning Ledgers

Product repositories may maintain Incident Learning Ledgers—structured records of security and operational incidents used to drive systemic improvement. Where they exist, incidents MUST be recorded according to the product's operations documentation.

---

## Model and AI Security

Models and agents at 1520ai are subject to additional security constraints:

- No autonomous decision authority
- No learning from production data without review
- No hidden state persistence
- Explicit input/output schema validation
- Deterministic execution in enforcement paths

**Model-related security failures are treated as high-severity incidents.**

---

## Monitoring & Detection

Security monitoring SHOULD include:

- Access control auditing
- Anomaly detection
- Drift monitoring
- Integrity checks on outputs and critical artifacts

### PHI Tripwire (Recommended Control)

Repositories that process healthcare text SHOULD implement PHI detection controls (e.g., NER- or rules-based tripwires).

If implemented:

- Tripwire failures are treated as security incidents and must be triaged
- Whitelist changes are governed actions requiring justification (to prevent quiet weakening of safeguards)
- Tripwires are safety nets (high-recall), not compliance certifications

---

## Emergency Changes

Emergency security changes may be executed when delay would materially increase exposure (e.g., suspected PHI leakage, active exploit).

Emergency changes:

- MAY be applied before full review
- MUST be documented retroactively
- MUST undergo post-hoc review
- MUST be logged in `CHANGELOG.md`

---

## Relationship to Governance & Change Control

- Authority and precedence are defined in [docs/governance.md](docs/governance.md)
- Change and exception handling follow [docs/change-control.md](docs/change-control.md)
- Active exceptions are tracked in [docs/EXCEPTIONS.md](docs/EXCEPTIONS.md)

**Security controls protect the system; they do not redefine what the system is allowed to decide.**

---

## Safe Harbor

1520ai supports good-faith security research.

**We commit to:**

- Not pursuing legal action against good-faith researchers
- Working collaboratively to validate and remediate issues

**Researchers are expected to:**

- Avoid unnecessary data access
- Avoid service disruption
- Provide reasonable time for remediation before disclosure

---

## Status

This policy is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
