# Linux Server Hardening, SSH Attack Monitoring & Automated IP Blocking

## Overview

This project documents a hands-on defensive cybersecurity lab focused on detecting SSH brute-force activity, monitoring authentication failures, hardening SSH configuration, analyzing attack data, and automatically blocking suspicious IP addresses.

The lab was performed in a controlled virtualized environment using **CentOS Stream 9** and **Kali Linux**. The project demonstrates the complete workflow from Linux server setup and SSH attack simulation to log analysis, security hardening, automated reporting, and IP blocking.

> **Scope:** Authorized educational lab environment only. No real-world or unauthorized systems were targeted.

---

## Objectives

- Build a controlled Linux security lab using CentOS Stream 9 and Kali Linux.
- Configure an SSH-enabled CentOS server.
- Deploy the services required for the lab environment.
- Simulate failed SSH authentication attempts from Kali Linux.
- Monitor failed SSH authentication events using Linux security logs.
- Extract attacker IP addresses from authentication logs.
- Generate daily and user-wise SSH attack reports.
- Harden the SSH configuration.
- Move SSH from the default port to a custom port.
- Configure SELinux to support the custom SSH port.
- Analyze attacker IP information using WHOIS.
- Automatically identify and block suspicious IP addresses.
- Maintain a backup of the IP-blocking configuration.
- Verify the effectiveness of the implemented security controls.

---

## Lab Environment

| Component          | Details             |
| ------------------ | ------------------- |
| Attacker           | Kali Linux          |
| Security Target    | CentOS Stream 9     |
| Virtualization     | Oracle VirtualBox   |
| SSH Service        | OpenSSH             |
| Web Server         | Apache HTTP Server  |
| FTP Service        | VSFTP               |
| Security Framework | SELinux             |
| Scripting          | Bash                |
| Password Wordlist  | `rockyou.txt`     |
| Log Source         | `/var/log/secure` |
| IP Blocking        | `/etc/hosts.deny` |

> The project was performed in a virtualized lab environment for educational security testing.

---

## Tools Used

- **Kali Linux** – attack simulation and security testing
- **CentOS Stream 9** – monitored Linux server
- **Oracle VirtualBox** – virtualized lab environment
- **OpenSSH** – SSH service used for authentication testing
- **Bash** – automation and log-processing scripts
- **Hydra** – SSH authentication testing in the authorized lab
- **WHOIS** – attacker IP and country information lookup
- **SELinux** – security policy enforcement and custom SSH-port configuration
- **grep** – filtering authentication and audit logs
- **awk** – log parsing and data extraction
- **sort** – organizing extracted attack data
- **rockyou.txt** – password wordlist used during the lab

---

## Methodology

The project followed this defensive security workflow:

```text
Lab Setup
   ↓
Service Deployment
   ↓
SSH Attack Simulation
   ↓
Authentication Log Monitoring
   ↓
Attack Data Extraction
   ↓
Daily / User-wise Reporting
   ↓
SSH Hardening
   ↓
SELinux Configuration
   ↓
Automated IP Identification
   ↓
IP Blocking
   ↓
Verification
```

### 1. Lab Setup & Service Deployment

* [ ] The CentOS Stream 9 virtual machine was imported into Oracle VirtualBox and configured with network connectivity.

The lab environment was prepared with the services required for the security exercise.

***System Preparation***

The CentOS system was updated and OpenSSH was installed:

```bash
yum update
yum install openssh-server
```

Additional services used during the lab were installed:

```bash
yum install vsftpd -y
yum install httpd
```

A reports directory was also created:

```bash
mkdir /reports
```

The project submission additionally configured an Apache virtual host and created the required report location under `/reports`.

This provided the basic Linux server environment required for the subsequent monitoring and security-control activities.

---

### 2. SSH Attack Simulation & Authentication Monitoring

Kali Linux was used to simulate failed SSH authentication attempts against the CentOS server.

The `rockyou.txt` wordlist was used during the lab as part of password testing.

**Authentication Monitoring**

The CentOS security log was monitored for failed SSH authentication events using:

```bash
watch 'tail /var/log/secure | grep FAILED'
```

Failed login attempts were then generated from Kali Linux using SSH connections with incorrect credentials.

Example lab commands documented in the project:

```bash
ssh -p 22 militry@10.0.2.15
```

and:

```bash
ssh -p 22 kali@10.0.2.15
```

The CentOS server recorded the failed authentication events in its security log.

**Security Observation**
The exercise demonstrated how repeated failed SSH authentication attempts can be detected through Linux authentication logs and used as the basis for further analysis and defensive response.

---

### 3. Automated SSH Attack Tracking

The project implemented Bash-based scripts to process SSH authentication logs and generate attack information.

**Daily SSH Attack Tracking**
The `b_track_ssh_daily` script was created to process failed SSH authentication activity and generate daily attack information.

The script was made executable and executed with:

```bash
chmod +x /root/b_track_ssh_daily
```

```bash
/root/b_track_ssh_daily
```

The script processes SSH authentication records, extracts attacker IP addresses, performs country lookups, and generates a report based on the observed failed login activity.

### 4. User-wise SSH Attack Analysis

