# Web Application Vulnerability Assessment & Penetration Testing

> A hands-on web application security assessment performed against a deliberately vulnerable simulated web application in an isolated VirtualBox lab environment.

![VAPT](<https://img.shields.io/badge/Focus-Web%20Application%20Security-red>)
![OWASP](https://img.shields.io/badge/Security-VAPT-orange)
![Kali Linux](<https://img.shields.io/badge/Platform-Kali%20Linux-blue>)
![Nmap](https://img.shields.io/badge/Tool-Nmap-informational)
![Burp Suite](<https://img.shields.io/badge/Tool-Burp%20Suite-orange>)
![Gobuster](https://img.shields.io/badge/Tool-Gobuster-green)
![VirtualBox](https://img.shields.io/badge/Lab-VirtualBox-purple)

---

## 📌 Project Overview

This project demonstrates a controlled Vulnerability Assessment and Penetration Testing (VAPT) exercise against a deliberately vulnerable simulated web application.

The assessment was performed in an isolated virtual lab using Kali Linux and a vulnerable virtual machine. The objective was to perform reconnaissance, identify exposed services and application weaknesses, validate vulnerabilities through controlled exploitation, and document security findings with remediation recommendations.

The target application was a simulated **Travel Blog** web application hosted on the vulnerable virtual machine.

The project covered both infrastructure-level enumeration and web application security testing.

---

## 🎯 Objectives

The main objectives of this project were:

- Deploy a vulnerable web application in a controlled VirtualBox environment.
- Configure network connectivity between the attacker and target machines.
- Perform reconnaissance and service enumeration.
- Identify exposed network services and open ports.
- Assess FTP configuration and anonymous access.
- Enumerate web application directories and resources.
- Inspect publicly accessible files and application source code.
- Identify sensitive information exposure.
- Assess administrative application functionality.
- Intercept and analyze HTTP requests using Burp Suite.
- Validate identified security weaknesses.
- Document vulnerabilities, impact, exploitation evidence, and remediation recommendations.

---

## 🏗️ Lab Architecture

The assessment was performed using an isolated virtual network.

```text
                  ┌──────────────────────────┐
                  │       Kali Linux         │
                  │                          │
                  │  Reconnaissance          │
                  │  Nmap                    │
                  │  Gobuster                │
                  │  Burp Suite              │
                  │  FTP / HTTP Testing      │
                  └────────────┬─────────────┘
                               │
                               │
                        Isolated NAT Network
                               │
                               ▼
                  ┌──────────────────────────┐
                  │      Vulnerable VM       │
                  │                          │
                  │  Simulated Travel Blog   │
                  │  FTP Service             │
                  │  HTTP Service            │
                  │  Exposed Resources       │
                  │  Admin Panel             │
                  └──────────────────────────┘
```

Lab Environment

| Component         | Purpose                                |
| ----------------- | -------------------------------------- |
| Kali Linux        | Security testing / attacker machine    |
| Vulnerable VM     | Target application                     |
| Oracle VirtualBox | Virtualization                         |
| NAT Network       | Isolated lab connectivity              |
| Nmap              | Network and service enumeration        |
| Gobuster          | Web content/directory enumeration      |
| Burp Suite        | HTTP request interception and analysis |
| FTP Client / wget | FTP enumeration and file retrieval     |

🔎 Assessment Methodology

The assessment followed a structured penetration-testing workflow:

```text
Lab Deployment
      ↓
Network Configuration
      ↓
Reconnaissance
      ↓
Service Enumeration
      ↓
Web Enumeration
      ↓
Vulnerability Identification
      ↓
Controlled Exploitation
      ↓
Evidence Collection
      ↓
Risk Analysis
      ↓
Remediation Recommendations
```

**1. Lab Deployment**

The vulnerable virtual machine was imported into Oracle VirtualBox and connected to the dedicated NAT network.

The target machine hosted the simulated web application and other network services used during the assessment.

The target environment was assigned an internal lab IP address.

**2. Reconnaissance & Service Enumeration**

Nmap was used to perform reconnaissance against the target system.

```bash
nmap -A <TARGET-IP>
```

The scan was used to identify:

* Open ports
* Running services
* Service versions
* Potential attack surfaces

The scan revealed multiple accessible services, which were subsequently investigated during the vulnerability assessment.

3. FTP Security Assessment

The FTP service was tested to determine whether anonymous authentication was permitted.

```bash
ftp <TARGET-IP>
```

Anonymous access was available on the target.

This represented a significant security misconfiguration because unauthenticated users could interact with files exposed through the FTP service.

The assessment demonstrated that files could be retrieved from the FTP server.

For example:

```bash
wget -m --nopassive ftp://anonymous:anonymous@<TARGET-IP>
```

A sensitive test file was successfully retrieved from the FTP service.

Finding

Anonymous FTP Access Enabled

Risk: Sensitive files could potentially be accessed by unauthorized users.

Recommendation

* Disable anonymous FTP access.
* Require authenticated access.
* Restrict FTP access to trusted users/networks.
* Prefer secure alternatives such as SFTP where appropriate.
* Review exposed files and remove sensitive information from publicly accessible locations.

4. Web Application Assessment

The HTTP service was accessed to identify the hosted web application.

The target hosted a simulated Travel Blog website.

The application was manually browsed to identify accessible functionality and potential attack surfaces.

5. Web Directory Enumeration

Gobuster was used to discover directories and resources that were not immediately visible through normal application navigation.

```bash
gobuster dir \
-u http://<TARGET-IP>/ \
-w /usr/share/seclists/Discovery/Web-Content/common.txt \
-t 100
```

The enumeration identified additional application paths and resources.

This demonstrated the importance of restricting access to sensitive directories and files that are not intended to be publicly accessible.

6. Sensitive Information Exposure
   6.1 `robots.txt`

The assessment identified an accessible `robots.txt` file containing information that should not have been exposed to unauthenticated users.

This demonstrated that publicly accessible files can disclose information about application resources.

### Recommendation

* Avoid placing sensitive information in `robots.txt`.
* Treat `robots.txt` as a discovery aid rather than an access-control mechanism.
* Enforce server-side authorization for sensitive resources.

### 6.2 Exposed Configuration / Information Resource

An additional application path was discovered during enumeration:

```
/c0nf1g/
```

The resource exposed sensitive technical information through the web application.

The assessment demonstrated how improperly exposed configuration or diagnostic resources can provide useful information to attackers.

### Recommendation

* Remove unnecessary diagnostic/configuration resources from production.
* Restrict access to administrative and technical information.
* Disable unnecessary information disclosure.
* Apply appropriate authentication and authorization controls.




7. Source Code Information Disclosure

The HTML source code of publicly accessible pages was inspected using the browser's source-view functionality.

Sensitive information was discovered directly within the page source.

This demonstrates that information hidden from the normal visual interface is not actually protected if it is delivered to the client.

Security Impact

Attackers can inspect client-side source code to discover:

Hidden application information
Internal paths
Development artifacts
Embedded secrets or tokens
Application implementation details



### Recommendation

* Never store secrets or sensitive information in client-side HTML/JavaScript.
* Remove debugging information from production applications.
* Perform proper server-side authorization.
* Review client-side assets during security testing.



8. Administrative Panel Assessment

A dedicated administrative endpoint was identified:

```
/4dm1n/
```


The page exposed an administrative login interface.

Further inspection of the application's source code revealed sensitive information associated with the administrative functionality.

This demonstrated weaknesses in the application's access-control and information-disclosure controls.

### Recommendation

* Protect administrative endpoints with strong authentication.
* Implement authorization checks server-side.
* Enforce MFA for privileged accounts.
* Restrict administrative interfaces by network or identity where appropriate.
* Avoid exposing sensitive implementation details through client-side resources.


9. HTTP Request Interception with Burp Suite

Burp Suite was configured to intercept traffic generated by the administrative section of the application.

The intercepted HTTP request was inspected before being forwarded to the application.


```
Browser
   ↓
Burp Suite Proxy
   ↓
HTTP Request Inspection
   ↓
Target Web Application
```



This demonstrated how an attacker can inspect and manipulate client-server communication during a web application security assessment.

### Security Testing Value

Burp Suite can be used to identify:

* Weak authentication mechanisms
* Missing authorization controls
* Sensitive parameters
* Insecure request handling
* Session-management weaknesses
* Application logic issues

# 🔎 Key Findings

The assessment identified several security weaknesses in the simulated application environment.

| Finding                                                     | Category                  | Impact                              |
| ----------------------------------------------------------- | ------------------------- | ----------------------------------- |
| Anonymous FTP access                                        | Security Misconfiguration | Unauthorized file access            |
| Sensitive data in HTML source                               | Information Disclosure    | Exposure of application information |
| Exposed`robots.txt`resources                              | Information Disclosure    | Application/resource discovery      |
| Exposed configuration/diagnostic resource                   | Security Misconfiguration | Technical information disclosure    |
| Weak administrative access controls                         | Broken Access Control     | Unauthorized access risk            |
| Publicly discoverable directories                           | Security Misconfiguration | Increased attack surface            |
| Sensitive information exposed through client-side resources | Information Disclosure    | Information leakage                 |

# 🛠️ Remediation Recommendations


### FTP Security

* Disable anonymous FTP access.
* Require strong authentication.
* Restrict access to trusted users and networks.
* Prefer secure file-transfer protocols where applicable.

### Web Application Security

* Implement proper authentication and authorization.
* Protect administrative endpoints.
* Remove sensitive information from client-side source code.
* Restrict access to configuration and diagnostic resources.

### Server Configuration

* Disable unnecessary directory listing.
* Remove unnecessary files and services.
* Apply least-privilege access controls.
* Regularly review exposed services and resources.

### Secure Development

* Never embed secrets in HTML, JavaScript, or other client-side resources.
* Perform security testing during development.
* Conduct regular vulnerability assessments.
* Keep server software and application components updated.


# 📄 Project Report

The complete course-end project report containing the detailed lab procedure, screenshots, testing steps, findings, and recommendations is available here:

**[View Complete Project Report (PDF)](./project-report/Conducting%20Vulnerability%20Assessment%20and%20Penetration%20Testing%20on%20a%20Simulated%20Web%20Application%20Environment.pdf)**



# 📚 Skills Demonstrated

* Web Application Security
* Vulnerability Assessment
* Penetration Testing
* Reconnaissance
* Network Enumeration
* Service Enumeration
* FTP Security Assessment
* Web Directory Enumeration
* Information Disclosure Analysis
* Access Control Assessment
* HTTP Request Analysis
* Burp Suite
* Nmap
* Gobuster
* Kali Linux
* Linux
* Security Reporting
* Vulnerability Remediation
