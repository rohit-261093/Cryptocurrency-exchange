
# Privileged Access Management (PAM) Standard  
**AWS-Based Cryptocurrency Exchange Environment**

---

## 1. Purpose

This Privileged Access Management (PAM) Standard defines the minimum security requirements for the management, control, monitoring, and review of **privileged access** within an **AWS-hosted cryptocurrency exchange**.

The objectives are to:
- Minimise standing privileged access
- Reduce insider and credential misuse risk
- Protect high-impact systems (wallets, signing services, trading engines)
- Support regulatory and operational resilience requirements (DORA)

This standard aligns with:
- NIST Cybersecurity Framework (CSF) 2.0
- ISO/IEC 27001:2022
- AWS Well-Architected Framework – Security Pillar

---

## 2. Scope

This standard applies to:
- Privileged human users
- Administrative roles
- Cloud infrastructure administrators
- Service, system, and robotic accounts
- Third-party privileged access

Across:
- All AWS accounts and regions
- Production and non-production environments
- Systems supporting custody, trading, settlement, and monitoring

---

## 3. Control Framework Mapping

| Framework | Control Areas |
|---------|---------------|
| NIST CSF 2.0 | PR.AA – Identity & Access Control |
| ISO/IEC 27001:2022 | A.5.15 – A.5.19 |

---

## 4. Minimum Security Requirements (MSRs)

### 4.1 General Privileged Access Controls (PAM-01)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| PAM-01.1 | Privileged access MUST NOT be granted to standard business users | PR.AA-01 | A.5.15 | IAM role listings; role descriptions |
| PAM-01.2 | Privileged users MUST use separate privileged identities | PR.AA-01 | A.5.18 | Distinct IAM roles for admin vs user access |
| PAM-01.3 | Privileged identities MUST be unique and clearly identifiable | PR.AA-01 | A.5.16 | IAM role naming conventions; tagging |
| PAM-01.4 | Shared privileged accounts MUST NOT be used for human access | PR.AA-01 | A.5.18 | IAM policy reviews; absence of shared admin users |
| PAM-01.5 | Privileged access MUST be time-bound | PR.AA-01 | A.5.18 | IAM role session duration settings |
| PAM-01.6 | Just-in-Time (JIT) privileged access MUST be implemented where feasible | PR.AA-01 | A.5.18 | Temporary role assignment logs |
| PAM-01.7 | Privileged activity MUST be logged and monitored | PR.AA-01 | A.5.33 | CloudTrail logs; SIEM alerts |
| PAM-01.8 | A register of all privileged roles MUST be maintained | PR.AA-01 | A.5.18 | IAM inventory exports |

**Crypto-specific note:**  
Standing administrative access to wallet and signing infrastructure is prohibited.

---

### 4.2 Privileged Authentication & Session Control (PAM-02)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| PAM-02.1 | MFA MUST be enforced for all privileged access | PR.AA-03 | A.5.17 | IAM MFA enforcement conditions |
| PAM-02.2 | Privileged sessions MUST be time-limited | PR.AA-03 | A.5.18 | Role session duration configuration |
| PAM-02.3 | Privileged credentials MUST NOT be hard-coded | PR.AA-03 | A.8.24 | Secrets Manager usage; code scan results |
| PAM-02.4 | Privileged credentials MUST be stored in an approved secrets vault | PR.AA-03 | A.5.17 | AWS Secrets Manager configurations |
| PAM-02.5 | Root account usage MUST be restricted and monitored | PR.AA-03 | A.5.18 | Root usage alerts; SCPs |

---

### 4.3 Privileged Role & Segregation of Duties (PAM-03)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| PAM-03.1 | Segregation of duties MUST exist between access administration and system administration | PR.AA-05 | A.5.19 | Distinct IAM admin roles |
| PAM-03.2 | Users MUST NOT approve or provision their own privileged access | PR.AA-05 | A.5.18 | Approval workflows; SCPs |
| PAM-03.3 | Privileged roles MUST follow least-privilege principles | PR.AA-02 | A.5.15 | Access Analyzer findings |
| PAM-03.4 | Privileged access to production MUST require additional approval | PR.AA-05 | A.5.18 | Change management records |
| PAM-03.5 | Privileged roles MUST be environment-specific | PR.AA-05 | A.5.19 | Separate prod vs non-prod roles |

---

### 4.4 Service Account Privilege Management (PAM-04)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| PAM-04.1 | Service accounts MUST NOT allow interactive login | PR.AA-02 | A.5.16 | IAM roles without console access |
| PAM-04.2 | Service account use MUST be explicitly approved | PR.AA-01 | A.5.18 | Service account approval records |
| PAM-04.3 | Service accounts MUST have documented owners | PR.AA-01 | A.5.18 | IAM role tagging (`owner`) |
| PAM-04.4 | Service account credentials MUST be vaulted | PR.AA-02 | A.5.17 | Secrets Manager rotation logs |
| PAM-04.5 | Service account privileges MUST be restricted | PR.AA-02 | A.5.15 | IAM role policy reviews |
| PAM-04.6 | Service accounts MUST be decommissioned when no longer required | PR.AA-02 | A.5.18 | IAM deletion logs |

**Crypto-specific note:**  
Service accounts interacting with wallets or key material require security sign-off.

---

### 4.5 Robotic & Automation Account Controls (PAM-05)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| PAM-05.1 | Automation accounts MUST NOT allow interactive login | PR.AA-01 | A.5.16 | IAM role restrictions |
| PAM-05.2 | Automation accounts MUST have named owners | PR.AA-01 | A.5.18 | Role ownership metadata |
| PAM-05.3 | Automation secrets MUST be centrally managed | PR.AA-02 | A.5.17 | Secrets Manager entries |
| PAM-05.4 | Automation access MUST be limited to required APIs | PR.AA-04 | A.5.15 | IAM policy scope validation |
| PAM-05.5 | Inactive automation accounts MUST be reviewed | PR.AA-05 | A.5.18 | IAM access analyzer reports |

---

### 4.6 Privileged Access Review & Recertification (PAM-06)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| PAM-06.1 | Privileged access MUST be reviewed at least quarterly | PR.AA-05 | A.5.18 | Quarterly access review attestations |
| PAM-06.2 | Review outcomes MUST be documented | PR.AA-05 | A.5.18 | Signed review records |
| PAM-06.3 | Unnecessary privileged access MUST be revoked | PR.AA-05 | A.5.15 | IAM policy change logs |
| PAM-06.4 | Evidence MUST be retained for at least two years | PR.AA-05 | A.5.33 | S3 retention / object lock |

---

## 5. Logging & Monitoring

- All privileged activity MUST be logged via AWS CloudTrail
- Logs MUST be centrally stored and immutable
- Alerts MUST exist for:
  - Privilege escalation
  - Root account usage
  - IAM policy changes

**Evidence:**
- CloudTrail config
- SIEM alert rules
- Incident tickets

---

## 6. Compliance & Review

- This standard MUST be reviewed every 24 months
- Exceptions require documented risk acceptance
- Evidence MUST be available for audit and regulatory inspection

---

## 7. Summary

This PAM standard implements a zero-standing-privilege model aligned with AWS-native controls and crypto-asset risk management expectations, ensuring strong protection of highly sensitive systems and credentials.
``
