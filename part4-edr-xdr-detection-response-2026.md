# Part 4: EDR/XDR — Detection & Response

## Series: Endpoint Security 2026 - Complete Guide

---

## 1. EDR vs XDR: Định nghĩa và sự khác biệt

### 1.1 EDR (Endpoint Detection and Response)

EDR là công nghệ bảo mật **liên tục giám sát endpoint devices** (laptops, desktops, servers, cloud workloads) để phát hiện hành vi đáng ngờ, điều tra threats, và thực hiện containment/remediation.

### 1.2 XDR (Extended Detection & Response)

XDR mở rộng EDR bằng cách **correlate telemetry từ nhiều sources**: endpoint, network, identity, cloud, và email — phát hiện multi-vector attacks mà isolated tools không thể thấy.

### 1.3 So sánh chi tiết

| Tiêu chí | EDR | XDR |
|----------|-----|-----|
| **Scope** | Endpoint only | Endpoint + Network + Identity + Cloud + Email |
| **Telemetry** | Process, file, registry, network (từ endpoint) | Cross-domain signals |
| **Detection** | Endpoint-focused behavioral analysis | Multi-vector attack correlation |
| **Visibility** | Deep on single endpoint | Broad across infrastructure |
| **Alert context** | Endpoint-level | Full attack story cross-platform |
| **Limitation** | Blind spot ngoài endpoint | Requires multi-vendor integration |

> "EDR delivers depth on the endpoint; XDR delivers breadth across endpoint, network, identity, cloud, and email telemetry." — Vectra AI 2026

### 1.4 Tại sao EDR alone không đủ trong 2026?

- **EDR-killer tooling** đã được 10+ ransomware groups sử dụng → endpoint-only visibility = single point of failure
- Modern attacks span nhiều domains (email → identity → endpoint → cloud)
- Attackers sử dụng LOTL → behaviors trên endpoint trông legitimate
- Cần context từ identity và network để confirm threat

---

## 2. EDR: Deep Dive

### 2.1 Cách EDR hoạt động

```
┌─────────────────────────────────────────────┐
│              EDR Architecture                │
│                                             │
│  ┌─────────┐    ┌──────────────────────┐   │
│  │Endpoint │───▶│ Telemetry Collection │   │
│  │ Agent   │    │ (processes, files,    │   │
│  │         │    │  network, registry)   │   │
│  └─────────┘    └──────────┬───────────┘   │
│                            │               │
│                            ▼               │
│              ┌─────────────────────┐       │
│              │  Cloud Analytics    │       │
│              │  - Behavioral rules │       │
│              │  - ML models        │       │
│              │  - Threat intel     │       │
│              │  - IOC matching     │       │
│              └──────────┬──────────┘       │
│                         │                  │
│                         ▼                  │
│              ┌─────────────────────┐       │
│              │  Detection & Alert  │       │
│              │  + Automated Response│       │
│              └─────────────────────┘       │
└─────────────────────────────────────────────┘
```

### 2.2 Core Capabilities

| Capability | Mô tả |
|-----------|--------|
| **Continuous Monitoring** | Thu thập telemetry 24/7 từ mọi endpoint |
| **Behavioral Detection** | Phát hiện anomalies dựa trên behavior, không chỉ signature |
| **Threat Hunting** | Proactive search cho threats chưa triggered alerts |
| **Investigation** | Timeline reconstruction, root cause analysis |
| **Containment** | Isolate endpoint, kill process, quarantine file |
| **Remediation** | Remove malware, restore files, rollback changes |
| **Forensics** | Full process tree, network connections, file changes |

### 2.3 Telemetry data EDR thu thập

```
Process Events:
  - Process creation (parent-child tree)
  - Command line arguments
  - DLL loading
  - Code injection

File Events:
  - File create/modify/delete
  - File hash changes
  - Ransomware-like bulk encryption

Network Events:
  - DNS queries
  - HTTP/S connections
  - Lateral movement attempts (SMB, WMI, RDP)

Registry Events:
  - Persistence mechanisms (Run keys, Services)
  - Security policy modifications

Authentication Events:
  - Login attempts (success/failure)
  - Privilege escalation
  - Credential access
```

### 2.4 EDR Detection Techniques

