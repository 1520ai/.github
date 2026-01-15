# 1520ai — AI Security & LLM Threat Defense

**Status:** Active
**Effective Date:** 2026-01-15
**Scope:** All AI and LLM-enabled systems
**Audience:** AI/ML engineers, security, architecture reviewers

---

## 1. Purpose

This document defines security requirements specific to AI systems, with emphasis on Large Language Model (LLM) threats and defenses.

AI security ensures that:

- AI systems resist adversarial manipulation
- Prompt injection attacks are prevented
- Model outputs are validated before use
- Sensitive data is not leaked through model behavior
- AI systems maintain integrity under attack

**AI systems are attack surfaces. Security is not optional.**

---

## 2. Relationship to Governance

This document operates under the authority of:

- [docs/governance.md](governance.md) — Authority hierarchy and binding invariants
- [docs/responsible-ai.md](responsible-ai.md) — AI posture and constraints
- [SECURITY.md](../SECURITY.md) — Security reporting and incident handling
- [docs/ai-release-gates.md](ai-release-gates.md) — Pre-deployment validation

AI security incidents follow the escalation path in [incident-response.md](incident-response.md).

---

## 3. Threat Model

### 3.1 AI-Specific Threats

| Threat | Description | Impact |
| ------ | ----------- | ------ |
| **Prompt Injection** | Malicious input that hijacks model behavior | Unauthorized actions, data leakage |
| **Jailbreaking** | Bypassing model safety constraints | Harmful outputs, policy violations |
| **Data Extraction** | Extracting training data or sensitive information | Privacy breach, IP theft |
| **Model Manipulation** | Causing incorrect or biased outputs | Wrong decisions, safety risks |
| **Denial of Service** | Overwhelming model resources | Service unavailability |
| **Supply Chain** | Compromised models or dependencies | Backdoors, malicious behavior |

### 3.2 The Lethal Trifecta

Systems MUST NOT combine all three of:

1. **Untrusted input** — User-provided or external data
2. **Access to sensitive data** — PHI, credentials, internal systems
3. **Ability to take action** — Execute code, call APIs, modify data

If all three are present, the system is vulnerable to prompt injection leading to data exfiltration or unauthorized actions.

**Mitigation:** Isolate capabilities. Systems with untrusted input should not have direct access to sensitive data AND action capabilities simultaneously.

---

## 4. Input Security

### 4.1 Input Validation

All AI system inputs MUST be validated:

| Validation | Requirement |
| ---------- | ----------- |
| Schema validation | Inputs conform to expected structure |
| Length limits | Maximum input length enforced |
| Character filtering | Dangerous characters escaped or rejected |
| Content filtering | Known attack patterns detected |

### 4.2 Prompt Injection Prevention

**Direct Injection Prevention:**

| Control | Description |
| ------- | ----------- |
| Input/instruction separation | User input clearly separated from system instructions |
| Delimiter enforcement | Strong delimiters between instruction and data |
| Input sanitization | User input escaped before inclusion in prompts |
| Instruction anchoring | System instructions reinforced after user input |

**Indirect Injection Prevention:**

| Control | Description |
| ------- | ----------- |
| Content inspection | External content scanned before processing |
| Source validation | Only trusted sources for retrieved content |
| Sandboxing | External content processed in isolation |
| Output filtering | Results validated before use |

### 4.3 Input Logging

All inputs to AI systems SHOULD be logged:

| Field | Description |
| ----- | ----------- |
| Timestamp | When input received |
| Source | Where input came from |
| Input hash | Hash of input (not full content for PHI) |
| Session ID | Correlation identifier |
| User ID | If authenticated |

**PHI Consideration:** Do not log full PHI content. Log metadata and hashes for traceability.

---

## 5. Output Security

### 5.1 Output Validation

All AI outputs MUST be validated before use:

| Validation | Requirement |
| ---------- | ----------- |
| Schema conformance | Output matches expected format |
| Content filtering | Harmful content detected and blocked |
| Confidence thresholds | Low-confidence outputs flagged or rejected |
| Consistency checks | Output consistent with input context |

### 5.2 Output Sanitization

Before outputs are displayed or used:

