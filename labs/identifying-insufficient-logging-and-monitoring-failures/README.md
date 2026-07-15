
# 🧪 Identifying Insufficient Logging and Monitoring Failures

## 📌 Course Context

This lab was completed as part of the **Application and Web Application Security** learning program.

The lab demonstrates how insufficient logging can lead to monitoring failures by configuring an Apache web server without access logging, verifying the absence of logs, and then enabling proper Apache logging to observe web server connections.

---

## 🎯 Objective

**Identifying insufficient logging leading to monitoring failures**

The objective of this lab is to understand how inadequate logging affects security monitoring and incident detection, and how proper Apache logging can help maintain visibility into web server activity.

---

## 📝 Overview

Logging and monitoring are essential components of web application and server security.

In this lab, an Apache web server was configured in Kali Linux to initially operate without connection logging. A test web page was then accessed through a local domain, and the Apache `access.log` was checked to demonstrate the lack of logging.

Logging was subsequently enabled by adding the appropriate `ErrorLog` and `CustomLog` directives to the Apache virtual host configuration. After restarting and reloading Apache, the web application was accessed again and the generated connection logs were verified.

This demonstrates how insufficient logging can make it difficult to detect suspicious activity, investigate security incidents, and monitor web server behavior.

---

## 🎯 Objectives

- Understand the importance of logging and monitoring in web server security.
- Configure an Apache web server in Kali Linux.
- Demonstrate a web server configuration with insufficient logging.
- Verify the absence of Apache access logs.
- Configure Apache access and error logging.
- Generate web server activity and inspect the resulting logs.
- Understand the security impact of insufficient logging.

---

## 🖥️ Lab Environment

| Component            | Details                                           |
| -------------------- | ------------------------------------------------- |
| Operating System     | Kali Linux                                        |
| Web Server           | Apache2                                           |
| Web Browser          | Firefox                                           |
| Domain               | `mydomain.local`                                |
| Web Root             | `/var/www/html`                                 |
| Apache Configuration | `/etc/apache2/sites-available/000-default.conf` |
| Access Log           | `/var/log/apache2/access.log`                   |
| Error Log            | `/var/log/apache2/error.log`                    |

---

## 🛠️ Tools & Technologies

- Kali Linux
- Apache2
- Firefox
- Apache Virtual Host Configuration
- Linux Terminal
- Apache Access Logs
- Apache Error Logs

---

## 🔬 Methodology

### 1. Configure Kali Linux and Apache

The Kali Linux terminal was opened with elevated privileges.

```bash
sudo su
```
The package repository was updated:
```bash
apt update
```
Apache2 was then installed:
```bash
apt install apache2
```

---

### 2. Inspect Apache Site Configuration
The available Apache site configurations were checked:
```bash
ls /etc/apache2/sites-available
```
The default virtual host configuration was opened:
```bash
nano /etc/apache2/sites-available/000-default.conf
```
The existing logging configuration was removed to demonstrate the effect of insufficient logging.

---

### 3. Create the Test Web Page
A basic HTML page was created under the Apache web root:
```bash
echo "<html><body><h1>Welcome to mydomain.local</h1></body></html>" | sudo tee /var/www/html/index.html
```
The page displays:
```
Welcome to mydomain.local
```

---

### 4. Enable the Apache Site
The default Apache site configuration was enabled:
```bash
a2ensite 000-default.conf
```
Apache2 was then started:
```bash
systemctl start apache2
```

---

### 5. Configure the Local Domain
The Kali Linux IP address was identified using:
```bash
ip a
```
The lab environment used:
```
192.168.1.5
```
The local hosts file was opened:
```bash
nano /etc/hosts
```
The following entry was added:
```
192.168.1.5 mydomain.local
```

---

### 6. Access the Web Application
Firefox was opened and the following URL was accessed:
```
http://mydomain.local
```
The test web page was successfully displayed.

---

