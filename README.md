# 🛡️SOC Detection Lab - Wazuh, Sysmon & Suricata

## Overview

> This project is a cloud-based Security Operations Center (SOC) detection lab designed to simulate real-world cyber attacks, collect security telemetry, and investigate alerts using open-source security tools.

*Know More About AWS Penetration Test Before Starting This ProjecT*:

<a href="https://aws.amazon.com/security/penetration-testing/">
<img src="https://img.shields.io/badge/AWS-Penetration%20Testing-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white">
</a>


The lab demonstrates:

- Endpoint monitoring
- Network visibility
- Threat detection
- Log analysis
- Incident response workflows
- Security alert investigation


## Objectives

The objectives of this lab were:

- Deploy a centralized security monitoring platform
- Collect endpoint telemetry from Windows and Linux systems
- Simulate attacker behavior from Kali Linux
- Generate security alerts
- Investigate detected activities
- Document incident response procedures


# Lab Architecture


Components:

## Wazuh Manager

Role:
- Centralized SIEM/XDR platform
- Alert processing
- Rule detection
- Log analysis


## Windows Server

Tools:

- Wazuh Agent
- Sysmon

Purpose:

Collect:

- Authentication events
- Process creation
- PowerShell activity
- Network connections
- File changes


## Linux Sensor

Tools:

- Suricata
- Wazuh Agent

Purpose:

- Network traffic monitoring
- IDS detection
- Network event logging


## Kali Linux

Purpose:

Attack simulation:

- Reconnaissance
- Brute force testing
- Enumeration


# Integrated Security Tools


## Wazuh

Used for:

- SIEM monitoring
- Endpoint detection
- Log collection
- Alert generation


Capabilities:

- Windows event monitoring
- File Integrity Monitoring
- Custom detection rules
- Threat intelligence integration


---

## Sysmon

Microsoft Sysinternals tool used for detailed Windows telemetry.


Events monitored:

Event ID 1:
- Process creation


Event ID 3:
- Network connections


Event ID 7:
- Image loaded


Event ID 10:
- Process access


Event ID 11:
- File creation


Event ID 22:
- DNS queries


---

## Suricata

Network Intrusion Detection System.

Collected:

- Network flows
- Protocol activity
- IDS alerts

Logs:

```bash
 /var/log/suricata/eve.json
```
Note: For Suricata
Traffic Mirror: Working ✅
Attack Detection: Partial ⚠️

---

## VirusTotal Integration

Integrated with Wazuh to enrich file events using threat intelligence.

Workflow:

File change detected

↓

Wazuh Syscheck calculates hash

↓

VirusTotal checks hash

↓

Detection appears in Wazuh


---

# Attack Simulations


## 1. RDP Brute Force

Attack:

Kali Linux

Target:

Windows Server


Example:

```bash
 hydra -l Administrator -P passwords.txt rdp:// TARGET_IP
```

Detected by:

- Windows Security Logs
- Wazuh rules
- Authentication monitoring


MITRE:

T1110 - Brute Force


---

## 2. Network Reconnaissance


Tool:

Nmap


Command:

```bash
 nmap -sS TARGET_IP
```
Detected by:

- Suricata
- Network logs


MITRE:

T1046 - Network Service Discovery


---

## 3. PowerShell Activity


Command:

```bash
 powershell.exe
```

Detected by:

- Sysmon
- Wazuh


MITRE:

T1059.001 - PowerShell


---

# Detection Flow

```yaml
Attack

  ↓

Kali Linux

  ↓

Windows/Linux Endpoint

  ↓

Wazuh Agent / Suricata

  ↓

Wazuh Manager

  ↓

Dashboard Alert

  ↓

Investigation

  ↓

Response
```


# Skills Demonstrated

- SOC monitoring
- SIEM deployment
- Threat detection
- Log analysis
- Incident response
- MITRE ATT&CK mapping
- Cloud security


# Repository Contents

This repository contains:

- Installation guides
- Configurations
- Attack simulations
- Detection examples
- Investigation notes
- Incident response playbook


## Incident Response Documentation

The complete incident response workflow is available here:

[Incident Response Playbook](./Incident-Response-Playbook.md)

## Trouble Shooting Guide File

Yep alot of issues was encounter while building this Lab, so here is a clear Troubleshooting Guide:

[TroubleShooting-Guide](./Troubleshooting(Important-command).md)

## Paths To Each Repository:

[Network-Architecture](../Architecture/network-design.md)

[Suricata](Architecture/network-design.md)

[VirusTotal]()

[Wazuh-FIM]()

## Repository Architecture:

```
AWS-AegisSOC-Monitoring-Lab/
│
├── README.md
│
├── Incidect-Response-Playbook.md
│
├── Troubleshooting(Important-command).md
│
├── Architecture/
│   ├── Image  
│   └── network-design.md
│
├── Suricata/
│   ├── Image
│   ├── Installation.md
│   └── configuration.md
│   
│
├── virustotal/
│   ├── Image
│   └── FIM-Malware-Detection.md
│
└── Wazuh/
   ├── Image
   ├── Installation-guide-onAWS.md
   └── configuration.md
```

## ⚠️ Disclaimer
> All experiments in this repository were conducted in a controlled lab environment for educational and research purposes only.
  No real systems or networks were targeted.
