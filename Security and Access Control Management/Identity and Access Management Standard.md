# Identity & Access Management (IAM) Standard  
**AWS-Based Cryptocurrency Exchange Environment**

---

## 1. Purpose

This Identity and Access Management (IAM) Standard defines the minimum security requirements for managing identities, authentication, authorization, and access within an **AWS-hosted cryptocurrency exchange** environment.

The objectives of this standard are to:
- Enforce least-privilege access
- Apply strong authentication controls
- Protect crypto assets (wallets, private keys, trading engines)
- Support regulatory compliance (DORA, GDPR)

This standard aligns with:
- NIST Cybersecurity Framework (CSF) 2.0
- ISO/IEC 27001:2022
- AWS Well-Architected Framework – Security Pillar

---

## 2. Scope

This standard applies to:
- Employees, contractors, and third parties
- Privileged and non-privileged users
- Service and application identities
- All AWS accounts and services supporting the cryptocurrency exchange

Including, but not limited to:
- Trading platforms
- Custody and wallet infrastructure
- APIs and customer-facing applications
- CI/CD pipelines and security tooling

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
