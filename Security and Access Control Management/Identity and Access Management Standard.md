
# Identity & Access Management (IAM) Standard  
**AWS-Based Cryptocurrency Exchange Environment**

---

## 1. Purpose

This Identity & Access Management (IAM) Standard defines the minimum security requirements for managing identities, authentication, authorisation, and access within an **AWS-hosted cryptocurrency exchange**.

The objectives of this standard are to:
- Enforce least-privilege access
- Apply strong authentication controls
- Protect crypto assets (wallets, private keys, trading engines)
- Support regulatory and operational resilience requirements (e.g. DORA, GDPR)

This standard aligns with:
- NIST Cybersecurity Framework (CSF) 2.0
- ISO/IEC 27001:2022
- AWS Well-Architected Framework – Security Pillar

---

## 2. Scope

This standard applies to:
- Employees, contractors, and third parties
- Privileged and non-privileged users
- Service, system, and application identities
- All AWS accounts, services, and environments supporting the cryptocurrency exchange

Including:
- Trading platforms
- Custody and wallet infrastructure
- APIs and customer-facing systems
- CI/CD pipelines and platform services

---

## 3. Control Framework Mapping

| Framework | Scope |
|---------|------|
| NIST CSF 2.0 | PR.AA – Identity & Access Control |
| ISO/IEC 27001:2022 | A.5.15 – A.5.19 |

---

## 4. Minimum Security Requirements (MSRs)

### 4.1 IAM Governance & Identity Management (IAM-01)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| IAM-01.1 | Access MUST be granted only to authorised users and systems with documented business justification | PR.AA-01 | A.5.15, A.5.18 | IAM Access Advisor reports; approved access tickets; IAM policy JSON |
| IAM-01.2 | Each user MUST have a unique, non-reusable identity | PR.AA-02 | A.5.16 | AWS IAM Identity Center user directory export |
| IAM-01.3 | All access requests MUST be logged and auditable | PR.AA-01 | A.5.18 | ServiceNow / Jira tickets mapped to IAM roles |
| IAM-01.4 | Credentials MUST NOT be shared | PR.AA-01 | A.5.17 | IAM policies preventing shared access keys |
| IAM-01.5 | Identities MUST be managed through a central identity platform | PR.AA-01 | A.5.16 | AWS IAM Identity Center configuration evidence |

**Crypto-specific note:**  
Shared credentials are strictly prohibited for wallet, signing, custody, and trading systems.

---

### 4.2 Authentication & Multi-Factor Authentication (IAM-02)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| IAM-02.1 | MFA MUST be enforced for all user access | PR.AA-03 | A.5.17 | MFA device assignments; Conditional Access policies |
| IAM-02.2 | MFA MUST be enforced for all privileged access | PR.AA-03 | A.5.17 | IAM policy conditions; SCPs enforcing MFA |
| IAM-02.3 | Authentication credentials MUST be encrypted in transit and at rest | PR.AA-03 | A.8.24 | TLS configs; AWS KMS usage |
| IAM-02.4 | Secrets MUST NOT be hard-coded | PR.AA-03 | A.8.24 | AWS Secrets Manager usage logs; code scans |
| IAM-02.5 | Single Sign-On SHOULD be used for internet-facing applications | PR.AA-03 | A.5.16 | AWS SSO / Cognito integration diagrams |

**Crypto-specific note:**  
MFA is mandatory for any system capable of initiating blockchain transactions or accessing private key material.

---

### 4.3 Privileged Access & Role Management (IAM-03)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| IAM-03.1 | Least-privilege access MUST be enforced at all times | PR.AA-02 | A.5.15 | IAM policy simulator results; Access Analyzer findings |
| IAM-03.2 | Users MUST NOT modify or approve their own access | PR.AA-05 | A.5.18 | SCPs preventing self-privilege escalation |
| IAM-03.3 | Segregation of duties MUST exist between system and access admins | PR.AA-05 | A.5.19 | Separate IAM admin roles |
| IAM-03.4 | Human access MUST be via time-bound role assumption, not static credentials | PR.AA-03 | A.5.17 | CloudTrail `AssumeRole` logs |

---

### 4.4 Joiner, Mover & Leaver (IAM-04)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| IAM-04.1 | Access MUST be provisioned based on approved joiner requests | PR.AA-01 | A.5.18 | HR-to-IAM provisioning logs |
| IAM-04.2 | Access MUST be reviewed promptly after role changes | PR.AA-01 | A.5.18 | Role change tickets |
| IAM-04.3 | Leaver accounts MUST be disabled immediately | PR.AA-01 | A.5.18 | AWS SSO deactivation timestamps |
| IAM-04.4 | All access MUST be removed within 24 hours of termination | PR.AA-01 | A.5.18 | IAM revocation logs |
| IAM-04.5 | Emergency termination MUST be supported | PR.AA-01 | A.5.18 | Emergency revocation runbooks |

**Crypto-specific note:**  
Rapid termination is critical to reduce insider trading or asset compromise risk.

---

### 4.5 Access Review & Recertification (IAM-05)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| IAM-05.1 | All user access MUST be reviewed at least annually | PR.AA-05 | A.5.18 | Access review attestations |
| IAM-05.2 | Privileged access SHOULD be reviewed quarterly | PR.AA-05 | A.5.18 | Privileged review reports |
| IAM-05.3 | Review outcomes MUST be documented | PR.AA-05 | A.5.18 | Signed review records |
| IAM-05.4 | Unnecessary access MUST be revoked | PR.AA-05 | A.5.15 | IAM policy diffs |
| IAM-05.5 | Evidence MUST be retained for at least two years | PR.AA-05 | A.5.33 | S3 retention policies |

---

### 4.6 Remote & Third-Party Access (IAM-06)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|-----------|------------|----------|-----------|-------------|
| IAM-06.1 | MFA MUST be enforced for all remote access | PR.AA-05 | A.5.17 | VPN / SSO MFA logs |
| IAM-06.2 | Third-party access MUST require valid contract and NDA | PR.AA-05 | A.5.19 | Vendor records |
| IAM-06.3 | Third-party access MUST be time-bound | PR.AA-05 | A.5.18 | IAM roles with expiration |
| IAM-06.4 | Third-party access MUST be revoked immediately when no longer required | PR.AA-05 | A.5.18 | CloudTrail revocation logs |

---

## 5. Logging & Monitoring

- All IAM activities MUST be logged via AWS CloudTrail
- Logs MUST be centrally stored, protected from deletion, and retained
- Alerts SHOULD exist for:
  - Privilege escalation
  - Root account usage
  - IAM policy changes

---

## 6. Compliance & Review

- This standard MUST be reviewed at least every 24 months
- Exceptions require documented risk acceptance
- Evidence MUST be available for audit and regulatory inspection

---

## 7. Summary

This IAM standard provides a control-to-evidence framework tailored for an AWS-native cryptocurrency exchange, supporting strong security, operational resilience, and regulatory compliance.
