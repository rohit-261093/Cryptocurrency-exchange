# Risk and Impact Analysis  
Crypto Exchange Platform (AWS Environment)

This document presents the Business Impact Analysis (BIA) and Risk Assessment
for a centralized cryptocurrency exchange deployed on Amazon Web Services (AWS).

The objective is to identify critical business services, assess the impact of
disruption, and understand AWS-specific risks that could affect platform
availability, integrity, and operations.

---

## 1. Scope

This analysis applies to the following platform capabilities:
- User authentication and access
- Spot trading (order book-based trading)
- Wallet management and internal settlement
- Deposits and withdrawals via blockchain networks
- Market data delivery
- OTC and C2C trading services

The platform is assumed to be hosted entirely within AWS, using a combination
of managed and self-managed services.

---

## 2. Business Impact Analysis (BIA)

### 2.1 Critical Business Services

| Service | Description |
|------|------------|
| User Authentication | Login, session management, API access |
| Spot Trading | Order placement, order matching, trade execution |
| Wallet Service | Balance management, fund locking, settlement |
| Deposits & Withdrawals | Blockchain interaction for asset movement |
| Market Data | Price feeds, order book updates |
| OTC / C2C Trading | Off-order-book and peer-to-peer trading |

---

### 2.2 Impact Dimensions

Impact is assessed across the following dimensions:
- **Financial** – lost revenue, compensation, liquidity risk
- **Regulatory / Legal** – custody obligations, compliance exposure
- **Reputational** – loss of user trust
- **Operational** – backlog, manual remediation effort

---

### 2.3 Business Impact Summary

| Business Service | Maximum Tolerable Disruption | RTO | RPO | Impact Summary |
|-----------------|-----------------------------|-----|-----|----------------|
| Wallet Service | Minutes | ≤ 1 min | 0 | Asset safety and regulatory risk |
| Spot Trading | Minutes | ≤ 30 sec | 0 | Revenue and market trust |
| Deposits / Withdrawals | Hours | ≤ 30 min | N/A | User dissatisfaction |
| User Authentication | Minutes | ≤ 5 min | N/A | Platform access blocked |
| Market Data | Minutes | ≤ 1 min | N/A | Trading usability impact |
| OTC / C2C Trading | Hours | ≤ 1 hour | N/A | Limited user impact |

**Key observation:**  
Wallet integrity has a higher business impact than trading availability.

---

## 3. Risk Assessment (AWS-Focused)

### 3.1 AWS Threat Categories

#### Infrastructure Risks
- Availability Zone (AZ) outage
- Compute node failure (EC2 / EKS)
- Storage failure (EBS)

#### Managed Service Risks
- Amazon RDS failover or replication issues
- ElastiCache (Redis) cluster failure
- Amazon MSK (Kafka) broker degradation
- AWS service quota exhaustion

#### Identity and Access Risks
- IAM misconfiguration
- Compromised credentials
- Excessive permissions
- Lack of separation of duties

#### Network Risks
- VPC routing misconfiguration
- Security group or NACL errors
- DNS (Route 53) resolution issues

#### Third-Party Dependency Risks
- Blockchain RPC provider outages
- External KYC/AML service downtime
- Market data provider failure

---

### 3.2 Risk Register (Sample)

| Risk | Affected Services | Likelihood | Impact | Risk Rating |
|----|------------------|------------|--------|-------------|
| AWS AZ outage | Trading, Wallet | Medium | High | High |
| RDS primary failure | Wallet, Ledger | Low | Critical | High |
| Redis cluster failure | Matchmaking | Medium | High | High |
| Kafka broker failure | Settlement | Medium | High | High |
| IAM misconfiguration | All services | Medium | Critical | Very High |
| RPC provider outage | Deposits/Withdrawals | High | Medium | High |

---

## 4. Mapping Business Impact to Risks

| Critical Service | Primary AWS-Related Risks |
|----------------|---------------------------|
| Wallet Service | RDS failure, IAM compromise, AZ outage |
| Spot Trading | Redis failure, compute failure, network partition |
| Deposits / Withdrawals | RPC provider outage, blockchain node desync |
| User Authentication | Load balancer failure, IAM issues |
| Market Data | WebSocket service failure, Redis cache issues |

This mapping ensures that risk treatment efforts are focused on services
with the lowest tolerance for disruption.

---

## 5. AWS Shared Responsibility Context

The analysis considers AWS’s shared responsibility model:

| Layer | Responsibility |
|----|----------------|
| Physical data centers | AWS |
| Underlying infrastructure | AWS |
| Managed service availability | AWS |
| Configuration, IAM, data integrity | Platform |
| Application logic and controls | Platform |

Most high-impact risks originate from configuration, identity, or application
logic rather than physical infrastructure failure.

---

## 6. Conclusion

This Risk and Impact Analysis establishes:
- Clear service criticality and disruption tolerance
- Defensible RTO and RPO targets
- AWS-specific risk visibility
- A foundation for defining continuity, recovery, and security controls

Subsequent documents build upon this analysis to define recovery strategies
and operational response plans.
