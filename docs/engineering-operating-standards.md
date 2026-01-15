# 1520ai — Engineering Standards

**Status:** Active
**Effective Date:** 2026-01-01
**Scope:** Organization-wide
**Audience:** All engineers, contributors, and technical reviewers

---

## Purpose

These engineering standards establish baseline expectations for all contributors across 1520ai repositories. They synthesize guidance from organization governance documents with industry-recognized best practices for safety, regulatory compliance, and software craftsmanship.

All engineers are expected to follow these standards in addition to any product-specific requirements and governance controls.

**This document defines how we build. Governance documents define what we are allowed to build.**

---

## Relationship to Organization Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/change-control.md](change-control.md) — Change and exception mechanics
- [docs/responsible-ai.md](responsible-ai.md) — AI posture and constraints
- [SECURITY.md](../SECURITY.md) — Security escalation and incident handling

Product repositories MAY define stricter engineering standards, but they:

- MUST reference this document
- MUST NOT weaken or contradict it
- SHOULD explicitly list additional constraints

---

## Quick Reference (Critical Rules)

1. **Documentation over code** — If implementation conflicts with documentation, documentation wins
2. **No silent overrides** — Governance controls cannot be bypassed programmatically
3. **Deterministic outputs** — Systems must produce identical outputs for identical inputs
4. **PHI is never casual** — Treat all protected health information with maximum care
5. **Human judgment remains primary** — AI assists but never enforces regulatory decisions
6. **Security issues are incidents** — Report immediately; do not quietly fix
7. **Test what matters** — Prioritize coverage of core logic and security-critical paths

---

## 1. Coding Style and Documentation

### 1.1 Python Style

**Indentation and whitespace**
Use 4 spaces per indentation level. Do not mix tabs and spaces.

**Line length**
Default limit is 88 characters (Black default). Teams may adopt stricter limits (79) or relaxed limits (up to 120) with explicit agreement documented in the repository.

**Imports**
Place imports at the top of files after module docstrings and group them as: standard library, third-party packages, then local modules. Avoid wildcard imports; be explicit.

**Blank lines**
Surround top-level function and class definitions with two blank lines and use a single blank line between methods inside a class.

### 1.2 Docstrings

