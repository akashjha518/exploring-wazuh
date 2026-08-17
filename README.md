# TryHackMe — Exploring Wazuh

Hands-on documentation for the TryHackMe room **Exploring Wazuh**.

- **Platform:** TryHackMe
- **Room:** Exploring Wazuh
- **Focus:** Wazuh SIEM/XDR capabilities, agent inventory, configuration assessment, vulnerability visibility, and dashboard analysis
- **Documented lab progress:** 42% at the time of capture
- **Evidence:** `evidence/`

## 1. Lab Objective

The lab introduces Wazuh as an open-source security platform and provides practical exposure to:

- Wazuh agents and agent status
- Security Configuration Assessment (SCA)
- CIS benchmark results
- IT Hygiene / software inventory
- Vulnerability Detection
- Security monitoring dashboards
- Endpoint security visibility

The goal of this documentation is to record the work completed in the lab with screenshots and concise technical notes.

## 2. Lab Environment

The supplied TryHackMe environment contains Wazuh dashboard access and two monitored endpoints:

| Endpoint | Observed details |
|---|---|
| Linux agent | Ubuntu Linux 24.04 LTS CIS benchmark |
| Windows agent | Microsoft Windows Server 2019 Datacenter |
| Windows agent ID | `002` |
| Windows agent IP | `10.82.99.206` |
| Wazuh version observed | `v4.14.3` |
| Windows CPU | `AMD EPYC 7571` |
| Windows memory | `4 GB` |
| Windows cores | `2` |

> The values above are taken from the supplied lab screenshots and describe the lab environment at capture time.

## 3. Key Lab Findings

### 3.1 Linux — Security Configuration Assessment

The Linux agent was opened in **Configuration Assessment**.

Observed CIS benchmark:

**CIS Ubuntu Linux 24.04 LTS Benchmark v1.0.0**

Results:

- Passed: **110**
- Failed: **127**
- Not applicable: **42**
- Score: **46%**
- Total checks: **279**
- Scan date shown: **March 10, 2026**

The dashboard also showed individual SCA checks, including kernel-module hardening checks. Several checks passed while at least one unused-filesystem check was shown as failed.

**Learning point:** SCA compares endpoint configuration against predefined security policies and benchmarks. Wazuh provides built-in policies based largely on CIS benchmarks.

### 3.2 Windows — IT Hygiene / Software Inventory

The Windows agent's **IT Hygiene → Software → Packages** view was inspected.

Observed:

- **9 unique packages**
- Package type: `win`
- Microsoft Visual C++ Redistributables
- AWS PV Drivers
- Amazon SSM Agent
- `aws-cfn-bootstrap`
- AWS Tools for Windows
- Wazuh Agent
- Notepad++ Team was visible in the vendor list

The lab question asking for the custom text editor installed on the Windows agent was answered:

**Notepad++**

### 3.3 Windows — Agent Details

The Windows endpoint page showed:

- Agent ID: `002`
- Status: **Disconnected**
- IP address: `10.82.99.206`
- Wazuh version: `v4.14.3`
- Operating system: **Microsoft Windows Server 2019 Datacenter 10.0.17763.1821**
- Host name: `WIN-SERVER`
- CPU: **AMD EPYC 7571**
- Memory: **4 GB**
- Cores: **2**
- Cluster node: `node01`

The lab question asking for the status of the agents managed by this Wazuh instance was answered:

**Disconnected**

The CPU question was answered:

**AMD EPYC 7571**

### 3.4 Windows — CIS Benchmark

The Windows Configuration Assessment page showed:

**CIS Microsoft Windows Server 2019 Benchmark v2.0.0**

Observed results:

- Passed: **85**
- Failed: **262**
- Not applicable: **0**
- Score: **24%**
- Total checks: **347**

This demonstrates how Wazuh can expose configuration weaknesses against a standardized CIS benchmark.

### 3.5 Wazuh Overview

The Wazuh overview dashboard was captured showing security monitoring categories including:

- Configuration Assessment
- Malware Detection
- Threat Hunting
- Vulnerability Detection
- File Integrity Monitoring
- MITRE ATT&CK
- IT Hygiene
- PCI DSS
- Docker
- Amazon Web Services

One captured dashboard state showed:

- Active agents: `0`
- Disconnected agents: `2`
- Critical alerts: `0`
- High alerts: `0`
- Medium alerts: `15`
- Low alerts: `1`

Another lab-provided environment screenshot showed a healthy state with two active agents and no disconnected agents. This demonstrates that dashboard values depend on the current lab state and should not be treated as permanent configuration.

## 4. Answers Recorded

| Lab question | Answer |
|---|---|
| What custom text editor is installed? | **Notepad++** |
| What is the Linux agent CIS Benchmark score? | **46%** |
| What is the status of the managed agents in the captured state? | **Disconnected** |
| What is the Windows agent CPU field value? | **AMD EPYC 7571** |

## 5. What I Learned

### Wazuh Security Configuration Assessment

SCA checks endpoint configuration against policy files. Wazuh ships with policies based on established benchmarks such as CIS. Results can be reviewed as passed, failed, or not applicable checks.

### System / Software Inventory

Wazuh's Syscollector collects endpoint inventory such as operating system, hardware, packages, network information, processes, users, services, and other system properties. This inventory is useful for asset visibility and vulnerability management.

### Vulnerability Detection

Wazuh correlates software inventory from monitored endpoints with vulnerability intelligence to identify vulnerable software and generate findings. This makes software inventory an important input to vulnerability management.

### SOC / Blue-Team Relevance

The lab connects several common defensive security activities:

`Asset Visibility → Configuration Assessment → Vulnerability Detection → Security Monitoring → Investigation`

## 6. Evidence

All screenshots supplied for this documentation are stored in the [`evidence/`](./evidence/) directory.

### Evidence index

1. `01-wazuh-linux-sca-46-percent.png` — Linux CIS benchmark and 46% score
2. `02-wazuh-windows-it-hygiene-packages.png` — Windows software/package inventory
3. `03-wazuh-windows-agent-overview.png` — Windows endpoint details
4. `04-wazuh-overview-dashboard-disconnected-agents.png` — Wazuh overview and alert summary
5. `05-tryhackme-windows-benchmark.png` — Windows CIS benchmark results
6. `06-tryhackme-windows-agent-questions.png` — Completed TryHackMe questions
7. `07-tryhackme-lab-machine-setup.png` — Lab machine setup
8. `08-tryhackme-room-progress-42-percent.png` — TryHackMe room progress
9. `09-wazuh-overview-dashboard.png` — Wazuh overview dashboard

## 7. References

- TryHackMe: [Exploring Wazuh](https://tryhackme.com/room/exploringwazuh)
- Wazuh documentation: Security Configuration Assessment
- Wazuh documentation: System Inventory
- Wazuh documentation: Vulnerability Detection

## 8. Disclaimer

This repository contains personal learning notes and screenshots from an authorized TryHackMe training environment. It is intended for cybersecurity education and portfolio documentation.
