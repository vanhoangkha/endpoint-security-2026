# Part 3: Zero Trust Architecture & Endpoint Security

## Series: Endpoint Security 2026 - Complete Guide

---

## 1. Zero Trust là gì?

Zero Trust là mô hình bảo mật được xây dựng trên nguyên tắc: **"Never trust, always verify"** — không tin tưởng bất kỳ user, device, workload, hay service nào theo mặc định, bất kể request đến từ bên trong hay bên ngoài mạng.

> "Every access request must be authenticated, authorized, and continuously validated before access is granted." — NIST SP 800-207

### Ba nguyên tắc cốt lõi (Microsoft Zero Trust):

1. **Verify explicitly** — Luôn xác thực và ủy quyền dựa trên tất cả data points
2. **Use least privilege access** — Giới hạn quyền truy cập tối thiểu cần thiết
3. **Assume breach** — Giả định hệ thống đã bị xâm nhập, minimize blast radius

---

## 2. Tại sao Zero Trust quan trọng trong 2026?

### 2.1 Perimeter-based security đã thất bại

Mô hình truyền thống (castle-and-moat):
- Trust mọi thứ bên trong network perimeter
- Chỉ verify traffic đến từ bên ngoài
- **Không phù hợp** với remote work, cloud, BYOD

### 2.2 Thống kê Gartner 2026

> "By the end of 2026, 10% of large enterprises will have a mature and measurable zero trust program in place, up from less than 1% in 2023." — Gartner Strategic Roadmap for Zero Trust

### 2.3 IGEL Zero Trust Evolution (2024 → 2026)

- 2024: Zero Trust là concept/framework
- 2025: Zero Trust bắt đầu được enforce (not just planned)
- 2026: Zero Trust trở thành **operational requirement**, không còn optional

---

## 3. Zero Trust Architecture (ZTA) cho Endpoint Security

### 3.1 Mô hình kiến trúc

```
┌─────────────────────────────────────────────────────────┐
│                    Policy Engine (PDP)                    │
│  ┌──────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Identity │  │ Device Trust │  │  Risk Assessment │  │
│  │  Provider │  │    Score     │  │     Engine       │  │
│  └──────────┘  └──────────────┘  └──────────────────┘  │
└─────────────────────────┬───────────────────────────────┘
                          │ Allow/Deny/MFA
┌─────────────────────────▼───────────────────────────────┐
│                 Policy Enforcement Point (PEP)            │
└─────────────────────────┬───────────────────────────────┘
                          │
    ┌─────────────────────┼──────────────────────┐
    │                     │                      │
    ▼                     ▼                      ▼
┌────────┐         ┌──────────┐          ┌──────────────┐
│Endpoint│         │  Cloud   │          │  On-Premise  │
│ Agent  │         │ Workload │          │   Resource   │
└────────┘         └──────────┘          └──────────────┘
```

### 3.2 Endpoint trong Zero Trust: 3 vai trò chính

| Vai trò | Mô tả |
|---------|--------|
| **Signal Provider** | Cung cấp device health, compliance status, behavior data |
| **Policy Enforcement** | Thực thi access decisions tại device level |
| **Trust Anchor** | Xác minh device identity và integrity |

### 3.3 Device Trust Score

Zero Trust đánh giá endpoint dựa trên nhiều signals:

```
Device Trust Score = f(
    OS patch level,
    EDR agent status,
    Encryption status,
    Compliance posture,
    Behavioral anomalies,
    Network location,
    User risk level,
    Authentication strength
)
```

**Kết quả:**
- High trust → Full access
- Medium trust → Limited access + step-up MFA
- Low trust → Block access + remediation required

---

## 4. Các pillars của Zero Trust Endpoint Security

### 4.1 Identity Verification

**Identity là control plane chính trong 2026:**

- **Workforce identities** — users, admins
- **Service accounts** — automated processes
- **Machine identities** — APIs, containers, workloads
- **Short-lived credentials** — giảm risk của credential theft

**Triển khai:**
- Strong MFA (phishing-resistant: FIDO2, passkeys)
- Conditional Access Policies
- Just-in-Time (JIT) access
- Passwordless authentication
- Continuous session validation

### 4.2 Device Security & Compliance

**Endpoint phải chứng minh trustworthiness trước khi được access:**

- Device enrolled và managed (UEM/MDM)
- OS updated, patches applied
- EDR agent running và healthy
- Disk encryption enabled
- No jailbreak/root detected
- Compliance với security baseline

### 4.3 Network Micro-Segmentation

- Không flat network — mỗi segment isolated
- East-west traffic cũng bị inspect
- Software-defined perimeter (SDP)
- Per-application access (không full VPN)

### 4.4 Application & Workload Security

- Application whitelisting
- Container security
- Runtime application self-protection (RASP)
- API gateway với authentication

### 4.5 Data Protection

- Data classification & labeling
- DLP policies
- Encryption at rest & in transit
- Rights management (restrict copy, forward, print)

---

## 5. Implementation Roadmap: Zero Trust cho Endpoints

