# Important Business Services and Impact Tolerances

## 1. Purpose

This document identifies the organisation’s **Important Business Services (IBS)** and defines the **impact tolerances** for each service.

The objective is to ensure that, in the event of an ICT-related disruption, the organisation can:
- Prioritise response and recovery activities
- Limit customer harm and market impact
- Make informed trade-offs during incidents
- Align BCP/DR capabilities with business needs

This document supports the Operational Resilience Framework and informs dependency mapping, testing, and recovery planning.

---

## 2. Definition of Important Business Services

An Important Business Service is a service delivered to external users where disruption could result in one or more of the following:
- Material customer detriment
- Financial loss to customers or the business
- Loss of market confidence
- Regulatory or legal impact
- Significant reputational damage

IBS are defined based on **customer outcomes**, not internal systems or organisational structure.

---

## 3. Criteria for Identifying IBS

Services were assessed against the following criteria:

- **Customer Impact**  
  Number of customers affected and severity of harm

- **Financial Impact**  
  Direct or indirect financial loss

- **Market Integrity**  
  Risk of disorderly markets or loss of trust

- **Regulatory Impact**  
  Breach of legal or regulatory obligations

- **Reputational Impact**  
  Impact on brand and customer confidence

Services meeting one or more of these criteria are classified as Important Business Services.

---

## 4. List of Important Business Services

Based on the assessment, the following services are classified as Important Business Services:

1. Crypto Trading Execution  
2. Digital Asset Custody  
3. Fiat Deposits and Withdrawals  
4. Wallet Transfers  

These services represent the core value delivered to customers and the areas where disruption would have the greatest impact.

---

## 5. Impact Tolerances – Overview

Impact tolerances define the **maximum acceptable level of disruption** for each IBS.

They are expressed across multiple dimensions:
- Maximum tolerable disruption duration
- Data integrity and confidentiality expectations
- Service degradation thresholds
- Customer and regulatory impact considerations

Impact tolerances are **business-driven** and are not equivalent to system-level RTOs or RPOs.  
They are used to guide recovery objectives, incident prioritisation, and resilience testing.

---

## 6. Impact Tolerances by Important Business Service

### 6.1 Crypto Trading Execution

**Service Description**  
Execution of customer buy and sell orders for supported crypto assets through web, mobile, and API channels.

**Impact Considerations**
- High customer visibility
- Financial exposure during volatile markets
- Market confidence risk

**Impact Tolerances**
- Maximum tolerable disruption duration: **Up to 60 minutes**
- Data integrity: **No loss or corruption of executed trades**
- Degraded mode: **Read-only or order placement disabled acceptable for limited periods**
- Customer impact threshold: **Customer communications required if disruption exceeds tolerance**

---

### 6.2 Digital Asset Custody

**Service Description**  
Secure storage and safeguarding of customer digital assets, including key management and wallet infrastructure.

**Impact Considerations**
- Customer asset safety
- Regulatory and legal exposure
- Trust and reputational risk

**Impact Tolerances**
- Maximum tolerable disruption duration: **Availability degradation acceptable if assets remain secure**
- Data integrity: **Zero tolerance for loss, corruption, or unauthorised access**
- Degraded mode: **Restricted access acceptable if security is maintained**
- Customer impact threshold: **Immediate escalation for any integrity or security concern**

---

### 6.3 Fiat Deposits and Withdrawals

**Service Description**  
Processing of customer fiat deposits and withdrawals through integrated banking and payment providers.

**Impact Considerations**
- Customer liquidity and access to funds
- Dependency on third-party providers
- Regulatory and complaints risk

**Impact Tolerances**
- Maximum tolerable disruption duration: **Up to 4 hours**
- Data integrity: **No loss or duplication of transaction records**
- Degraded mode: **Delayed processing acceptable with customer notification**
- Customer impact threshold: **Escalation required for prolonged or repeated delays**

---

### 6.4 Wallet Transfers

**Service Description**  
On-chain transfers of digital assets between internal and external wallets.

**Impact Considerations**
- Customer access to funds
- Blockchain dependency
- Fraud and error risk

**Impact Tolerances**
- Maximum tolerable disruption duration: **Up to 2 hours**
- Data integrity: **No incorrect or unauthorised transfers**
- Degraded mode: **Outbound transfers paused acceptable if inbound tracking continues**
- Customer impact threshold: **Clear communication required during extended disruption**

---

## 7. Relationship to BCP and DR

Impact tolerances defined in this document:
- Inform recovery prioritisation during incidents
- Guide the setting of RTOs and RPOs for supporting systems
- Determine acceptable degraded service modes
- Influence the design and testing of BCP and DR plans

BCP and DR capabilities are assessed against their ability to restore services **within these impact tolerances**.

---

## 8. Review and Maintenance

This document is reviewed:
- At least annually
- Following material incidents affecting IBS
- When introducing new products or services
- In response to regulatory or risk profile changes

Updates are approved by senior management to ensure continued alignment with business priorities and risk appetite.

---

## 9. Summary

By clearly identifying Important Business Services and defining impact tolerances, the organisation establishes a practical foundation for Operational Resilience.

This approach ensures that recovery efforts, resilience testing, and risk management activities are focused on protecting customers and maintaining trust in the most critical services.
