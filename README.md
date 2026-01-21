# Cryptocurrency Exchange – Security, Operational Resilience & Governance

## Overview

This repository demonstrates a **practical, regulator-aligned approach** to security, operational resilience, and ICT risk management for a **mid-sized cryptocurrency exchange**.

The content has been developed to:
- Align with **DORA and financial services regulatory expectations**
- Reflect **realistic operating constraints** (lean teams, cloud-native platforms)
- Focus on **outcomes, accountability, and proportionality**
- Serve as an **interview and capability demonstration artefact**

The repository does not represent a full production implementation. Instead, it focuses on the **governance, resilience, and security frameworks** that support critical exchange services.

---

## Scope of the Repository

The repository is deliberately scoped to the following **Important Business Services (IBS)**:

- **Crypto Trading Execution**
- **Digital Asset Custody**

All resilience, incident, governance, and security artefacts are designed around these two services to maintain relevance and clarity.

---

## Assumptions & Architecture Context

### Assumptions

The **Assumptions** folder documents the key assumptions underpinning all artefacts in this repository, including:

- A **cloud-native cryptocurrency exchange**
- Lean organisational structure with no standalone resilience or GRC teams
- Shared ownership of security, resilience, and risk across technology and leadership
- Material reliance on third-party ICT providers
- Proportionate governance aligned to organisational scale

These assumptions are stated explicitly to avoid over-engineering and unrealistic controls.

---

### Architecture

The **Assumptions** folder also contains the **high-level system architecture diagram**, which provides context for:

- Identification of Important Business Services
- Mapping of critical dependencies
- ICT and third-party risk identification
- Security and access control considerations
- Resilience and incident response scenarios

A supporting narrative is provided in:
- **High Level System Design.md**

The architecture is used as a **reference model**, not a prescriptive implementation.

---

## Repository Structure

The repository is organised by **control and governance domains**, rather than by technology layers.

---

### 📁 Assumptions (https://github.com/rohit-261093/Cryptocurrency-exchange/tree/23f36ec38b735a7a36bdf8b8b915a1fc6c1a2572/Assumptions)
- Key operating assumptions
- High-level architecture diagram
- System design overview

This folder provides the foundation for all other documents.

---

### 📁 BCP-DR
- Business Continuity and Disaster Recovery considerations
- **Incident Response & Post-Incident Review Framework**

Incident management is intentionally placed alongside BCP/DR to reinforce the link between:
- service disruption
- recovery
- learning and improvement

---

### 📁 Digital Operational Resilience
- Operational Resilience Framework
- Important Business Services & Impact Tolerances
- Mapping of Dependencies
- ICT Risks & Key Risk Indicators (KRIs)
- Digital Operational Resilience Testing
- **Third-Party ICT Risk Management**

This folder aligns closely with **DORA’s operational resilience lifecycle**, including third-party dependencies.

---

### 📁 Governance and Reporting
- ICT Governance & Oversight
- ICT Reporting, Audit & Regulatory Engagement

This folder provides a **single, coherent governance and reporting view**, covering:
- senior management and Board oversight
- regulatory reporting and engagement
- audit and evidence management

---

### 📁 Security and Access Control Management
- Security and Access Control Management framework

This folder focuses on **security governance and access control principles** that support the exchange architecture and critical services.

Security is described at a **policy and oversight level**, rather than technical configuration, to reflect the purpose of the repository.

---

## Security & Access Control – Intentional Scope

Security and access control content focuses on:
- Identity and access management principles
- Privileged access and segregation of duties
- Secure access to critical systems
- Integration with incident response and operational resilience
- Governance and oversight of security controls

Detailed technical implementations are intentionally out of scope.

---

## How to Read This Repository

The following reading order is recommended:

1. **Assumptions & Architecture**
2. **Business Continuity Management**(BCP-DR)
3. **Operational Resilience Framework** (Digital Operational Resilience)
4. **Important Business Services & Impact Tolerances** (Digital Operational Resilience)
5. **Incident Response & Post-Incident Review Framework** (BCP-DR)
6. **Governance & Reporting**
7. **Security and Access Control Management**

Supporting documents provide depth and regulatory context but are not required for an initial walkthrough.
