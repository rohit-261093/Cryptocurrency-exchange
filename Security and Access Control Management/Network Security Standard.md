
# Network Security Standard  
**AWS-Based Cryptocurrency Exchange Environment**

---

## 1. Purpose

This Network Security Standard defines the minimum security requirements to **design, segment, protect, monitor, and test** the exchange’s AWS network estate. It aims to prevent unauthorized access, minimize blast radius, and protect services that handle **trading**, **customer data**, and **wallet/signing functions**, while meeting regulatory and operational resilience obligations.

**Framework Alignment**
- **NIST CSF 2.0**: ID.AM, PR.AC/PR.AA (Access Control), PR.DS (Data Security), PR.PT (Protective Technology), DE.CM (Monitoring), RS.MI (Response & Mitigation)
- **ISO/IEC 27001:2022**: A.5.15 (Identity management), A.8.1–A.8.9 (Technical controls incl. network security, segmentation, configuration management), A.8.16 (Monitoring activities), A.5.30 (ICT readiness for business continuity)

---

## 2. Scope

This standard applies to:
- All **AWS accounts and regions** supporting the exchange
- Network constructs (VPCs, subnets, routing, gateways), **Security Groups (SGs)**, **Network ACLs (NACLs)**, **AWS Network Firewall/WAF**, **Route 53**, **CloudFront**, **API Gateway**, **ALB/NLB**, **EKS** and **ECS** networking, **VPC Lattice**, **PrivateLink**, **Transit Gateway**, **VPN/Direct Connect**
- Edge and application‑layer protections, DDoS safeguards, and service‑to‑service communication
- Third‑party and vendor network connectivity used for operations (e.g., liquidity providers, analytics)

---

## 3. Roles & Responsibilities

| Role | Responsibilities |
|---|---|
| Standard Owner | Owns and approves changes; resolves conflicts in interpretation. |
| Security Risk & Governance (SRG) | Governance of exceptions; risk acceptance; audit readiness. |
| Cloud Platform / Network Engineering | AWS network architecture, segmentation, routing, and guardrail implementation. |
| Application Owners | Define port/protocol needs; ensure least‑privilege SG rules and service‑to‑service policies. |
| SOC / SecOps | Continuous monitoring, alerting, incident response integration. |
| Vendor Management | Contractual security for third‑party connectivity; due diligence. |

---

## 4. Minimum Security Requirements (MSRs)

> **Evidence** means screenshots/exports/config JSONs or dashboards that an auditor can inspect.  
> Use **AWS Organizations** and **SCPs** to enforce guardrails wherever possible.

### 4.1 VPC Architecture & Segmentation (NET‑01)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑01.1 | Isolate environments into dedicated **VPCs** (Prod, Non‑Prod, SecOps) with separate accounts; no flat networks. | PR.PT‑05 | A.8.1, A.8.9 | AWS Organizations OU layout; VPC inventories; account/VPC diagrams. |
| NET‑01.2 | Use **subnet tiers** (public, private app, private data) and restrict east‑west flows with SGs and NACLs. | PR.AA‑02, PR.PT‑04 | A.8.1, A.8.8 | Subnet route tables; SG/NACL rulesets; Config/Firewall Manager compliance. |
| NET‑01.3 | Centralize **egress** and **ingress** via shared services (ALB/NLB, NAT, egress VPC) and inspect via **Network Firewall** or partner IDS/IPS. | PR.PT‑04 | A.8.1 | Network Firewall policies; Transit Gateway attachments; flow logs. |
| NET‑01.4 | **Crown Jewel Segments** (wallet/signing, trading engines) must be isolated in dedicated subnets/VPCs with no direct internet routing. | PR.AA‑02, PR.DS‑01 | A.8.1, A.8.8 | Route tables (no IGW paths); VPC peering/PrivateLink topology; SG rules. |
| NET‑01.5 | Use **Transit Gateway** or **VPC Lattice** for controlled service connectivity; deny transitive trust without explicit approval. | PR.PT‑05 | A.8.1 | TGW route tables; Lattice service policies; change records. |

---

