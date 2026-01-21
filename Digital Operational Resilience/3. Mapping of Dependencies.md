# Mapping of Dependencies – Crypto Trading Execution & Digital Asset Custody

## 1. Purpose

This document maps the **key dependencies** supporting the organisation’s two most critical Important Business Services:
- Crypto Trading Execution
- Digital Asset Custody

The objective is to demonstrate how dependency mapping is used to support operational resilience in a **practical and proportionate way**, aligned with the organisation’s size and complexity.

This artefact intentionally focuses on a limited subset of services to provide sufficient depth and clarity.

---

## 2. Scope and Approach

### In Scope
- Crypto Trading Execution
- Digital Asset Custody

### Out of Scope
- Fiat services
- Wallet-to-wallet transfers
- Ancillary customer services

Dependencies are mapped at a level sufficient to:
- Identify material risks
- Support incident response
- Enable realistic resilience testing

Non-material or low-impact dependencies are excluded to maintain clarity.

---

## 3. Dependency Categories

Dependencies are grouped into the following categories:
- Business functions
- Applications and platforms
- Infrastructure and cloud services
- Data and backups
- Third-party providers
- Key operational roles

---

## 4. Dependency Mapping by Important Business Service

### 4.1 Crypto Trading Execution

**Service Description**  
Execution of customer buy and sell orders across supported crypto assets through web, mobile, and API channels.

---

#### Business Functions
- Trading operations
- Incident management and on-call support
- Customer communications

---

#### Applications and Platforms
- Trading engine
- Order management system
- Market data services
- API gateway
- Customer-facing web and mobile applications

---

#### Infrastructure and Cloud Services
- Primary cloud region
- Load balancing and network connectivity
- Compute and container orchestration services

---

#### Data and Backups
- Order and trade databases
- Configuration repositories
- Automated backups and replication mechanisms

---

#### Third-Party Providers
- Cloud service provider
- Market data providers
- Monitoring and alerting platforms

---

#### Key Operational Roles
- Engineering on-call
- Security and incident response
- Operations support

---

### 4.2 Digital Asset Custody

**Service Description**  
Secure storage and safeguarding of customer digital assets, including wallet infrastructure and key management processes.

---

#### Business Functions
- Asset operations
- Security monitoring
- Key management procedures

---

#### Applications and Platforms
- Wallet management platform
- Key management systems (e.g. HSM or equivalent)
- Blockchain node services

---

#### Infrastructure and Cloud Services
- Secure compute environments
- Segmented network architecture
- Cold and warm storage environments

---

#### Data and Backups
- Wallet configuration data
- Key material backups (where applicable)
- Audit and access logs

---

#### Third-Party Providers
- Wallet technology vendors
- Cloud infrastructure provider
- Blockchain infrastructure services

---

#### Key Operational Roles
- Security operations
- Asset operations
- Authorised key custodians

---

## 5. Cross-Service Dependencies and Key Risks

The following dependencies are shared across both services and represent areas of heightened risk:

- Cloud infrastructure provider
- Identity and access management systems
- Monitoring and alerting platforms
- On-call engineering and security roles

Shared dependencies are reviewed to:
- Identify single points of failure
- Understand concentration risk
- Inform resilience testing scenarios

---

## 6. How This Mapping Is Used

This dependency mapping is used to:
- Prioritise actions during incidents
- Support scenario-based resilience testing
- Assess the impact of changes to systems or vendors
- Inform BCP and DR planning for critical components

---

## 7. Review and Maintenance

This document is reviewed:
- Periodically as systems evolve
- Following material incidents or test outcomes
- When significant changes are made to in-scope services

Updates are kept concise to ensure the mapping remains usable during real incidents.

---

## 8. Summary

By focusing on the two most critical services, this dependency mapping provides a clear and practical view of how operational resilience is supported without unnecessary complexity.
This approach ensures that resilience efforts remain targeted, effective, and scalable.
