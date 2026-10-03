# SonarQube-Based Static Application Security Testing (SAST) of DVWA

## Course Context

This lab was completed as part of my Cyber Security learning journey, focusing on **Application Security, Static Application Security Testing (SAST), Secure SDLC, and vulnerability identification**.

The lab demonstrates how SonarQube can be configured and used to perform static security analysis against the source code of **Damn Vulnerable Web Application (DVWA)**.

---

## Objective

The objective of this lab is to configure SonarQube and scan the source code of a vulnerable web application (DVWA) to perform a detailed security analysis.

The exercise focuses on identifying security issues such as **unsafe dynamic code execution and insecure permissions**, understanding their security impact, and gaining hands-on experience in analyzing and interpreting SAST scan results.

---

## Overview

In this lab, I performed an end-to-end SAST assessment of the DVWA source code using **SonarQube**.

The lab involved:

- Downloading the DVWA source code
- Installing Java 21
- Setting up SonarQube
- Starting the SonarQube server
- Creating a local SonarQube project
- Generating a project analysis token
- Installing and configuring SonarQube Scanner CLI
- Running a static analysis against the DVWA source code
- Reviewing the generated SonarQube results
- Investigating identified security issues
- Understanding the security impact of the findings

---

## Objectives

- Understand the fundamentals of Static Application Security Testing (SAST)
- Configure and run SonarQube locally
- Perform static analysis against vulnerable application source code
- Identify security issues through automated source-code analysis
- Investigate code injection-related findings
- Investigate insecure permission-related findings
- Understand how SAST can support Secure SDLC practices
- Gain practical experience interpreting SonarQube security findings

---

## Lab Environment

| Component        | Details                                |
| ---------------- | -------------------------------------- |
| Operating System | Windows Server 2022                    |
| Application      | Damn Vulnerable Web Application (DVWA) |
| SAST Platform    | SonarQube                              |
| Scanner          | SonarQube Scanner CLI                  |
| Java             | Java 21                                |
| Browser          | Web Browser                            |
| Target           | DVWA Source Code                       |

---

## Tools & Technologies

- **SonarQube**
- **SonarQube Scanner CLI**
- **Java 21**
- **DVWA**
- **Windows Server 2022**
- **PowerShell**
- **Static Application Security Testing (SAST)**
- **Secure SDLC**

---

# Methodology

### 1. Download DVWA Source Code

The DVWA source code was downloaded and extracted on the Windows Server environment.

DVWA was selected as the target application because it is intentionally vulnerable and provides a suitable environment for practicing application security testing.

---

### 2. Install Java 21

Java 21 was installed as one of the required dependencies for running the SonarQube environment.

The lab documentation specifies Java 21 as the required Java version.

---

### 3. Setup SonarQube

The SonarQube package was downloaded and extracted.

The SonarQube installation directory was then accessed through:

```text
Downloads\sonarqube-*.*.*\sonarqube-*.*.*\bin\windows-x86-64
```
PowerShell was opened inside the `windows-x86-64` directory.
SonarQube was started using:
```powershell
.\StartSonar.bat
```
After the server started successfully, the SonarQube web interface was accessed through:
```
http://localhost:9000
```
The default credentials specified in the lab were:
```
Username: admin
Password: admin
```

---

### 4. Create a SonarQube Project
A local project was created in the SonarQube interface for analyzing the DVWA source code.
The project was configured so that SonarQube could associate the scanner analysis results with the DVWA project.

---

### 5. Generate Project Token
A project analysis token was generated from the SonarQube project configuration.
The token was required for authenticating the SonarQube Scanner while sending the analysis results to the SonarQube server.
**Security Note**: Project tokens should be treated as secrets and should never be committed to a public GitHub repository.

---

### 6. Configure SonarQube Scanner
The SonarQube Scanner CLI was downloaded for Windows x64 and extracted.
The scanner directory was accessed and the required scanner files were configured for performing the DVWA analysis.
The DVWA source code was copied into the scanner's bin directory as specified in the lab procedure.

---

### 7. Configure the Analysis Command
The SonarQube analysis command generated from the SonarQube project setup was modified to include the source-code path of the DVWA application.
The modified command was then copied and executed from PowerShell inside the scanner directory.
The scanner performed static analysis against the DVWA source code and uploaded the results to the local SonarQube server.

---