### Phase 1: Foundation (Months 1-3)

```
Asset inventory — identify ALL endpoints
Identity consolidation — single IdP, enforce MFA
Deploy EDR trên 100% managed devices
Enable device compliance policies
Baseline network traffic patterns
```

### Phase 2: Control (Months 4-6)

```
Conditional Access — block non-compliant devices
Network segmentation — isolate critical assets
Privileged Access Management (PAM) deployment
Application control policies
Data classification & DLP
```

### Phase 3: Automation (Months 7-9)

```
Automated remediation for non-compliant endpoints
Risk-based authentication flows
SOAR integration for incident response
Continuous compliance monitoring
Threat hunting workflows
```

### Phase 4: Optimization (Months 10-12)

```
Measure & improve trust scores accuracy
Reduce false positives in access decisions
Cross-platform policy unification
Advanced analytics & threat intelligence
Regular zero trust maturity assessments
```

---

## 6. Zero Trust + Endpoint: Use Cases thực tế

### Use Case 1: Remote Worker Access

```
Scenario: Employee on personal laptop → access corporate app

Zero Trust Flow:
1. User authenticates (MFA + device cert)
2. Device compliance check (EDR active? Patched? Encrypted?)
3. Risk assessment (location, time, behavior)
4. Decision: 
   - Compliant → grant access
   - Non-compliant → limited access (web only, no download)
   - High risk → block + alert SOC
```

### Use Case 2: Compromised Endpoint Detection

```
Scenario: EDR detects suspicious PowerShell execution

Zero Trust Response:
1. EDR signals anomaly → device trust score drops
2. Policy engine revokes active sessions
3. Conditional access blocks new requests
4. Endpoint isolated from network
5. SOC alerted for investigation
6. After remediation → device re-assessed → access restored
```

### Use Case 3: Contractor/BYOD Access

```
Scenario: Contractor needs access to specific project files

Zero Trust Approach:
1. Identity verified via external IdP federation
2. Device assessed (may not be fully managed)
3. Access granted ONLY to specific resources (micro-perimeter)
4. Session monitored continuously
5. No persistent access — re-verify on each session
6. Data: view-only, no download, watermarked
```

---

## 7. Challenges khi triển khai Zero Trust

| Challenge | Giải pháp |
|-----------|-----------|
| **Legacy systems** không support modern auth | Gateway/proxy layer để wrap legacy apps |
| **User friction** từ continuous verification | Risk-based → chỉ challenge khi risk tăng |
| **Visibility gaps** (unmanaged devices) | Network-based controls cho unknown devices |
| **Complexity** — quá nhiều policies | Start small, expand incrementally |
| **Cost** — tools & expertise | Prioritize crown jewels trước |
| **Cultural resistance** | Executive sponsorship + phased rollout |

---

## 8. Zero Trust Maturity Model

### Level 1: Traditional
- Perimeter-based security
- Static passwords
- Full network access sau VPN

### Level 2: Advanced
- MFA deployed
- Some conditional access
- Basic device compliance checks
- Network segmentation bắt đầu

### Level 3: Optimal (Target 2026)
- Continuous verification
- Risk-based adaptive access
- Micro-segmentation everywhere
- Automated response to anomalies
- Cross-domain signal correlation
- Passwordless authentication

---

## 9. Tools & Technologies

### Identity & Access
- Microsoft Entra ID (Conditional Access)
- Okta Identity Engine
- CrowdStrike Falcon Identity

### Endpoint Compliance
- Microsoft Intune
- VMware Workspace ONE
- Jamf (macOS/iOS)

### Network Zero Trust
- Zscaler Private Access (ZPA)
- Palo Alto Prisma Access
- Cloudflare Access

### XDR/Signal Correlation
- Microsoft Defender XDR
- CrowdStrike Falcon
- SentinelOne Singularity

---

## 10. Key Metrics để đo lường Zero Trust

| Metric | Target |
|--------|--------|
| % endpoints compliant | > 95% |
| MFA adoption rate | 100% |
| Mean time to detect non-compliance | < 5 minutes |
| Mean time to revoke access (compromised) | < 1 minute |
| % applications behind Zero Trust | > 90% |
| False positive rate (access blocks) | < 2% |
| Phishing-resistant MFA coverage | > 80% |

---

## 11. Key Takeaways

- **Zero Trust = Strategy, not product** — cần approach có hệ thống, phased implementation
- **Identity là control plane mới** — bao gồm users, services, machines
- **Endpoint là trust signal quan trọng nhất** — device health quyết định access level
- **10% large enterprises** sẽ có mature Zero Trust program vào cuối 2026
- **Continuous validation** — không phải one-time check, mà liên tục monitor
- **Start with identity + endpoints** — đây là foundation, rồi mở rộng sang network/data

---

## Tiếp theo

**→ Part 4: EDR/XDR — Detection & Response**

---

*Series: Endpoint Security 2026 | Sources: NIST SP 800-207, Microsoft, Gartner, IGEL, Reach Security, ESET, GlobalTechCouncil | Date: June 2026*