### 7. Verify Insufficient Logging
The Apache log directory was inspected:
```bash
ls /var/log/apache2
```
The Apache access log was then checked:
```bash
tail /var/log/apache2/access.log
```
At this stage, no log entries were generated.
This demonstrates the monitoring problem caused by insufficient logging: although the web server was receiving requests, the corresponding activity was not being recorded in the access log.

---

### 8. Enable Apache Logging
The Apache virtual host configuration was opened again:
```bash
nano /etc/apache2/sites-available/000-default.conf
```
The following logging directives were added before `</VirtualHost>`:
```apache
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
```
The configuration enables:
- Apache error logging through error.log
- Apache access logging through access.log
- The combined log format for recording connection information

---

### 9. Restart Apache
Apache was restarted to apply the configuration:
```bash
systemctl restart apache2
```
Apache was then reloaded:
```bash
systemctl reload apache2
```

---

### 10. Generate Web Server Activity
The test web page was accessed again:
```
http://mydomain.local
```
This generated a new HTTP request to the Apache server.

---

### 11. Verify the Generated Logs
The Apache access log was checked again:
```bash
tail /var/log/apache2/access.log
```
This time, Apache connection logs were visible.
The difference between the two configurations demonstrates the importance of enabling appropriate logging for effective monitoring.

---

## 📊 Findings Summary
| Test | Configuration | Observation | Security Impact |
|---|---|---|---|
| 1 | Logging disabled/removed | No access log entries | Web activity cannot be effectively monitored |
| 2 | Website accessed | Page loads successfully | Activity occurs without sufficient visibility |
| 3 | `ErrorLog` configured | Error logging enabled | Server errors can be investigated |
| 4 | `CustomLog` configured | Access logs generated | Web requests become observable |
| 5 | Access log inspected | Connection information visible | Improves monitoring and investigation capability |

---

## 🔐 Security Relevance
Insufficient logging can create a significant visibility gap in a web server environment.
Without adequate logs:
- Suspicious requests may go unnoticed.
- Security incidents become harder to investigate.
- Attack activity may not leave sufficient evidence.
- Administrators have reduced visibility into server activity.
- Incident response becomes more difficult.
- Monitoring systems may not have enough information to detect abnormal behavior.
Proper logging provides security teams with useful information for monitoring, investigation, troubleshooting, and incident response.

---

## 🧩 Security Concepts Demonstrated
### Insufficient Logging
A system that does not record relevant security and operational events provides limited visibility into activity occurring on the system
### Security Monitoring
Logs provide the underlying data required to monitor system and application activity.
### Incident Investigation
Access and error logs can provide useful evidence when investigating suspicious or abnormal activity.
### Apache Logging
Apache can record web requests and server errors through directives such as:
```apache
ErrorLog
CustomLog
```

---

## 📈 Observations / Results
### Before Logging Configuration
The web application was accessible, but checking:
```bash
tail /var/log/apache2/access.log
```
did not show the expected connection entries.
This demonstrated the monitoring failure caused by insufficient logging.
### After Logging Configuration
After adding:
```apache
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
```
and restarting/reloading Apache, accessing the web page generated entries in:
```
/var/log/apache2/access.log
```
The lab successfully demonstrated the difference between insufficient and properly configured logging.

---

## 🧠 Key Learnings
- Logging is an important part of effective security monitoring.
- A functional web application does not necessarily mean that sufficient monitoring is in place.
- Apache logging can be controlled through its virtual host configuration.
- CustomLog can be used to record web server access requests.
- ErrorLog records Apache server errors.
- Insufficient logging can create gaps in security visibility.
- Logs are valuable during troubleshooting, monitoring, and incident investigation.
- Security monitoring depends on having sufficient and useful event data.

---

## ⚠️ Security & Ethical Use
This lab was performed in an isolated and authorized learning environment for cybersecurity education and defensive security practice.
The techniques demonstrated here should only be applied to systems for which you have explicit authorization.

---

[View the complete lab report (PDF)](./lab-report/Lab_Identifying_Insufficient_Logging_and_Monitoring_Failures.pdf)