| Technique | Ví dụ |
|-----------|-------|
| **IOC matching** | Known malware hashes, C2 domains |
| **Behavioral rules** | PowerShell downloading + executing = suspicious |
| **ML anomaly detection** | Unusual process spawning patterns |
| **MITRE ATT&CK mapping** | Map behaviors to known TTPs |
| **Threat intelligence** | Real-time feeds từ research teams |
| **Stack analysis** | Detect code injection via memory analysis |

---

## 3. XDR: Deep Dive

### 3.1 XDR Correlation Engine

```
Data Sources → Normalization → Correlation → Detection → Response

┌────────────┐
│  Endpoint  │──┐
├────────────┤  │
│  Network   │──┤     ┌──────────────┐     ┌───────────┐
├────────────┤  ├────▶│ Correlation  │────▶│ Unified   │
│  Identity  │──┤     │   Engine     │     │  Alert    │
├────────────┤  │     └──────────────┘     └───────────┘
│   Cloud    │──┤
├────────────┤  │
│   Email    │──┘
└────────────┘
```

### 3.2 XDR Detection: Multi-Vector Attack Example

```
Traditional (siloed) view:
  Email team: "User received phishing email" → LOW priority
  Identity team: "Failed MFA attempt" → LOW priority  
  Endpoint team: "PowerShell execution" → MEDIUM priority
  Network team: "Unusual outbound traffic" → LOW priority

XDR correlated view:
  "User received phishing → clicked link → credential compromised → 
   attacker logged in → PowerShell downloaded tool → 
   lateral movement → data exfiltration detected"
  → CRITICAL INCIDENT with full attack chain
```

### 3.3 XDR Advantages

- **Giảm alert fatigue** — correlate many low-severity → one high-severity incident
- **Full attack story** — hiểu complete kill chain, không chỉ fragments
- **Faster investigation** — tất cả evidence trong một console
- **Better detection** — patterns chỉ visible khi combine multiple sources
- **Automated response** — coordinate actions across domains

---

## 4. Top EDR/XDR Platforms 2026

### 4.1 Market Leaders (Updated June 2026)

| Platform | Type | Strengths | Notable 2026 |
|----------|------|-----------|--------------|
| **CrowdStrike Falcon** | EDR/XDR | Threat intel, speed, lightweight agent | Overwatch threat hunting benchmark |
| **Microsoft Defender XDR** | XDR | Native M365/Azure, identity correlation | Gartner Leader 7th consecutive year, added automated endpoint isolation |
| **SentinelOne Singularity** | XDR | AI autonomous response, Purple AI | Best autonomous response capability |
| **Palo Alto Cortex XDR** | XDR | Network+endpoint, XSIAM, highest MITRE scores | Highest combined protection+detection in MITRE evals |
| **Trend Micro Vision One** | XDR | Multi-layer, broad telemetry | AI endpoint convergence focus |

### 4.2 Head-to-Head: CrowdStrike vs SentinelOne vs Microsoft Defender (2026)

| Category | CrowdStrike Falcon | SentinelOne Singularity | Microsoft Defender XDR |
|----------|-------------------|------------------------|----------------------|
| **Best for** | Threat intelligence + human hunting | Autonomous response + speed | Microsoft ecosystem integration |
| **AI/Automation** | Charlotte AI copilot | Purple AI (NL threat hunting) | Copilot for Security |
| **MITRE ATT&CK** | Strong detection coverage | Strong autonomous blocking | Good prevention, improving detection |
| **Unique Advantage** | Overwatch 24/7 human hunting | Storyline™ automated correlation | Native identity + email + cloud correlation |
| **Weakness** | Higher cost | Complex setup for non-enterprise | Requires full Microsoft stack |
| **AiTM Token Theft** | ❌ Not detected at endpoint | ❌ Not detected at endpoint | ❌ Not detected at endpoint |
| **Pricing** | Premium ($$$) | Mid-premium ($$) | Best value if already M365 E5 ($) |

> "CrowdStrike wins on threat intelligence. SentinelOne wins on autonomous response. Microsoft wins on ecosystem integration and value." — Redress Compliance 2026

**Key Finding (CloudSkope 2026 test):** None of the big 3 detect AiTM token theft at the endpoint level — this is an architectural limitation requiring identity-layer detection.

### 4.3 MITRE ATT&CK Evaluations (Latest)