| Control | Description |
| ------- | ----------- |
| HTML escaping | Prevent XSS if displayed in web context |
| Command escaping | Prevent injection if used in commands |
| Format validation | Ensure output is well-formed |
| PII scanning | Detect inadvertent PII in outputs |

### 5.3 Output Filtering

Outputs MUST be filtered for:

| Content Type | Action |
| ------------ | ------ |
| PHI leakage | Block and log |
| Credential exposure | Block and alert |
| Harmful content | Block and log |
| Policy violations | Block and log |
| Instruction leakage | Block (system prompt exposure) |

### 5.4 Output Logging

All outputs from AI systems SHOULD be logged:

| Field | Description |
| ----- | ----------- |
| Timestamp | When output generated |
| Request ID | Correlation to input |
| Output hash | Hash of output |
| Model version | Which model produced output |
| Confidence | Model confidence if available |
| Filtered | Whether output was filtered |

---

## 6. Prompt Security

### 6.1 System Prompt Protection

System prompts (instructions to the model) MUST be protected:

| Control | Description |
| ------- | ----------- |
| Confidentiality | System prompts not exposed to users |
| Integrity | System prompts not modifiable by input |
| Extraction prevention | Refuse requests to reveal system prompt |
| Version control | System prompts versioned and auditable |

### 6.2 Prompt Design Principles

| Principle | Description |
| --------- | ----------- |
| Least privilege | Prompt grants minimum necessary capabilities |
| Defense in depth | Multiple layers of instruction |
| Explicit boundaries | Clear statement of what model should not do |
| Fail secure | Ambiguous situations result in refusal |

### 6.3 Prompt Template Security

When using prompt templates:

| Control | Description |
| ------- | ----------- |
| Parameterization | User input inserted via parameters, not concatenation |
| Escaping | Special characters in parameters escaped |
| Validation | Parameters validated before insertion |
| Testing | Templates tested with adversarial inputs |

---

## 7. Model Security

### 7.1 Model Integrity

| Control | Description |
| ------- | ----------- |
| Checksum verification | Model files verified before loading |
| Signed models | Models cryptographically signed |
| Secure storage | Models stored with access controls |
| Version tracking | Model versions tracked in registry |

### 7.2 Model Isolation

| Control | Description |
| ------- | ----------- |
| Sandboxed execution | Models run in isolated environments |
| Resource limits | CPU, memory, and time limits enforced |
| Network isolation | Models cannot make arbitrary network calls |
| File system isolation | Models cannot access arbitrary files |

### 7.3 Model Supply Chain

| Control | Description |
| ------- | ----------- |
| Source verification | Models from trusted sources only |
| Dependency scanning | Model dependencies scanned for vulnerabilities |
| License compliance | Model licenses reviewed and compliant |
| Update process | Secure process for model updates |

---

## 8. Data Protection in AI

### 8.1 Training Data Security

| Control | Description |
| ------- | ----------- |
| Data minimization | Only necessary data used for training |
| PHI exclusion | PHI not used in training without explicit approval |
| De-identification | Training data de-identified where possible |
| Access control | Training data access restricted |
| Lineage tracking | Training data sources documented |

### 8.2 Inference Data Security

| Control | Description |
| ------- | ----------- |
| Data in transit | Encrypted connections to model endpoints |
| Data at rest | Inference logs encrypted |
| Data retention | Inference data retained per policy |
| Access logging | Access to inference data logged |

### 8.3 Memorization Prevention

Models MUST be evaluated for memorization risks:

| Control | Description |
| ------- | ----------- |
| Memorization testing | Test for verbatim training data extraction |
| Differential privacy | Consider DP techniques for sensitive training |
| Output filtering | Filter outputs matching sensitive patterns |
| Monitoring | Monitor for anomalous output patterns |

---

## 9. Authentication & Authorization

### 9.1 API Security

| Control | Description |
| ------- | ----------- |
| Authentication | All AI endpoints require authentication |
| Authorization | Role-based access to AI capabilities |
| Rate limiting | Request rate limits per user/API key |
| Quota management | Usage quotas enforced |

### 9.2 Capability-Based Access

| Capability | Authorization Level |
| ---------- | ------------------- |
| Read-only queries | Standard user |
| Data modification | Elevated permissions |
| System configuration | Administrator only |
| Model management | AI Engineering only |

