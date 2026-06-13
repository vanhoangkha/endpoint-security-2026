# Part 5: Policy, Compliance & Frameworks (NIST)

## Series: Endpoint Security 2026 - Complete Guide

---

## 1. Tại sao Policy & Compliance quan trọng?

Endpoint security không chỉ là technology — nó cần **policy governance** để đảm bảo:

- Mọi endpoint tuân thủ security baselines
- Tổ chức đáp ứng yêu cầu regulatory
- Có accountability khi incidents xảy ra
- Leadership có thể track và review security posture

> "In 2026, cyber risk is a boardroom-level financial liability, officially elevated to the same tier as financial and legal risk." — ComplyJet

---

## 2. NIST Cybersecurity Framework 2.0 (CSF 2.0)

### 2.1 Overview

NIST CSF 2.0 (released Feb 2024, celebrating 2 years in Feb 2026) là **voluntary framework** gồm standards, guidelines, và best practices để quản lý cybersecurity risk.

### 2.2 Sáu Core Functions (CSF 2.0)

| Function | Mô tả | Áp dụng cho Endpoint |
|----------|--------|----------------------|
| **GOVERN** (New in 2.0) | Establish cybersecurity strategy & oversight | Endpoint security governance, budget, accountability |
| **IDENTIFY** | Understand assets, risks, and supply chain | Asset inventory, risk assessment |
| **PROTECT** | Implement safeguards | EPP, hardening, encryption, access control |
| **DETECT** | Discover anomalies & events | EDR/XDR monitoring, behavioral analysis |
| **RESPOND** | Take action on detected incidents | Containment, investigation, communication |
| **RECOVER** | Restore capabilities | Backup restoration, lessons learned |

### 2.3 NIST CSF Applied to Endpoint Security

#### GOVERN (GV)
```
GV.OC: Organizational Context
  - Define endpoint security roles & responsibilities
  - Align endpoint strategy with business objectives
  - Board-level reporting on endpoint risk

GV.RM: Risk Management Strategy
  - Risk appetite cho endpoint threats
  - Accept/mitigate/transfer decisions
  - Third-party endpoint risk management
```

#### IDENTIFY (ID)
```
ID.AM: Asset Management
  - Complete inventory of ALL endpoints
  - Hardware/software asset tracking
  - Data classification on endpoints
  - Unmanaged device discovery

ID.RA: Risk Assessment
  - Endpoint vulnerability scanning
  - Threat modeling per endpoint type
  - Risk scoring per device
```

#### PROTECT (PR)
```
PR.AA: Identity & Access Management
  - MFA on all endpoints
  - Conditional access policies
  - Privileged access management

PR.DS: Data Security
  - Disk encryption (BitLocker, FileVault)
  - DLP on endpoints
  - Secure data destruction

PR.IP: Protective Technology
  - EDR/EPP deployment
  - Application control
  - Security baselines & hardening
  - Patch management
```

#### DETECT (DE)
```
DE.CM: Continuous Monitoring
  - EDR telemetry collection
  - Behavioral anomaly detection
  - Threat hunting activities

DE.AE: Analysis
  - Alert triage & investigation
  - MITRE ATT&CK mapping
  - False positive tuning
```

#### RESPOND (RS)
```
RS.MA: Incident Management
  - Endpoint isolation procedures
  - Forensic preservation
  - Escalation workflows

RS.CO: Communications
  - Internal notification procedures
  - Regulatory breach notification
  - Stakeholder updates
```

#### RECOVER (RC)
```
RC.RP: Recovery Planning
  - Endpoint restore procedures
  - Backup validation
  - Business continuity for endpoint loss

RC.IM: Improvements
  - Post-incident review
  - Policy updates based on lessons learned
  - Continuous improvement cycle
```

---

## 3. NIST SP 800-53: Security Controls cho Endpoints

### 3.1 Relevant Control Families