**Key developments:**
- For the first time, evaluations included **Reconnaissance tactic** (early-stage detection)
- Now includes **macOS** testing
- New insights on **false positive rates** and **efficiency metrics**
- Evaluations now use **procedural variation** — same technique, different methods

**Vendor highlights:**
- **Palo Alto Cortex XDR**: Highest combined protection + detection
- **ESET**: 100% protection score, tied first place among 9 vendors for earliest blocking
- **Evaluation focus**: Prevention-first approach increasingly validated

> "MITRE ATT&CK Evaluations are not competitive rankings — no scores, ratings, or rankings. They show HOW solutions detect behavior." — MITRE

### 4.4 Key Selection Criteria

```
1. Detection Efficacy
   - MITRE ATT&CK evaluation results
   - False positive rates
   - Zero-day detection capability

2. Response Capabilities
   - Automated containment speed
   - Remediation options
   - Forensic investigation depth

3. Integration
   - SIEM/SOAR connectivity
   - API availability
   - Third-party ecosystem

4. Operational Impact
   - Agent performance (CPU/RAM footprint)
   - Deployment complexity
   - Analyst workflow efficiency

5. Coverage
   - OS support (Windows, macOS, Linux, mobile)
   - Cloud workload protection
   - Container/Kubernetes support
```

---

## 5. Automated Incident Response (2026)

### 5.1 Sự chuyển đổi: Manual → Automated

> "The best EDR/XDR tools for automated incident response in 2026 are defined by the ability to contain a threat without waiting for an analyst to approve the action." — Ciphers Security

### 5.2 Automated Response Actions

| Severity | Action | Approval |
|----------|--------|----------|
| **Critical** | Isolate endpoint from network | Auto (immediate) |
| **Critical** | Kill malicious process | Auto |
| **High** | Block suspicious IP/domain | Auto |
| **High** | Disable compromised user account | Auto or 1-click |
| **Medium** | Quarantine suspicious file | Auto |
| **Medium** | Force password reset | Semi-auto (notify admin) |
| **Low** | Alert analyst for review | Manual |

### 5.3 Response Playbook: Ransomware Detection

```
TRIGGER: EDR detects bulk file encryption + ransom note creation

AUTOMATED RESPONSE (within seconds):
  1. ISOLATE endpoint from network (preserve evidence)
  2. KILL ransomware process tree
  3. BLOCK lateral movement (disable SMB shares)
  4. DISABLE associated user account
  5. SNAPSHOT endpoint state for forensics
  6. ALERT SOC team with full context
  7. CHECK other endpoints for same IOCs
  8. INITIATE backup verification

ANALYST FOLLOW-UP:
  9. Root cause investigation
  10. Scope assessment (blast radius)
  11. Recovery initiation
  12. Post-incident review
```

---

## 6. EDR Evasion & Counter-Measures

### 6.1 Kỹ thuật Attacker dùng để bypass EDR

| Technique | Mô tả | Counter-Measure |
|-----------|--------|-----------------|
| **EDRKillShifter** | Terminate EDR processes via BYOVD | Tamper protection, driver blocklist |
| **Direct syscalls** | Bypass user-mode hooks | Kernel-level monitoring |
| **DLL sideloading** | Load malicious DLL via legitimate app | DLL integrity checking |
| **Timestomping** | Modify file timestamps | Multiple evidence sources |
| **Process hollowing** | Inject code into legitimate process | Memory scanning |
| **Fileless malware** | Execute only in memory | Memory analysis, AMSI |
| **LOLBin abuse** | Use legitimate OS tools | Behavioral analytics |

### 6.2 EDR Resilience Best Practices

1. **Tamper protection enabled** — prevent agent uninstall/disable
2. **Kernel-level sensors** — not just user-mode hooks
3. **Cloud-based analysis** — agent cannot be fully blinded locally
4. **Multi-signal correlation** — XDR fills EDR blind spots
5. **Regular agent updates** — patch evasion techniques quickly
6. **Driver vulnerability management** — block known vulnerable drivers
7. **Canary processes** — detect EDR-killing attempts

---

## 7. Threat Hunting với EDR/XDR

### 7.1 Proactive vs Reactive

```
Reactive: Wait for alert → investigate → respond
Proactive: Hypothesize threat → hunt for evidence → find → remediate

Trong 2026, proactive threat hunting là requirement, không còn luxury.
```

### 7.2 Threat Hunting Queries (Examples)

