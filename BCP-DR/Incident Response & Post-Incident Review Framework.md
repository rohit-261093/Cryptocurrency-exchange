# Incident Response & Post-Incident Review Framework

## 1. Purpose

This document defines the organisation’s approach to **incident response and post-incident reviews** for ICT-related incidents that may impact customer services, security, or regulatory obligations.

The objective is to ensure incidents are:
- Detected and assessed quickly
- Managed in a coordinated and proportionate manner
- Resolved within defined impact tolerances where possible
- Used as learning opportunities to strengthen operational resilience

This framework supports the Operational Resilience and ICT Risk Management artefacts.

---

## 2. Scope

### In Scope
- Security incidents
- Availability and performance incidents
- Data integrity incidents
- Third-party service disruptions
- Near-miss events with potential customer impact

### Out of Scope
- Non-ICT operational issues
- Minor service issues resolved within normal operations

---

## 3. Incident Definition

An incident is defined as:
> Any unplanned event that compromises, or has the potential to compromise, the confidentiality, integrity, or availability of systems supporting Important Business Services.

---

## 4. Incident Classification

Incidents are classified based on **impact**, not root cause.

### 4.1 Severity Levels

| Severity | Description |
|--------|-------------|
| **Sev 1 – Critical** | Major impact to Important Business Services, customer harm, or regulatory risk |
| **Sev 2 – High** | Partial service disruption or high-risk security event |
| **Sev 3 – Medium** | Limited impact or contained security issue |
| **Sev 4 – Low** | Minor issue with no material impact |

Severity may be escalated as new information becomes available.

---

## 5. Incident Detection and Reporting

Incidents may be detected through:
- System monitoring and alerts
- Security monitoring tools
- Third-party notifications
- Customer reports
- Internal staff escalation

All suspected incidents are logged and assessed promptly.

---

## 6. Incident Response Process

Incident response follows a structured but flexible lifecycle:

### 6.1 Identification and Triage
- Initial assessment of scope and impact
- Classification of incident severity
- Identification of impacted IBS

### 6.2 Containment and Mitigation
- Immediate actions to limit impact
- Activation of degraded service modes where appropriate
- Isolation of affected systems for security incidents

### 6.3 Communication and Escalation
- Internal escalation based on severity
- Coordination across engineering, security, and operations
- Customer communication where impact thresholds are met
- Regulatory notification considered where required

### 6.4 Resolution and Recovery
- Restoration of services
- Validation of data integrity and system stability
- Monitoring for recurrence

---

## 7. Roles and Responsibilities

Incident response is managed using **existing operational roles**, without reliance on a dedicated incident response team.

Key roles include:
- Incident Lead (typically engineering or security on-call)
- Technical responders
- Operations and customer support representatives
- Senior management for high-severity incidents

Clear ownership is assigned for each incident to ensure accountability.

---

## 8. Relationship to Operational Resilience

During incidents, defined **impact tolerances** are used to:
- Prioritise response actions
- Inform decisions on service degradation or suspension
- Determine escalation and communication thresholds

Where impact tolerances are at risk of being breached, senior management involvement is required.

---

## 9. Regulatory Notification and Reporting

Certain ICT-related incidents may trigger regulatory notification obligations.

Regulatory reporting is integrated into the incident response process and is based on:
- Incident severity
- Impact on Important Business Services
- Duration of disruption
- Data integrity or security implications
- Potential customer or market impact

### Notification Principles

- Regulatory notification is considered as part of incident triage for high-severity incidents
- Initial notifications may be made based on incomplete information and updated as investigations progress
- Reporting is coordinated to ensure accuracy, consistency, and appropriate senior management oversight

### Reporting Stages

Where required, regulatory reporting may include:
- Initial notification of a significant incident
- Follow-up updates as additional information becomes available
- A final report outlining root cause, impact, and remediation actions

Regulatory communications are documented as part of the incident record.


## 10. Post-Incident Review (PIR)

Post-incident reviews are conducted for:
- All Sev 1 incidents
- Significant Sev 2 incidents
- Repeated or systemic issues
- Near-miss events with high potential impact

The objective is learning, not blame.

---

## 11. Post-Incident Review Process

Each PIR includes:
- Incident summary and timeline
- Root cause analysis
- Assessment against impact tolerances
- Effectiveness of detection and response
- Customer and regulatory impact
- Actions taken during the incident
- Improvement actions and owners

Findings are documented and tracked to completion.

---

## 12. Integration with Risk and Resilience

Outcomes from PIRs are used to:
- Update ICT risk assessments
- Refine KRIs and thresholds
- Improve resilience testing scenarios
- Enhance BCP and incident playbooks
- Inform investment and prioritisation decisions

This ensures incidents directly contribute to continuous improvement.

---

## 13. Review and Maintenance

This framework is reviewed:
- Periodically as services evolve
- Following material incidents
- In response to regulatory or threat landscape changes

Updates are communicated to relevant teams to ensure continued effectiveness.

---