A second script, `b_track_ssh_userwise`, was implemented to analyze failed SSH login activity associated with users.
The script was created using:

```bash
vi /root/b_track_ssh_userwise
```

It was then made executable:

```bash
chmod +x /root/b_track_ssh_userwise
```

and executed with:

```bash
/root/b_track_ssh_userwise
```

The resulting output provided attack information extracted from the SSH security logs, including observed failed authentication activity.

---

### 5. SSH Hardening

The SSH server configuration was reviewed and modified as part of the hardening process.

The SSH daemon configuration file was edited using:

```bash
vi /etc/ssh/sshd_config
```

The project changed the default SSH port:

```
Port 22
```

to:

```
Port 2222
```

Changing the listening port was part of the documented SSH hardening exercise.
Changing the SSH port can reduce exposure to automated scanning of the default port, but it should not be treated as a replacement for strong authentication and other SSH security controls.

---

### 6. SELinux Configuration for Custom SSH Port

Because SELinux was enabled in the CentOS environment, the custom SSH port required SELinux configuration.

Existing SSH port mappings were checked with:

```bash
semanage port -l | grep ssh
```

Port `2222` was then associated with the SSH SELinux type:

```bash
semanage port -a -t ssh_port_t -p tcp 2222
```

The SSH service was restarted:

```bash
systemctl restart sshd
```

The service status was then verified:

```bash
systemctl status sshd
```

The project documentation shows the SSH daemon running successfully after the configuration change.

---

### 7. Attack Data Analysis & WHOIS Enrichment

The project also analyzed attacker IP information and enriched the extracted data using WHOIS.

The WHOIS package was installed with:

```bash
yum install whois
```

The generated attack information was processed to identify the originating IP addresses and associated country information.

The scripts used command-line utilities such as:

```
grep
awk
sort
whois
```

This demonstrated how raw authentication logs can be transformed into more useful security reports for investigation and analysis.

---

### 8. Automated IP Blocking

The project implemented a Bash script named:

```
protect_ssh
```

The script was designed to identify IP addresses associated with failed SSH authentication activity and add them to the TCP wrapper deny configuration.

The script was created using:

```bash
vi /root/protect_ssh
```

and made executable:

```bash
chmod +x /root/protect_ssh
```

The required deny-list files were created:

```bash
touch /etc/hosts.deny
```

and a backup file was also created:

```bash
touch /etc/hosts.deny.bak
```

The protection script was then executed:

```bash
/root/protect_ssh
```

Finally, the resulting deny-list entries were inspected with:

```bash
tail /etc/hosts.deny
```

## Defensive Workflow

```
Failed SSH Attempts
        ↓
/var/log/secure
        ↓
Attack IP Extraction
        ↓
protect_ssh
        ↓
/etc/hosts.deny
        ↓
Suspicious IP Blocked
```

---

## Findings Summary

| # | Finding / Observation                        | Security Relevance                                           | Defensive Control                   |
| - | -------------------------------------------- | ------------------------------------------------------------ | ----------------------------------- |
| 1 | Repeated failed SSH authentication attempts  | Indicates potential brute-force activity                     | Log monitoring and attack tracking  |
| 2 | Attacker IP addresses visible in SSH logs    | Enables investigation and attribution                        | IP extraction and WHOIS analysis    |
| 3 | SSH exposed on the default port              | Common target for automated scanning                         | Custom SSH port configuration       |
| 4 | SELinux required configuration for port 2222 | Security policy can prevent service operation if not updated | `semanage` SSH port configuration |
| 5 | Repeated suspicious IP activity              | Can contribute to continued authentication attacks           | Automated IP blocking               |
| 6 | Raw logs difficult to analyze manually       | Slows investigation and reporting                            | Bash automation and log parsing     |

---

## Key Lessons Learned

- Linux authentication logs provide valuable evidence for detecting SSH attacks.
- Repeated failed authentication attempts can be programmatically extracted and analyzed.
- Bash scripting can automate repetitive security monitoring and reporting tasks.
- SSH hardening should include configuration controls beyond simply changing the listening port.
- SELinux policies must be considered when services are moved to non-default ports.
- Attacker IP information can be enriched with external registration data such as WHOIS.
- Automated blocking can reduce repeated access attempts from identified suspicious IP addresses.
- Security controls should always be verified after implementation.

---

## Project Outcome

The project demonstrated a complete defensive workflow for monitoring and responding to repeated SSH authentication attacks in a controlled Linux environment.

The lab successfully covered:

- Linux server and service setup
- SSH attack simulation
- Authentication-log monitoring
- Automated SSH attack reporting
- User-wise attack analysis
- SSH hardening
- Custom SSH port configuration
- SELinux port configuration
- WHOIS-based IP analysis
- Automated IP blocking
- `/etc/hosts.deny` verification

The final workflow connected attack detection, log analysis, security hardening, automation, and defensive response into a single Linux security lab.

---

## Project Report

The complete step-by-step project report, including screenshots and execution evidence, is available here:

[View the complete project report (PDF)](<./project-report/Securing%20Linux%20Servers%20Using%20Honeypots%20and%20IP%20Blocking.pdf>)