**Hunt 1: Suspicious PowerShell**
```
Query: processes WHERE 
  name = "powershell.exe" AND
  (command_line CONTAINS "-encodedcommand" OR
   command_line CONTAINS "-nop" OR
   command_line CONTAINS "downloadstring" OR
   command_line CONTAINS "IEX")
  AND parent_process NOT IN (approved_automation_list)
```

**Hunt 2: LOTL Lateral Movement**
```
Query: network_events WHERE
  destination_port IN (445, 135, 5985, 5986) AND
  source_process IN ("wmiprvse.exe", "powershell.exe", "cmd.exe") AND
  source_user != destination_machine_owner
```

**Hunt 3: EDR Tampering**
```
Query: process_events WHERE
  target_process_name IN (edr_process_list) AND
  action IN ("terminate", "suspend") AND
  actor_process NOT IN (trusted_management_tools)
```

**Hunt 4: Credential Dumping**
```
Query: file_events WHERE
  target_path CONTAINS "lsass" OR
  (process_name = "rundll32.exe" AND 
   command_line CONTAINS "comsvcs.dll" AND
   command_line CONTAINS "MiniDump")
```

---

## 8. EDR/XDR Deployment Best Practices

### 8.1 Deployment Checklist

```
Pre-Deployment:
☐ Inventory all endpoints (OS, version, role)
☐ Test agent compatibility in lab environment
☐ Define exclusion policies (performance-sensitive apps)
☐ Plan rollout waves (pilot → dept → org-wide)
☐ Configure network access for cloud console

Deployment:
☐ Deploy to 100% managed endpoints
☐ Enable tamper protection immediately
☐ Configure alert severity levels
☐ Set up automated response policies (start conservative)
☐ Integrate with SIEM/SOAR

Post-Deployment:
☐ Tune false positives (first 2-4 weeks)
☐ Validate detection with purple team exercises
☐ Train SOC analysts on investigation workflows
☐ Establish threat hunting cadence
☐ Monitor agent health & coverage gaps
```

### 8.2 Common Mistakes to Avoid

- ❌ Deploy trong detection-only mode vĩnh viễn (không bao giờ enable response)
- ❌ Exclude quá nhiều paths/processes (tạo blind spots)
- ❌ Ignore agent health alerts (agent offline = invisible endpoint)
- ❌ Không integrate với identity systems (miss full attack context)
- ❌ Không test automated response (surprise failures during real incident)

---

## 9. Metrics & KPIs

| Metric | Target 2026 |
|--------|-------------|
| **MTTD** (Mean Time to Detect) | < 1 hour |
| **MTTR** (Mean Time to Respond) | < 30 minutes |
| **Agent coverage** | > 99% managed endpoints |
| **Agent health** | > 98% online & updated |
| **False positive rate** | < 5% of alerts |
| **Automated containment** | > 80% of critical alerts |
| **MITRE ATT&CK coverage** | > 85% of techniques |
| **Threat hunting frequency** | Weekly cadence |

---

## 10. Tương lai: Từ EDR/XDR → AI-Native SOC

### 2026 và Beyond:

- **AI copilots** — Purple AI (SentinelOne), Copilot for Security (Microsoft) hỗ trợ investigation
- **Autonomous triage** — AI phân loại và prioritize alerts
- **Natural language hunting** — query bằng tiếng Anh thay vì query language
- **Predictive detection** — phát hiện pre-attack indicators
- **Self-healing endpoints** — auto-remediation không cần human
- **Identity-aware EDR** — correlate endpoint behavior với user risk

---

## 11. Key Takeaways

- **EDR là table stakes** — minimum requirement, không còn competitive advantage
- **XDR là evolution cần thiết** — vì attacks span multiple domains
- **Automated response là defining factor** — contain trong giây, không phải giờ
- **EDR evasion là thực tế** — cần tamper protection + multi-signal detection
- **Threat hunting chuyển từ luxury → requirement** — proactive beats reactive
- **AI-native operations** — the next evolution of detection & response

---

## Tiếp theo

**→ Part 5: Policy, Compliance & Frameworks (NIST)**

---

*Series: Endpoint Security 2026 | Sources: Vectra AI, CrowdStrike, SentinelOne, Palo Alto, Heimdal Security, The Hacker News, Ciphers Security | Date: June 2026*
