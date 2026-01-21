# Digital Operational Resilience Testing

## 1. Purpose

This document describes how the organisation designs and conducts **Digital Operational Resilience Testing** to assess its ability to remain within defined impact tolerances during ICT-related disruptions.

The objective of testing is to:
- Validate assumptions made in dependency mapping
- Assess the organisation’s ability to withstand severe but plausible scenarios
- Identify weaknesses before real incidents occur
- Drive continuous improvement in operational resilience

Testing is scenario-driven and proportionate to the organisation’s size and risk profile.

---

## 2. Scope

### In Scope
- Crypto Trading Execution
- Digital Asset Custody

---

## 3. Testing Principles

Resilience testing is designed around the following principles:

- **Scenario-based**  
  Tests are based on realistic disruption scenarios rather than individual system failures.

- **Severe but plausible**  
  Scenarios reflect realistic threat conditions without assuming catastrophic failure.

- **Business-outcome focused**  
  Testing assesses impact on Important Business Services, not just technical recovery.

- **Proportionate**  
  Testing depth and frequency are aligned with organisational maturity and risk.

---

## 4. Types of Resilience Testing

The organisation uses a combination of the following testing approaches:

- Tabletop exercises
- Targeted failover or degradation testing
- Cyber incident simulations
- Third-party disruption scenarios
- Backup and recovery validation

Not all test types are applied uniformly; selection is risk-driven.

---

## 5. Scenario Design

Scenarios are designed based on:
- Identified ICT risks
- Dependency mapping
- Historical incidents and near misses
- Emerging threat intelligence

Each scenario includes:
- Scenario description and assumptions
- Impacted IBS
- Expected service behaviour
- Success criteria aligned to impact tolerances

---

## 6. Resilience Test Scenarios

### Scenario 1: Prolonged Cloud Infrastructure Outage During Peak Trading

**Description**  
Loss of availability in the primary cloud region affecting trading-related services during a period of high market volatility.

**Impacted IBS**
- Crypto Trading Execution

**Key Dependencies Tested**
- Cloud infrastructure
- Trading engine and order management system
- Market data services
- Incident response coordination

**Expected Behaviour**
- Trading enters a controlled degraded mode
- No loss or corruption of trade data
- Clear customer communication
- Recovery within defined impact tolerance

**Key Observations**
- Effectiveness of failover or degradation mechanisms
- Speed of incident detection and escalation
- Decision-making under time pressure

---

### Scenario 2: Market Data Feed Failure

**Description**  
Failure or degradation of external market data feeds leading to inaccurate or delayed pricing information.

**Impacted IBS**
- Crypto Trading Execution

**Key Dependencies Tested**
- Third-party market data providers
- Pricing validation controls
- Trading safeguards

**Expected Behaviour**
- Trading safeguards triggered
- Prevention of erroneous order execution
- Controlled suspension if required
- Prompt investigation and resolution

---

### Scenario 3: Wallet Management Platform Outage

**Description**  
Unavailability of the wallet management platform supporting digital asset custody.

**Impacted IBS**
- Digital Asset Custody

**Key Dependencies Tested**
- Wallet management platform
- Key management systems
- Security monitoring

**Expected Behaviour**
- Assets remain secure
- Access restrictions applied if required
- No unauthorised transactions
- Clear internal escalation and communication

---

## 7. Assessment Against Impact Tolerances

Each test is assessed against:
- Duration of service disruption
- Data integrity and security outcomes
- Customer impact
- Effectiveness of response and recovery

Where impact tolerances are breached or at risk, remediation actions are defined and tracked.

---

## 8. Documentation and Follow-Up

For each test, the following is documented:
- Scenario and assumptions
- Actions taken and timelines
- Outcomes and gaps identified
- Lessons learned
- Remediation actions and owners

Remediation actions are prioritised based on risk and customer impact.

---

## 9. Integration with BCP and Incident Management

Testing outcomes are used to:
- Validate BCP and DR assumptions
- Improve incident response playbooks
- Refine dependency mapping
- Adjust impact tolerances where necessary

This ensures resilience testing directly improves real-world response capability.

---