---

## 10. Monitoring & Detection

### 10.1 Security Monitoring

| Monitor | Purpose |
| ------- | ------- |
| Input anomaly detection | Detect unusual input patterns |
| Output anomaly detection | Detect unusual output patterns |
| Rate monitoring | Detect abuse patterns |
| Error monitoring | Detect exploitation attempts |

### 10.2 Attack Detection

| Attack Pattern | Detection Method |
| -------------- | ---------------- |
| Prompt injection | Pattern matching, semantic analysis |
| Jailbreak attempts | Known pattern detection, output analysis |
| Data extraction | Output scanning, query pattern analysis |
| Enumeration | Rate analysis, query diversity analysis |

### 10.3 Alerting

| Severity | Alert Mechanism | Response Time |
| -------- | --------------- | ------------- |
| Critical | Page on-call | Immediate |
| High | Alert channel | 1 hour |
| Medium | Ticket creation | 1 business day |
| Low | Log for review | Weekly review |

---

## 11. Testing Requirements

### 11.1 Security Testing

AI systems MUST undergo security testing:

| Test Type | Frequency | Scope |
| --------- | --------- | ----- |
| Prompt injection testing | Pre-release, major changes | All input vectors |
| Jailbreak testing | Pre-release, major changes | Safety constraints |
| Output validation testing | Pre-release | All output types |
| Penetration testing | Annual | Full system |

### 11.2 Adversarial Testing

| Test | Description |
| ---- | ----------- |
| Red team exercises | Dedicated team attempts to bypass controls |
| Automated fuzzing | Automated generation of adversarial inputs |
| Known attack patterns | Testing against published attack techniques |
| Edge case testing | Testing boundary conditions and unusual inputs |

### 11.3 Test Documentation

All security tests MUST be documented:

| Field | Description |
| ----- | ----------- |
| Test ID | Unique identifier |
| Test type | Category of test |
| Date | When test conducted |
| Tester | Who conducted test |
| Findings | Issues discovered |
| Remediation | How issues were addressed |
| Retest | Verification of fixes |

---

## 12. Incident Response

### 12.1 AI-Specific Incidents

| Incident Type | Severity | Response |
| ------------- | -------- | -------- |
| Successful prompt injection | High | Immediate containment, investigation |
| Data leakage via model | Critical | Immediate containment, breach assessment |
| Jailbreak bypass | Medium | Patch and redeploy |
| Model compromise | Critical | Take offline, forensic analysis |

### 12.2 Containment Actions

| Action | When to Use |
| ------ | ----------- |
| Rate limit reduction | Suspected abuse |
| Input filtering enhancement | Active attack |
| Output filtering enhancement | Data leakage risk |
| Service suspension | Critical compromise |
| Model rollback | Compromised model |

### 12.3 Post-Incident

After AI security incidents:

1. Conduct root cause analysis
2. Update threat model
3. Enhance controls
4. Update testing suite
5. Document lessons learned

---

## 13. Compliance

### 13.1 AI Security Checklist

Pre-deployment checklist:

- [ ] Input validation implemented
- [ ] Output validation implemented
- [ ] Prompt injection testing completed
- [ ] Jailbreak testing completed
- [ ] System prompt protected
- [ ] Logging configured
- [ ] Monitoring configured
- [ ] Rate limiting configured
- [ ] Authentication required
- [ ] Authorization implemented

### 13.2 Ongoing Compliance

| Activity | Frequency |
| -------- | --------- |
| Security testing | Pre-release |
| Penetration testing | Annual |
| Control review | Quarterly |
| Threat model update | Annual or after incidents |

---

## 14. Exceptions

Exceptions to AI security requirements:

- MUST be documented in [docs/exceptions.md](exceptions.md)
- MUST include compensating controls
- MUST be time-bounded
- MUST be approved by Security and AI Engineering leadership

Research and experimentation environments MAY have reduced requirements but MUST NOT process production data or PHI.

---

## 15. Enforcement

AI security requirements are enforced through:

- Code review requirements
- Security testing gates
- Release approval process
- Incident review

**Deploying AI systems without security review is a governance violation.**

---

## Status

This document is **active and binding**.

All material changes follow change control and are recorded in `CHANGELOG.md`.