All modules, classes, functions, and exported methods must have docstrings. Follow [PEP 257](https://peps.python.org/pep-0257/) conventions:

- Use triple double quotes (`"""`) for docstrings
- One-line docstrings should fit on a single line and use a concise imperative summary ("Return the pathname…"), not a description of parameters
- Multi-line docstrings start with a summary line, followed by a blank line and then a more detailed description
- Document return types and side effects; avoid duplicating parameter names

### 1.3 Naming Conventions

- Use `snake_case` for functions and variables; `CamelCase` for class names
- Prefix private attributes and helper functions with a single underscore
- Avoid abbreviations unless they are well known (e.g., URI, UTC)
- File and module names should be lowercase and avoid hyphens

### 1.4 Other Languages

For languages other than Python, follow established community style guides (e.g., Google Style Guides, Airbnb for JavaScript/TypeScript) unless a product repository specifies otherwise.

---

## 2. Version Control and Commit Discipline

### 2.1 Git Practices

**Branch structure**
Use short-lived branches with descriptive names (`feature/…`, `bugfix/…`, `governance/…`) and open pull requests early.

**Atomic commits**
Each commit should contain a logically complete unit of work. Do not mix unrelated changes.

**Commit messages**
Write clear titles in the imperative mood (e.g., "Add validation for gate inputs"), followed by a blank line and a body describing why the change was made. Reference related issues or governance tickets when appropriate.

**Rebasing**
Rebase feature branches onto the latest main or dev regularly to keep history linear and avoid large merge conflicts.

**Tagging and releases**
Follow Semantic Versioning (MAJOR.MINOR.PATCH) and document changes in `CHANGELOG.md`. Releases containing authority-affecting changes require governance review.

### 2.2 Pull Request Requirements

**Documentation first**
For changes that alter how a system decides, enforces, or explains outcomes, update relevant documentation before modifying code. Per [governance.md](governance.md), documentation overrides implementation.

**Code review**
At least one other engineer must approve every PR. Use small PRs (<400 lines of code) and time-boxed reviews (60–90 minutes) to reduce reviewer fatigue. Larger changes require explicit justification.

**Checklists**
Reviewers should work through a checklist covering functionality, readability, security, performance, and tests. Code that touches security-critical areas—authentication, authorization, data validation, cryptography, or API endpoints—requires heightened scrutiny.

**Static analysis**
Run linting and static security analysis automatically as part of CI. Tools help catch obvious issues but do not replace human review.

**Constructive feedback**
Comments should explain why an issue is problematic and suggest improvements. Avoid terse or personal criticism; foster a collaborative environment.

**Documentation of decisions**
Summarize key findings and resolutions in the PR description or in a team wiki. Maintaining a record of common mistakes accelerates future reviews.

**Involving juniors**
Include junior engineers in reviews to build collective understanding and encourage knowledge transfer.

---

## 3. Testing and Quality Assurance

### 3.1 Unit, Integration, and Golden Tests

**Unit tests**
Must exist for every function or class that contains logic. Use deterministic tests that do not depend on external services.

**Golden tests**
Should lock the behavior of deterministic pipelines, especially adjudication or enforcement logic. Avoid updating golden outputs without deliberate review.

**Integration tests**
Should validate end-to-end scenarios, including interactions with critical system components.

### 3.2 Code Coverage

1520ai builds systems for regulated, audit-sensitive environments. Coverage expectations:

| Component Type | Target Coverage |
| -------------- | --------------- |
| Core business logic | ≥90% |
| Security-sensitive components | ≥90% |
| Data access layers | ≥80% |
| UI components | 60–70% |

Focus on meaningful tests—do not write tests merely to boost numbers.

### 3.3 Continuous Integration (CI)

**Pre-commit hooks**
Use repository-provided pre-commit configuration to run linters, formatters, and security scans before commits are created.

**CI pipelines**
All PRs must pass automated tests, linting, coverage thresholds, and security scans. Coverage drops below configured thresholds must be justified in the PR description.

**Branch protection**
Enable status checks for main and dev branches so merges cannot occur without successful CI and code review.

---

## 4. Security and Privacy

1520ai operates in HIPAA-regulated environments and handles sensitive health information. Security controls are protective and must never override regulatory authority.

### 4.1 Encryption & Storage

**Encrypt all PHI**
Use strong algorithms such as AES-256 for storage and TLS 1.2+ for network transport. Do not store encryption keys in source code; use a dedicated key management service.

**Avoid real PHI in dev/test**
Use synthetic or properly de-identified data for development and testing. If production data is absolutely necessary, require documented approval, isolate its use, and securely delete it after debugging.

**Secure backups**
Encrypt database dumps and backups and treat them with the same controls as production data. Follow secure destruction procedures when decommissioning storage media.

### 4.2 Access Control & Authentication

**Unique identities and MFA**
Assign unique user IDs for every engineer, reviewer, and administrator and enforce multi-factor authentication on all systems handling PHI. Shared accounts are prohibited.

**Principle of least privilege**
Implement role-based access control (RBAC) so users can access only the minimum PHI necessary. Short session timeouts and secure cookie settings (HttpOnly, Secure) are required.

### 4.3 API & Integration Security

**No PHI in URLs**
Never include PHI in URLs or query parameters; use POST requests with body payloads and opaque identifiers.

**Authenticated endpoints**
Require OAuth 2.0, API keys with scoped permissions, or similar authentication mechanisms for all endpoints that handle PHI. Enforce authorization on the server for every request.

**Vendor vetting**
Third-party integrations that might touch PHI must sign a Business Associate Agreement and demonstrate HIPAA compliance.

### 4.4 Logging & Monitoring

**Audit logs**
Record who accessed a record and when, not the medical content itself. Treat logs as sensitive data and retain them for at least six years or as required by law.

**Anomaly detection**
Monitor for unusual patterns (bulk downloads, off-hours access, cross-department record viewing) and set alerts.

**Sensitive logging**
Do not send PHI to external logging or error services. Mask or hash sensitive values before logs leave your control.

### 4.5 Development Practices for PHI

**De-identify early**
Incorporate de-identification at the start of data pipelines and use synthetic datasets for testing.

**Sanitize free text**
Apply NLP redaction or exclude free-text fields that might contain hidden identifiers.

**Incident readiness**
Build features to quickly revoke API keys, deactivate accounts, and generate audit reports. The ability to answer "who accessed what and when" must be real-time.

**Avoid metadata leaks**
Strip EXIF data from images, sanitize file names, and set `Cache-Control: no-store` on PHI responses.

**Client-side security**
Ensure mobile/web apps encrypt data at rest and clear sensitive data from memory; avoid local storage for PHI.

**Remove debug endpoints**
Ensure test backdoors and dump routes are never deployed to production.

### 4.6 PHI Detection and Incident Handling

Repositories that process healthcare text SHOULD implement PHI detection controls (e.g., NER- or rules-based tripwires) as pre-commit and CI steps.

**True positives**
If a real-world identifier is detected, stop work, follow the incident response runbook, open a security ticket, and notify <security@1520.ai> immediately. PHI detection failures are potential HIPAA violations and must not be ignored.

**Bypass**
Only in documented emergencies may detection controls be bypassed; this requires approval and justification per [change-control.md](change-control.md).

---

## 5. Governance and Determinism

1520ai enforces a strict separation between regulatory authority and implementation. Governance documents define what systems are allowed to do; code and models implement those rules but cannot override them.

### Binding Invariants (Engineering Implications)

**Documentation over code**
If implementation conflicts with documentation, documentation wins. Update documents first.

**No silent overrides**
Governance controls and enforcement gates cannot be bypassed or overridden programmatically. Probabilistic models may assist but never enforce decisions.

**Deterministic outputs**
Systems must produce identical outputs for identical inputs. Avoid:

- Time-based randomness
- Nondeterministic ordering
- Unbounded concurrency
- External calls that return different values on each run

Where nondeterminism is unavoidable (e.g., random seeds), surface it as part of the API and record it for audit.

**Human-in-the-loop escalation**
Hard stops always require human review. Clear escalation paths must be defined in product documentation.

**Monitoring is observational**
Monitoring tools detect anomalies but never modify decisions. Their role is to inform, not enforce.

---

## 6. Model and AI Usage

**Assistive role only**
Models may generate explanations, suggest relevant evidence, and flag patterns, but they must never enforce regulatory decisions or assign outcomes autonomously.

**No training on production data**
Models must not learn from PHI or production data without explicit review and approval. Training must use synthetic or de-identified datasets.

**Deterministic execution**
For models used in enforcement paths, fix random seeds and ensure stable outputs across runs. For generative models, record prompts and outputs for audit.

**Prompt safety**
Validate all model inputs against schemas, escape untrusted user inputs to prevent injection, and maintain a prompt log.

**Avoid the lethal trifecta**
Per [SECURITY.md](../SECURITY.md), systems must not combine:

- Untrusted input
- Access to sensitive data
- Ability to take external action

---

## 7. Documentation and Knowledge Management

**Source of truth**
The `docs/` directory contains authoritative documentation. Always update relevant docs when introducing new features, gates, signals, or authority flows.

**Runbooks**
Operations, incident response, and contributor validation procedures must be documented and followed precisely.

**API reference and schemas**
Keep data models and schemas up-to-date and reflect any contract changes in API documentation. Contracts are canonical—clients should not infer structure from implementation details.

**Incident learning**
Log all incidents and near misses and write human-readable summaries. The goal is continuous improvement.

---

## 8. Professional Conduct

**Inclusive culture**
Foster a respectful, collaborative environment. Code reviews, comments, and communications should assume positive intent and avoid personal attacks.

**Mentorship**
Senior engineers should actively mentor junior colleagues, encourage questions, and share domain knowledge. Involving junior reviewers improves quality and builds future expertise.

**Bias mitigation**
When working with NLP or ML models, be aware of potential biases. Evaluate model outputs across diverse demographic groups and report any disparities through the responsible-AI governance channel.

---

## 9. Continuous Improvement

Engineering standards are living documents. Propose updates through PRs following the change-control process with appropriate classification (Policy Change, Control Tightening, Clarification).

Regularly review emerging best practices, regulatory updates, and internal post-mortems to refine these standards.

---

## Enforcement

These standards are enforced through:

- Code review requirements
- CI/CD checks
- CODEOWNERS approval
- Audit and incident review

**Failure to follow engineering standards in security-critical or governance-affecting areas is treated as a system risk, not a stylistic preference.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.

---

## Final Note

Adhering to these standards helps ensure that 1520ai systems remain deterministic, secure, and auditable. When in doubt, err on the side of safety, transparency, and governance discipline.
