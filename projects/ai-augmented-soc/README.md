The lab therefore provides hands-on exposure to both **SOC operations** and the broader  **security-engineering lifecycle** .

This provides a structured way to prioritize defensive improvements.

# AI-Augmented SOC Implementation for Enterprise Threat Detection & Response

> A hands-on cybersecurity lab demonstrating the design and implementation of a mini Security Operations Center (SOC) using SIEM, network monitoring, AI-assisted log analysis, SOAR automation, threat hunting, and security-control mapping.

![SOC](<https://img.shields.io/badge/Focus-Security%20Operations%20Center-red>)
![SIEM](https://img.shields.io/badge/SIEM-Splunk-orange)
![Network Monitoring](<https://img.shields.io/badge/Network%20Monitoring-Zeek-blue>)
![AI](https://img.shields.io/badge/AI-LogAI-purple)
![SOAR](https://img.shields.io/badge/SOAR-Shuffle-green)
![Linux](https://img.shields.io/badge/Platform-Linux-yellow)
![Windows Server](<https://img.shields.io/badge/Platform-Windows%20Server%202022-blue>)
![VirtualBox](https://img.shields.io/badge/Lab-Virtualization-lightgrey)

---

## 📌 Project Overview

This project demonstrates the implementation of a mini Security Operations Center (SOC) designed to support enterprise-style threat detection and response.

The lab combines multiple security technologies to create a workflow for:

- Collecting and ingesting security logs
- Centralizing security telemetry using Splunk
- Monitoring network activity using Zeek
- Applying AI-assisted analysis to security logs
- Performing threat hunting and IOC-based investigation
- Automating security operations using SOAR
- Mapping security controls to MITRE ATT&CK and D3FEND concepts
- Identifying security-control gaps
- Measuring defensive control coverage

The project was implemented in a controlled virtual lab environment using Windows Server, Linux-based systems, Kali Linux, Splunk, Zeek, Salesforce LogAI, and Shuffle.

---

## 🎯 Objectives

The primary objectives of this project were:

1. Build a mini SOC environment for security monitoring.
2. Collect and centralize logs using Splunk.
3. Configure log forwarding from a Linux system to Splunk.
4. Detect failed authentication activity through security logs.
5. Deploy Zeek for network security monitoring.
6. Apply AI-assisted log analysis using Salesforce LogAI.
7. Perform threat hunting and investigate Indicators of Compromise (IOCs).
8. Deploy Shuffle as a SOAR platform.
9. Map security controls to D3FEND techniques.
10. Identify gaps in defensive coverage.
11. Calculate overall security-control coverage.
12. Create dashboards for security visibility and analysis.

---

## 🏗️ SOC Architecture

The project follows a simplified SOC architecture:

```text
                         ┌─────────────────────────┐
                         │      Security Events    │
                         │                         │
                         │ Authentication Logs     │
                         │ System Logs             │
                         │ Network Activity        │
                         └────────────┬────────────┘
                                      │
                                      ▼
                         ┌─────────────────────────┐
                         │     Log Collection      │
                         │                         │
                         │   Splunk Forwarder      │
                         │   Zeek                  │
                         └────────────┬────────────┘
                                      │
                                      ▼
                         ┌─────────────────────────┐
                         │          Splunk         │
                         │                         │
                         │ SIEM / Log Management   │
                         │ Search & Correlation    │
                         │ Reports & Dashboards    │
                         └────────────┬────────────┘
                                      │
                         ┌────────────┴────────────┐
                         │                         │
                         ▼                         ▼
              ┌───────────────────┐     ┌────────────────────┐
              │ AI-Assisted        │     │ Threat Hunting     │
              │ Log Analysis       │     │ & IOC Investigation│
              │                    │     │                    │
              │ Salesforce LogAI   │     │ Correlation        │
              └─────────┬─────────┘     └──────────┬─────────┘
                        │                          │
                        └────────────┬─────────────┘
                                     ▼
                         ┌─────────────────────────┐
                         │         SOAR            │
                         │                         │
                         │       Shuffle           │
                         │ Automation / Response   │
                         └────────────┬────────────┘
                                      │
                                      ▼
                         ┌─────────────────────────┐
                         │ Security Control        │
                         │ Mapping & Gap Analysis  │
                         │                         │
                         │ MITRE ATT&CK / D3FEND   │
                         └─────────────────────────┘
```

## 🧪 Lab Environment

| Component                  | Purpose                                             |
| -------------------------- | --------------------------------------------------- |
| Windows Server 2022        | Splunk Enterprise / SIEM                            |
| Linux / Ubuntu             | Log generation and security telemetry               |
| Kali Linux                 | Security analysis and threat-hunting environment    |
| Splunk Enterprise          | Log aggregation, search, correlation and dashboards |
| Splunk Universal Forwarder | Log forwarding                                      |
| Zeek                       | Network security monitoring                         |
| Salesforce LogAI           | AI-assisted log analysis                            |
| Shuffle                    | Security orchestration and automation               |
| Docker / Docker Compose    | Shuffle deployment                                  |
| MITRE ATT&CK / D3FEND      | Threat and defensive-control mapping                |

## 1. Centralized Log Collection with Splunk

   The first phase focused on building the SOC's centralized logging capability.

   Splunk Enterprise was deployed on Windows Server 2022 and configured to receive security telemetry.

   A Splunk Universal Forwarder was configured on the Linux environment to forward system and authentication logs to the Splunk server.

   The project monitored log sources including:

```
/var/log/auth.log
/var/log/syslog
/var/log/secure
/var/log
```

The forwarded data was then made available for investigation through Splunk Search & Reporting.

## 🔎 Authentication Event Detection

Splunk was used to search authentication events and identify failed login attempts.

Example search:

```
index="main" "Failed Password"
```

The project also created a report to summarize failed authentication activity by host.

This demonstrates a basic SOC detection workflow:

```
Authentication Event
        ↓
Log Collection
        ↓
Splunk Ingestion
        ↓
Search / Correlation
        ↓
Detection
        ↓
Security Investigation
```

## 2.Network Security Monitoring with Zeek

The second phase introduced Zeek as a network security monitoring component.

Zeek was installed in an Ubuntu environment and configured as part of the SOC lab.

Zeek provides network telemetry that can be used to investigate:

* Network connections
* Protocol activity
* Suspicious network behavior
* Hosts and communication patterns
* Security events

This adds network visibility alongside host-based log monitoring.

## 3. AI-Assisted Log Analysis

The project incorporated Salesforce LogAI to demonstrate AI-assisted security log analysis.

LogAI was installed in a Python virtual environment and configured with its analysis components.

The LogAI interface was used to support analysis capabilities including:

* Log pattern analysis
* Anomaly analysis
* Log clustering
* Security-event investigation

The overall workflow was:

```
Security Logs
      ↓
Preprocessing
      ↓
AI-Assisted Analysis
      ↓
Pattern / Anomaly Identification
      ↓
Security Investigation
```

The purpose of the AI component is to augment traditional SOC analysis rather than replace analyst investigation.

## 4. Threat Hunting & IOC Investigation

The project included a threat-hunting phase focused on investigating Indicators of Compromise (IOCs).

The workflow combines:

* Security logs
* Network telemetry
* Log analysis
* IOC investigation
* Correlation
* Analyst-driven investigation

A simplified investigation workflow is:

```
Security Event
      ↓
Identify Suspicious Activity
      ↓
Extract IOC
      ↓
Pivot Across Available Telemetry
      ↓
Correlate Events
      ↓
Determine Potential Threat
      ↓
Response / Mitigation
```

This demonstrates the relationship between SIEM data, network telemetry, AI-assisted analysis, and security investigation.

## 5. SOAR Implementation with Shuffle

The fourth phase introduced Shuffle as the Security Orchestration, Automation and Response (SOAR) component.

Shuffle was deployed using Docker and Docker Compose.

```
Security Event
      ↓
Detection / Investigation
      ↓
SOAR Workflow
      ↓
Automated Security Action
      ↓
Response
```

SOAR can help reduce repetitive manual work by integrating security tools and automating predefined response workflows.

The project used Shuffle to demonstrate the integration of security operations with an orchestration layer.

## 6. Security Control Mapping

The project also included security-control mapping using D3FEND-related data.

Security controls were mapped against defensive techniques to determine whether specific defensive capabilities were covered.

The workflow included:

```
Security Controls
        ↓
Control-to-Technique Mapping
        ↓
D3FEND Techniques
        ↓
Coverage Analysis
        ↓
Identify Defensive Gaps
```

Splunk lookup tables were used to correlate:

* Security controls
* Attack mitigation mappings
* D3FEND techniques
* Defensive categories

## 7. Security Gap Analysis

The project identified defensive techniques that were not adequately covered by the available security controls.

The analysis classified techniques based on whether corresponding controls were present.

Example concept:

```
Control Available
       ↓
     Covered

Control Missing
       ↓
      Gap
```

This provides a structured way to prioritize defensive improvements.

# 8. Security Coverage Calculation

The project also calculated the percentage of defensive techniques covered by the available controls.

The calculation was performed using Splunk queries against the D3FEND and control-inventory datasets.

The resulting coverage metric provides a high-level measurement of defensive readiness.

```
Total Defensive Techniques
              ↓
       Compare Controls
              ↓
      Covered vs Gaps
              ↓
       Coverage %
```

# 🔐 Security Operations Workflow

The complete project workflow can be summarized as:

```
             ┌─────────────────┐
             │ Security Events │
             └────────┬────────┘
                      ↓
             ┌─────────────────┐
             │ Log Collection  │
             │ + Network Data  │
             └────────┬────────┘
                      ↓
             ┌─────────────────┐
             │      SIEM       │
             │     Splunk      │
             └────────┬────────┘
                      ↓
          ┌───────────┴───────────┐
          ↓                       ↓
 ┌────────────────┐      ┌────────────────┐
 │ AI-Assisted    │      │ Threat Hunting │
 │ Log Analysis   │      │ & IOC Analysis │
 │    LogAI       │      │                │
 └───────┬────────┘      └───────┬────────┘
          └───────────┬───────────┘
                      ↓
             ┌─────────────────┐
             │ SOAR Automation │
             │    Shuffle      │
             └────────┬────────┘
                      ↓
             ┌─────────────────┐
             │ Control Mapping │
             │  & Gap Analysis│
             └─────────────────┘
```

# 📊 Key Capabilities Demonstrated



This project demonstrates practical exposure to:

* Security Operations Center workflows
* SIEM implementation
* Centralized log management
* Security event investigation
* Authentication-event detection
* Network security monitoring
* AI-assisted log analysis
* Threat hunting
* IOC investigation
* Security event correlation
* SOAR concepts
* Security automation
* MITRE ATT&CK concepts
* MITRE D3FEND concepts
* Defensive-control mapping
* Security gap analysis
* Security coverage measurement
* Linux security monitoring
* Windows Server security monitoring
* Docker-based security tooling

# 🛠️ Tools & Technologies

| Category               | Technologies                                       |
| ---------------------- | -------------------------------------------------- |
| SIEM                   | Splunk Enterprise                                  |
| Log Collection         | Splunk Universal Forwarder                         |
| Network Monitoring     | Zeek                                               |
| AI / Log Analysis      | Salesforce LogAI                                   |
| SOAR                   | Shuffle                                            |
| Containerization       | Docker, Docker Compose                             |
| Operating Systems      | Windows Server 2022, Ubuntu, Kali Linux            |
| Threat Framework       | MITRE ATT&CK                                       |
| Defensive Framework    | MITRE D3FEND                                       |
| Scripting / Automation | Bash, Python                                       |
| Security Analysis      | IOC investigation, log correlation, threat hunting |

# 🔎 Key Takeaways



The project demonstrates how multiple security technologies can be combined into a SOC workflow rather than operating as isolated tools.

The implementation connects:

```
Visibility
   ↓
Detection
   ↓
Investigation
   ↓
Threat Hunting
   ↓
Automation
   ↓
Defensive Control Analysis
```

The lab therefore provides hands-on exposure to both **SOC operations** and the broader  **security-engineering lifecycle** .

# 📄 Project Report


The complete course-end project report containing the detailed implementation steps, screenshots, configuration procedures, analysis, and final results is available here:

**[View Complete Project Report (PDF)](./project-report/AI-Augmented%20SOC%20Implementation%20for%20Enterprise%20Threat%20Detection%20and%20Response.pdf)**