### 9. Review SonarQube Overview
The SonarQube Overview page displayed the results of the source-code analysis.
The project dashboard provided an overview of the analysis status and identified issues requiring further investigation.
This demonstrated how SAST tools can provide centralized visibility into security issues discovered during source-code analysis.

---

### Findings Summary
| Finding | File | Security Relevance |
|---|---|---|
| Make sure that this dynamic injection or execution of code is safe | `dvwa/dvwa/js/dvwaPage.js` | Potential unsafe dynamic code execution / injection |
| Make sure this permission is safe | `dvwa/../htmlpurifier/HTMLPurifier/DefinitionCache/Serializer.php` | Potential insecure permission configuration |

---

## 10. Investigate Dynamic Code Execution Issue
One of the identified SonarQube issues was:
```
Make sure that this dynamic injection or execution of code is safe
```
SonarQube highlighted the issue in:
```
dvwa/dvwa/js/dvwaPage.js
```
The finding demonstrates how SAST can identify potentially unsafe patterns involving dynamic code injection or execution.
Such findings require developers or security engineers to review the relevant code and determine whether the dynamic behavior is controlled and safe.

---

### 11. Investigate Permission-Related Issue
Another SonarQube issue identified during the scan was:
```
Make sure this permission is safe
```
The issue was identified in:
```
dvwa/../htmlpurifier/HTMLPurifier/DefinitionCache/Serializer.php
```
The lab identifies the relevant location at:
```
Line 122
```
This finding demonstrates how static analysis can identify potentially unsafe permission-related behavior in application code.

---

## Security Relevance
Static Application Security Testing is an important component of a secure software development lifecycle because it allows security issues to be identified by analyzing source code before the application reaches production.
In this lab, SonarQube was used to automatically analyze vulnerable application source code and highlight areas requiring security review.
The exercise demonstrates the practical value of integrating automated security analysis into development and code-review processes.

---

## Security Concepts Demonstrated
### Static Application Security Testing (SAST)
Analyzing application source code to identify potentially vulnerable or insecure coding patterns.
### Secure SDLC
Integrating security testing and code analysis into the software development lifecycle.
### Code Injection
Understanding how dynamically executed or injected code can introduce application security risks.
### Permission Security
Reviewing file or application permissions to identify potentially unsafe configurations.
### Vulnerability Identification
Using automated security tooling to identify areas of source code that require further investigation.
### Security Code Review
Reviewing flagged source-code locations to understand the underlying security issue and its potential impact.

---

## Observations / Results
The SonarQube SAST analysis successfully processed the DVWA source code and generated security findings.
Key observations from the lab:
- SonarQube was successfully configured and executed locally.
- DVWA source code was successfully analyzed.
- The SonarQube project dashboard displayed the analysis results.
- SonarQube identified a potential dynamic code injection/execution issue.
- The issue was associated with:

```
dvwa/dvwa/js/dvwaPage.js
```
- SonarQube also identified a permission-related issue.
- The permission-related issue was associated with:
```
dvwa/../htmlpurifier/HTMLPurifier/DefinitionCache/Serializer.php
```
- The analysis demonstrated how SAST tools can assist in identifying security weaknesses during the development lifecycle.

---

## Key Learnings
- Learned how to configure SonarQube for local SAST analysis.
- Learned how to use SonarQube Scanner CLI to analyze source code.
- Gained practical experience performing SAST against DVWA.
- Learned how automated source-code analysis can identify potentially insecure coding patterns.
- Learned how to investigate SonarQube security findings at specific source-code locations.
- Improved understanding of code injection and permission-related security risks.
- Understood the role of automated security testing in the Secure SDLC.
- Gained hands-on experience with interpreting SAST results rather than only running a security scanner.

---

## Project Outcome
Successfully completed an end-to-end SonarQube-based Static Application Security Testing (SAST) assessment of DVWA.
The lab provided practical experience in:
```
Source Code
     ↓
SonarQube Scanner
     ↓
Static Analysis
     ↓
Security Findings
     ↓
Source-Code Investigation
     ↓
Security Impact Analysis
```
The exercise strengthened practical knowledge of **Application Security, SAST, vulnerability identification, secure coding, and Secure SDLC practices.**

---

[View the complete lab report (PDF)](./lab-report/Lab_SonarQube_Based_Static_Application_Security_Testing_(SAST)_of_DVWA.pdf)
