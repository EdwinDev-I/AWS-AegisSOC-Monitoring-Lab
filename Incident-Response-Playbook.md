# 📚 Incident Response Playbook

# SOC Detection Lab (Wazuh + Sysmon + Suricata)

## Overview

This repository contains an Incident Response Playbook developed for a Security Operations Center (SOC) detection lab deployed in AWS.

The lab demonstrates how security events are collected, detected, investigated, and responded to using open-source security monitoring tools.

The environment combines:

- Wazuh SIEM/XDR
- Windows Server endpoint monitoring
- Sysmon telemetry collection
- Suricata network intrusion detection
- VirusTotal threat intelligence integration
- Kali Linux attack simulation

The purpose of this playbook is to document the SOC workflow used for:

- Detection
- Investigation
- Containment
- Eradication
- Recovery
- Security improvement

All activities are performed in a controlled lab environment.

---

# 1️⃣ Lab Architecture

## Infrastructure

| Component | Description |
|---|---|
| AWS Cloud | Hosts security monitoring infrastructure |
| Wazuh Manager | Central SIEM and alert analysis platform |
| Windows Server | Endpoint monitored with Wazuh Agent + Sysmon |
| Ubuntu Sensor | Network monitoring with Suricata |
| Kali Linux | Attack simulation environment |

---

# Data Flow
```
kali
|
|
Attack Simulation
|
|
Windows / Ubuntu Endpoint
|
|
Wazuh Agent + Suricata
|
|
Wazuh Manager
|
|
SOC Dashboard Investigation
```
---

# 2️⃣ Security Tools and Data Sources

## Wazuh

Purpose:

- Centralized log collection
- Alert generation
- Detection rules
- Security investigation

Collects:

- Windows Event Logs
- Sysmon events
- Authentication activity
- File integrity monitoring events
- Security alerts


---

## Sysmon

Microsoft Sysinternals monitoring tool.

Provides detailed endpoint telemetry.

Monitored events include:

### Event ID 1
Process Creation

Example:

- PowerShell execution
- Suspicious programs
- Command execution


### Event ID 3
Network Connections

Example:

- Outbound connections
- Suspicious communication


### Event ID 11
File Creation

Example:

- New executables
- Dropped files


---

## Suricata

Network Intrusion Detection System.

Purpose:

- Network traffic inspection
- Protocol monitoring
- IDS alert generation

Logs:
```
/var/log/suricata/eve.json
```
Suricata helps detect:

- Scanning activity
- Suspicious connections
- Network-based attacks

---

## VirusTotal

Threat intelligence enrichment.

Workflow:
```
File Detected
|
|
Wazuh Syscheck
|
|
File Hash Generated
|
|
VirusTotal Lookup
|
|
Threat Intelligence Result
```

---

# 3️⃣ Incident Response Lifecycle

The SOC follows the standard incident response process:

1. Preparation
2. Detection and Analysis
3. Containment
4. Eradication
5. Recovery
6. Lessons Learned

---

# 4️⃣ Detection and Analysis

Security events are detected through:

- Wazuh alerts
- Sysmon events
- Suricata alerts
- Threat intelligence matches


## Common Lab Detections

### 1. Brute Force Attempts

Example:

Multiple failed authentication attempts.

Detection sources:

- Windows Security Logs
- Wazuh Rules


MITRE ATT&CK:
```
T1110-Brute Force
```
---

### 2. Network Reconnaissance

Example:

Port scanning from Kali Linux.

Tool:
nmap
Detection sources:

- Suricata
- Network logs


MITRE ATT&CK:
```
T1046-Network Service Discovery
```
---

### 3. Suspicious Process Execution

Example:

Unexpected PowerShell execution.

Detection sources:

- Sysmon Event ID 1
- Wazuh


MITRE ATT&CK:
```
T1059.001-PowerShell
```
---

### 4. Malicious File Detection

Example:

Suspicious executable created.

Detection sources:

- Sysmon
- Wazuh File Integrity Monitoring
- VirusTotal


---

# 5️⃣ Incident Investigation Process

When an alert is triggered:

## Step 1: Review Alert Details

Check:

- Alert severity
- Timestamp
- Source IP
- Destination IP
- Host involved
- Detection rule


---

## Step 2: Identify Source Activity

Determine:

- Source system
- User account
- Network connection
- Process involved


Classify activity:

- Expected
- Suspicious
- Malicious


---

## Step 3: Collect Evidence

Review:

### Wazuh

- Alert details
- Agent logs


### Windows

- Security logs
- Sysmon events


### Linux

- Authentication logs
- Suricata eve.json


---

## Step 4: Confirm Threat

Indicators:

- Repeated failed logins
- Unknown processes
- Suspicious network traffic
- Malicious hashes
- Unauthorized changes


---

# 6️⃣ Containment Procedures

Once malicious activity is confirmed:

## Endpoint Containment

Actions:

- Isolate affected host
- Block attacker IP
- Disable compromised accounts
- Stop malicious processes


---

## Network Containment

Actions:

- Block suspicious traffic
- Update firewall rules
- Restrict access


---

## Wazuh Active Response

Wazuh can automate:

- IP blocking
- Process termination
- Host response actions

---

# 7️⃣ Eradication

Remove the root cause.

Actions:

- Remove malicious files
- Terminate suspicious processes
- Reset credentials
- Patch vulnerabilities
- Update security rules


Verify:

- No persistence mechanisms remain
- Monitoring is active

---

# 8️⃣ Recovery

Restore normal operation.

Steps:

1. Re-enable services
2. Confirm system health
3. Monitor logs
4. Validate security controls


Continue monitoring through Wazuh.

---

# 9️⃣ Post Incident Review

Questions:

1. How was the attack detected?
2. Which tools generated alerts?
3. Was response time acceptable?
4. Were logs sufficient?
5. Are new detection rules required?


Document improvements.

---

# 🔟 Future Improvements

Planned enhancements:

- Complete AWS Traffic Mirroring integration
- Improve Suricata network visibility
- Add custom Wazuh detection rules
- Expand attack simulations
- Automate response actions
- Add additional threat intelligence sources


---

# ⚠️ Disclaimer

This project is for educational and research purposes only.
All attacks were simulated inside a controlled AWS lab environment.
No unauthorized systems or networks were targeted.