| Control Family | ID | Endpoint Relevance |
|---------------|----|--------------------|
| **Access Control** | AC | User auth, session management, remote access |
| **Audit & Accountability** | AU | Logging, monitoring, audit trails |
| **Configuration Management** | CM | Baselines, change control, inventory |
| **Identification & Authentication** | IA | MFA, device identity, credential management |
| **Incident Response** | IR | Detection, containment, recovery |
| **Maintenance** | MA | Patching, updates, remote maintenance |
| **Media Protection** | MP | Encryption, secure disposal |
| **System & Communications Protection** | SC | Network segmentation, encryption in transit |
| **System & Information Integrity** | SI | Malware protection, vulnerability management |

### 3.2 Key Controls cho Endpoint Security

```
AC-2:  Account Management — manage user accounts on endpoints
AC-7:  Unsuccessful Logon Attempts — lockout policies
AU-2:  Audit Events — define what to log on endpoints
AU-6:  Audit Review, Analysis, and Reporting
CM-2:  Baseline Configuration — security baselines
CM-6:  Configuration Settings — hardening standards
CM-7:  Least Functionality — disable unnecessary services
CM-8:  System Component Inventory — asset management
IA-2:  Identification and Authentication — MFA
IA-5:  Authenticator Management — password policies
IR-4:  Incident Handling — response procedures
IR-6:  Incident Reporting — notification timelines
MA-2:  Controlled Maintenance — patching procedures
MP-6:  Media Sanitization — secure device disposal
SC-7:  Boundary Protection — firewall, segmentation
SC-28: Protection of Information at Rest — encryption
SI-2:  Flaw Remediation — vulnerability patching
SI-3:  Malicious Code Protection — AV/EDR
SI-4:  System Monitoring — continuous monitoring
SI-7:  Software, Firmware, and Information Integrity
```

---

## 4. Endpoint Security Policy: Xây dựng từ đầu

### 4.1 Policy Structure

```
┌─────────────────────────────────────────┐
│         Endpoint Security Policy         │
├─────────────────────────────────────────┤
│  1. Purpose & Scope                      │
│  2. Roles & Responsibilities             │
│  3. Acceptable Use                       │
│  4. Device Requirements                  │
│  5. Access Control                       │
│  6. Data Protection                      │
│  7. Monitoring & Compliance              │
│  8. Incident Response                    │
│  9. Enforcement & Exceptions             │
│  10. Review & Update Schedule            │
└─────────────────────────────────────────┘
```

### 4.2 Essential Policy Elements

#### Device Requirements (Minimum Security Baseline)

```
ALL managed endpoints MUST:
☐ Run approved OS version (within N-1 patch level)
☐ Have EDR agent installed, active, and reporting
☐ Enable disk encryption (BitLocker/FileVault)
☐ Have host-based firewall enabled
☐ Auto-lock after 5 minutes of inactivity
☐ Use approved DNS (block known malicious domains)
☐ Have latest critical patches within 72 hours
☐ Register with UEM/MDM system

PROHIBITED on managed endpoints:
☒ Disable or tamper with security agents
☒ Install unauthorized software
☒ Store unencrypted sensitive data
☒ Connect to unsecured public Wi-Fi without VPN
☒ Share credentials or bypass MFA
☒ Use personal cloud storage for work data
```

#### BYOD Policy

```
Personal devices accessing corporate resources MUST:
☐ Enroll in MDM (work profile only)
☐ Meet minimum OS version requirements
☐ Enable screen lock with biometric or PIN (6+)
☐ Allow remote wipe of corporate data (not personal)
☐ Use corporate VPN for all work traffic
☐ Accept monitoring of work-related activities only

Access limitations for BYOD:
- View-only access to sensitive data
- No offline sync of confidential files
- Session timeout: 8 hours max
- Geo-restrictions apply
```

#### Patch Management Policy

```
Critical patches:    Deploy within 72 hours
High patches:       Deploy within 7 days
Medium patches:     Deploy within 30 days
Low patches:        Deploy within 90 days

NOTE (2026 Reality):
- Exploitation time collapsed from 56 days → ~10 hours
- CISA new directive: risk-based patching (not CVSS-only)
- EPSS (Exploit Prediction Scoring System) now required alongside CVSS
- AI + automation patches for M365 Copilot, GitHub Copilot, Azure ML now included
- "Patching on human schedules while attackers operate at machine speed" is malpractice

2026 Best Practice (Action1/CISA):
- Prioritize by real-world exploitation + asset exposure + attacker impact
- CVSS-only prioritization is now considered MALPRACTICE (Dupple 2026)
- Automate where possible — manual patching cannot keep up
- Include firmware, drivers, and AI tooling in patch scope

Exceptions:
- Require documented business justification
- Must have compensating controls
- Review every 30 days
- Approve by CISO or delegate
```