### 4.2 Ingress, Egress & Edge Protection (NET‑02)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑02.1 | Terminate public traffic at **CloudFront/ALB/API Gateway** with TLS 1.2+; redirect HTTP→HTTPS; use **AWS Certificate Manager**. | PR.DS‑02 | A.8.23 | Listener configs; ACM certs; TLS policy docs. |
| NET‑02.2 | Protect internet‑facing apps with **AWS WAF** (managed rules + custom rules for business logic); enable **Bot Control** where relevant. | PR.PT‑04 | A.8.8 | WAF web ACLs; rule metrics; blocked request logs. |
| NET‑02.3 | Enforce **least‑egress**: default deny to internet; approve only required destinations/ports with explicit tickets. | PR.AA‑02 | A.8.1 | NAT/egress policies; SG egress lists; change approvals. |
| NET‑02.4 | Use **AWS Shield Advanced** for DDoS on key endpoints (login, trading APIs, hot‑wallet interfaces); define playbooks. | RS.MI‑01 | A.5.30 | Shield Advanced subscription; DDoS response playbooks; incidents. |
| NET‑02.5 | For third‑party integrations, prefer **PrivateLink**/**VPC peering** over public internet; if internet is required, enforce mutual TLS and source pinning. | PR.PT‑04 | A.8.1 | PrivateLink endpoints; peering configs; API mTLS settings. |

---

### 4.3 Identity‑Aware Networking & Access Control (NET‑03)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑03.1 | Prefer **SG‑to‑SG** references and identity‑based policies (IAM, Lattice) over IP‑based rules. | PR.AA‑02 | A.5.15, A.8.1 | SG references; IAM policies; Lattice service policies. |
| NET‑03.2 | **No 0.0.0.0/0** inbound to compute except via managed edge (ALB/API GW/CloudFront); block RDP/SSH from internet. | PR.AA‑03 | A.8.1 | SG analyzer reports; Config rules flagging 0.0.0.0/0. |
| NET‑03.3 | Admin access to private subnets via **SSM Session Manager** (no bastion, no inbound SSH); break‑glass logged. | PR.AA‑03 | A.5.17 | SSM session logs; SCPs denying `ec2:AuthorizeSecurityGroupIngress` for 22/3389. |
| NET‑03.4 | Use **Route 53** private hosted zones for internal service discovery; disallow split‑horizon misconfigurations. | PR.PT‑05 | A.8.1 | Route 53 zone configs; resolver rules. |

---

### 4.4 Data‑in‑Transit Security (NET‑04)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑04.1 | Enforce **TLS 1.2+** everywhere; use modern ciphers; re‑issue certs before expiry; pin keys where feasible for wallet services. | PR.DS‑02 | A.8.23 | Listener security policies; ACM renewal reports. |
| NET‑04.2 | Encrypt east‑west traffic for sensitive services (wallet, KMS clients, trading) via mTLS or service mesh (**App Mesh/Envoy**). | PR.DS‑02 | A.8.23 | Mesh configs; certificate authorities; traffic policies. |
| NET‑04.3 | For site‑to‑site connectivity, use **AWS VPN** or **Direct Connect** with MACsec (where available) and route filtering. | PR.DS‑02 | A.8.23 | VPN/Direct Connect configs; MACsec docs; TGW route filters. |

---

### 4.5 Kubernetes & Container Networking (NET‑05)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑05.1 | Use **EKS** in private subnets; restrict control plane access; enable **VPC CNI** with fine‑grained SGs per node/pod where applicable. | PR.PT‑05 | A.8.1, A.8.8 | EKS cluster & endpoint access settings; SGs; Config conformance packs. |
| NET‑05.2 | Enforce **pod‑to‑pod** and **namespace** isolation via **NetworkPolicies**; deny‑all by default for sensitive namespaces. | PR.AA‑02 | A.8.1 | NetworkPolicy manifests; admission controller policies. |
| NET‑05.3 | Ingress via **ALB Ingress Controller** with WAF integration; encrypt to pods; no public node ports. | PR.DS‑02 | A.8.23 | Ingress manifests; ALB/WAF attachments. |
| NET‑05.4 | **Service Mesh** for mTLS, authz, and traffic policy on critical services (trading, wallet APIs). | PR.DS‑02 | A.8.23 | Mesh policy exports; telemetry proving mTLS enforced. |

---

### 4.6 Observability: Flow Logs, IDS/IPS & Threat Detection (NET‑06)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑06.1 | Enable **VPC Flow Logs** (all subnets) to a central account/S3 with **Object Lock**; retain ≥ 400 days. | DE.CM‑01 | A.5.33, A.8.16 | Flow Log configuration; S3 retention & WORM settings. |
| NET‑06.2 | Enable **GuardDuty** (org‑wide) and investigate High/Medium network findings within defined SLAs. | DE.CM‑07 | A.8.16 | GuardDuty console; finding tickets; closure notes. |
| NET‑06.3 | Use **Network Firewall** or IDS/IPS inline for east‑west and egress inspection on high‑risk segments. | PR.PT‑04 | A.8.1 | Firewall policies; Suricata rule updates; throughput metrics. |
| NET‑06.4 | Centralize logs (WAF, ALB/NLB, CloudFront, API GW, Route 53 Resolver, VPC Flow, NAT, VPN) into SIEM; build anomaly alerts. | DE.CM‑08 | A.8.16 | Kinesis/Firehose routes; SIEM dashboards; alert runbooks. |

---

### 4.7 Change Control, Baselines & Guardrails (NET‑07)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑07.1 | All network changes tracked via tickets and **Infrastructure‑as‑Code (IaC)** pipelines with peer review. | PR.IP‑03 | A.8.9 | Git PRs; CI logs; change records linked to deployments. |
| NET‑07.2 | Enforce **SCPs** and **AWS Config** rules (e.g., no public S3/EFS, no 0.0.0.0/0 to admin ports, mandatory Flow Logs). | PR.PT‑06 | A.8.1, A.8.9 | SCPs; Config rule compliance dashboards; auto‑remediation evidence. |
| NET‑07.3 | Use **Firewall Manager** for org‑wide WAF, SG auditing, and Network Firewall policy enforcement. | PR.PT‑06 | A.8.1 | Firewall Manager policies; non‑compliance reports. |

---

### 4.8 Third‑Party Connectivity & Remote Access (NET‑08)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑08.1 | Prefer **PrivateLink**, VPN, or DX for vendor connectivity; public endpoints require mTLS and IP pinning. | PR.PT‑04 | A.5.20, A.8.1 | PrivateLink endpoints; VPN configs; allowlists. |
| NET‑08.2 | **Time‑bound** access for vendors; log and review quarterly; remove when no longer needed. | PR.AA‑05 | A.5.19 | IAM roles with session duration; Flow Log evidence; review attestations. |
| NET‑08.3 | Remote admin access must use **SSM Session Manager** or zero‑trust proxies with MFA; no direct SSH/RDP from internet. | PR.AA‑03 | A.5.17 | SSM session logs; PAM evidence; SCPs. |

---

### 4.9 Crypto‑Specific Safeguards (NET‑09)

| Control ID | Requirement | NIST CSF | ISO 27001 | AWS Evidence |
|---|---|---|---|---|
| NET‑09.1 | **Wallet/Signing** segments: deny inbound from non‑wallet VPCs; access only via approved service endpoints; no public routes. | PR.AA‑02 | A.8.1 | Route tables; SGs; PrivateLink policies. |
| NET‑09.2 | **Trading & Market Data**: prioritize low latency while preserving segmentation (dedicated subnets/VPC peering/TGW routes). | PR.PT‑05 | A.8.1 | TGW policies; peering configs; latency SLOs vs security rules. |
| NET‑09.3 | **Cold Wallet Ops**: network‑isolated jump windows using ephemeral access, audited, and dual‑control approvals. | PR.AA‑05 | A.8.1, A.8.16 | Change windows; break‑glass logs; dual‑approval records. |

---

## 5. Monitoring & Metrics

- **Coverage**: % of VPCs with Flow Logs + GuardDuty + WAF/Firewall Manager coverage  
- **Exposure**: # of SGs with 0.0.0.0/0 to sensitive ports; # of public subnets with unintended routes  
- **Edge Security**: WAF rule effectiveness (blocked/allowed), Shield incidents MTTR  
- **Findings**: GuardDuty network findings (open, MTTR, SLA breach)  
- **Change Hygiene**: % of network changes via IaC; failed/rolled‑back changes

---

## 6. Evidence Retention

- Retain network security evidence for **≥ 2 years** in **S3 with Object Lock**.  
- Evidence includes: configs, flow logs, WAF/Firewall logs, Config/SCP compliance, change approvals, incident records.

---

## 7. Exceptions

- Exceptions must be **documented, risk‑assessed, time‑boxed**, and approved by **SRG**.  
- Compensating controls (WAF rules, SG tightening, mTLS, rate limiting) must be implemented and verified.

---

## 8. Review & Maintenance

- Review this standard **at least every 24 months** or upon significant architecture/regulatory change.  
- Validate guardrails after major AWS service updates or region expansions.

---

## 9. Quick AWS-to-Control Reference (Auditor Cheat Sheet)

- **Segmentation & Routing:** VPCs, Subnets, NACLs, SGs (SG‑to‑SG), TGW, VPC Lattice, PrivateLink  
- **Edge & DDoS:** CloudFront, ALB/NLB, API Gateway, WAF, AWS Shield Advanced, ACM  
- **Inspection:** AWS Network Firewall, IDS/IPS partners  
- **Observability:** VPC Flow Logs, WAF/ALB/CloudFront/API GW logs, Route 53 Resolver Query Logs, GuardDuty, CloudTrail  
- **Guardrails:** Organizations, SCPs, AWS Config, Firewall Manager  
- **Remote Admin:** SSM Session Manager (no inbound SSH/RDP)