---

## 5. Compliance Frameworks & Regulations

### 5.1 Framework Comparison cho Endpoint Security

| Framework | Scope | Mandatory? | Endpoint Focus |
|-----------|-------|-----------|----------------|
| **NIST CSF 2.0** | All organizations | Voluntary (mandatory for US federal) | High |
| **NIST 800-53** | Federal systems | Mandatory (FISMA) | Very High |
| **ISO 27001** | Global standard | Voluntary (certification) | High |
| **CIS Controls v8** | All organizations | Voluntary | Very High (Controls 1-6) |
| **PCI DSS 4.0** | Payment card data | Mandatory (contractual) | Medium |
| **HIPAA** | Healthcare (US) | Mandatory | Medium |
| **GDPR** | EU personal data | Mandatory | Medium |
| **SOC 2** | Service providers | Voluntary (trust) | Medium |
| **CMMC 2.0** | DoD contractors | Mandatory | High |

### 5.2 CIS Controls v8: Top Priority cho Endpoints

```
Control 1:  Inventory and Control of Enterprise Assets
Control 2:  Inventory and Control of Software Assets
Control 3:  Data Protection
Control 4:  Secure Configuration of Enterprise Assets
Control 5:  Account Management
Control 6:  Access Control Management
Control 7:  Continuous Vulnerability Management
Control 8:  Audit Log Management
Control 9:  Email and Web Browser Protections
Control 10: Malware Defenses
Control 13: Network Monitoring and Defense
```

### 5.3 Compliance Automation

```
Traditional compliance:
  Manual audit → spreadsheets → point-in-time assessment → report

2026 compliance:
  Continuous monitoring → automated evidence collection → 
  real-time dashboards → always-ready for audit
```

**Tools hỗ trợ:**
- Microsoft Compliance Manager
- Qualys Policy Compliance
- Rapid7 InsightVM
- Tenable.io
- Drata / Vanta (SOC 2 automation)

---

## 6. NIST Compliance Implementation: Step-by-Step

### Step 1: Gap Analysis

```
Assessment activities:
1. Map current controls to NIST framework
2. Identify gaps vs required controls
3. Prioritize based on risk & effort
4. Document current state vs target state
5. Get leadership buy-in with risk quantification
```

### Step 2: Control Selection

```
Based on:
- Organization risk profile
- Regulatory requirements
- System categorization (Low/Moderate/High impact)
- Available resources & budget
- Industry best practices
```

### Step 3: Implementation

```
For endpoints specifically:
1. Deploy UEM/MDM → achieve device visibility
2. Define & enforce security baselines
3. Deploy EDR → detection capability
4. Enable encryption → data protection
5. Implement PAM → access control
6. Automate patching → vulnerability management
7. Configure logging → audit capability
```

### Step 4: Documentation

```
Required documentation:
- System Security Plan (SSP)
- Risk Assessment Report
- Plan of Action & Milestones (POA&M)
- Incident Response Plan
- Configuration Management Plan
- Continuous Monitoring Strategy
```

### Step 5: Assessment

```
- Internal assessment (self-evaluation)
- Third-party assessment (auditor)
- Penetration testing
- Vulnerability assessments
- Control effectiveness testing
```

### Step 6: Continuous Monitoring

```
Ongoing activities:
- Real-time compliance dashboards
- Automated drift detection
- Regular vulnerability scans
- Periodic control assessments
- Policy exception reviews
- Annual full reassessment
```

---

## 7. Endpoint Hardening Standards

### 7.1 CIS Benchmarks (Updated 2026)

CIS cung cấp detailed hardening guides cho:
- Windows 10/11 Enterprise
- **Apple macOS 26 Tahoe** (v1.1.0 — released 2026)
- Linux (Ubuntu, RHEL, CentOS)
- iOS / Android
- Servers (Windows Server, Linux)
- **Microsoft Intune for Windows** (new — GPO automation)
- Cloud platforms (AWS, Azure, GCP)
- Kubernetes, Docker

**CIS Benchmarks 2026 Stats:**
- Over **100+ benchmarks** published
- Developed by subject matter experts + public comment
- Automation support: GPOs (Windows), Bash scripts (Unix/Linux)
- Tools: CIS-CAT Pro, Wazuh, NinjaOne, Automox

**Real-world case:** "From 0% to 92% compliance — hardening Windows 11 against CIS Benchmark using Wazuh + PowerShell automation" (Medium, June 2026)

### 7.2 Windows Endpoint Hardening Checklist

```
OS Configuration:
☐ Enable BitLocker with TPM
☐ Configure Windows Firewall (deny inbound by default)
☐ Disable SMBv1
☐ Enable Credential Guard
☐ Enable LSASS protection (RunAsPPL)
☐ Disable unnecessary services (Remote Registry, etc.)
☐ Configure AppLocker/WDAC policies
☐ Enable Secure Boot + UEFI

Authentication:
☐ Enforce password complexity (14+ characters)
☐ Account lockout after 5 failed attempts
☐ MFA required for all users
☐ Block NTLM where possible
☐ Disable storing LAN Manager hash

Logging & Monitoring:
☐ Enable PowerShell Script Block Logging
☐ Enable Process Creation auditing (Event 4688)
☐ Enable command-line in process creation events
☐ Configure Windows Event Forwarding (WEF)
☐ Enable Sysmon for detailed telemetry

Network:
☐ Disable LLMNR and NetBIOS
☐ Configure DNS-over-HTTPS
☐ Block outbound to known-bad IPs (threat intel)
☐ Restrict RDP access (only via jump server)
```

---

## 8. Governance & Accountability

### 8.1 RACI Matrix cho Endpoint Security

| Activity | CISO | IT Ops | Security Team | End Users |
|----------|------|--------|---------------|-----------|
| Policy creation | A | C | R | I |
| Baseline definition | A | C | R | I |
| Agent deployment | I | R | C | I |
| Patch management | A | R | C | I |
| Incident response | A | C | R | I |
| Compliance reporting | A | C | R | I |
| Security awareness | A | I | R | C |
| Exception approval | R | I | C | I |

*R=Responsible, A=Accountable, C=Consulted, I=Informed*

### 8.2 Reporting to Leadership

**Monthly Dashboard:**
- % endpoints compliant with baseline
- Critical vulnerabilities unpatched > SLA
- Number of security incidents
- Mean time to patch critical vulnerabilities
- EDR agent health & coverage

**Quarterly Board Report:**
- Risk posture trend (improving/declining)
- Compliance status vs frameworks
- Key incidents and lessons learned
- Budget vs spending vs risk reduction
- Peer benchmarking

---

## 9. Exception Management

```
Exception Request Process:
1. Business justification documented
2. Risk assessment completed
3. Compensating controls identified
4. Time-limited (max 90 days, renewable)
5. Approved by appropriate authority:
   - Low risk: Security team lead
   - Medium risk: CISO
   - High risk: CIO + CISO
6. Tracked in exception register
7. Reviewed at each expiration
8. Audit trail maintained
```

---

## 10. Key Takeaways

- **NIST CSF 2.0** cung cấp framework toàn diện với 6 functions (GOVERN mới)
- **Compliance không phải one-time** — continuous monitoring là yêu cầu 2026
- **Policy phải actionable** — clear baselines, measurable, enforceable
- **Automation là key** — manual compliance không scale
- **Gap analysis trước** — biết mình ở đâu trước khi quyết định đi đâu
- **Leadership accountability** — cyber risk = boardroom issue

---

## Tiếp theo

**→ Part 6: Incident Response & Best Practices**

---

*Series: Endpoint Security 2026 | Sources: NIST CSF 2.0, NIST SP 800-53, SentinelOne, Heimdal, UpGuard, Trio, Microsoft, CIS | Date: June 2026*
