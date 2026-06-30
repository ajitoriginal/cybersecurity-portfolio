# Securing Web Applications with HTTPS and Data & Configuration Archiving

## 📌 Overview

This lab demonstrates two important application security and operational security practices:

1. Securing a web application using **HTTPS**
2. Archiving application data and configuration files using **7-Zip with password protection**

The lab was performed on a **Windows Server 2022 virtual machine** using **XAMPP**, with an e-Diary Management System (EDMS) web application hosted locally.

---

## 🎯 Objectives

- Configure Apache to support HTTPS.
- Verify that the application is accessible over HTTPS.
- Configure SSL-related Apache settings.
- Archive the web application's files.
- Archive the application's database data.
- Protect backup archives using password-based encryption.
- Store application and database backups in a dedicated backup directory.

---

## 🛠️ Tools & Technologies

- Windows Server 2022
- XAMPP
- Apache
- MySQL
- Microsoft Edge
- 7-Zip
- HTTPS / SSL/TLS
- e-Diary Management System (EDMS) (A Sample Web Application)

---

## 🔐 Part 1: Securing the Web Application with HTTPS

### Step 1: Configure Apache SSL

The Windows Server 2022 VM was launched and XAMPP was started.

Apache's SSL configuration file was opened through:

```text
XAMPP Control Panel → Apache → Config → httpd-ssl.conf
```

### Step 2: Verify HTTPS Port

Apache was configured to listen on:

```
Port 443
```

Port 443 is used for HTTPS communication.

---

### Step 3: Configure SSL Session Cache Timeout

The following Apache configuration was modified:

```apache
SSLSessionCacheTimeout 300
```

to:

```apache
SSLSessionCacheTimeout 100
```

---

### Step 4: Update Server Administrator Email

The Apache SSL configuration was updated by changing:

```
admin@example.com
```

to:

```
webmaster@example.com
```

---

### Step 5: Save the Configuration

The updated `httpd-ssl.conf` configuration was saved.

---

### Step 6: Start Apache and MySQL

Apache and MySQL services were started from the XAMPP Control Panel.

---

### Step 7: Verify the Web Application over HTTPS

The EDMS application was accessed through Microsoft Edge using:

```
https://localhost/edms
```

The application successfully loaded through the HTTPS endpoint.

---

## 📦 Part 2: Archiving Application Data and Configuration

### Step 1: Install 7-Zip

7-Zip was downloaded and installed on the Windows Server 2022 VM.

---

### Step 2: Archive the Web Application

The EDMS application directory was located at:

```
C:\xampp\htdocs\edms
```

The directory was right-clicked and archived using:

```
7-Zip → Add to archive...
```

---

### Step 3: Configure the Archive

The 7-Zip archive settings were configured and a password was applied to protect the archive.

---

### Step 4: Create the Backup Directory

A dedicated backup directory was created:

```
C:\Backup
```

The archived EDMS application was saved inside this directory with password protection.

---

### Step 5: Archive the Database

The database-related file was located at:

```
C:\xampp\mysql\data\edmsdb.sql
```

The `edmsdb.sql` file was selected and archived using:

```
7-Zip → Add to archive...
```

---

### Step 6: Password-Protect the Database Archive

A password was configured for the database archive before saving it.
The resulting archive was stored in:

```
C:\Backup
```

---

## 🔄 Lab Workflow
```
Windows Server 2022
        │
        ▼
      XAMPP
        │
        ├── Apache
        │     │
        │     ├── httpd-ssl.conf
        │     ├── HTTPS Port 443
        │     └── SSL Configuration
        │
        └── MySQL
              │
              └── EDMS Database
                    │
                    ▼
              edmsdb.sql

        ▼
   EDMS Web Application
        │
        ▼
https://localhost/edms

        │
        ▼
     7-Zip
        │
        ├── EDMS Application Archive
        │
        └── Database Archive
                │
                ▼
           C:\Backup
                │
                ▼
        Password Protected Archives
```

---

## 🔎 Security Concepts Demonstrated
### HTTPS
HTTPS provides encrypted communication between the client and web server, helping protect sensitive information from interception and tampering.
### SSL/TLS Configuration
Apache's SSL configuration was modified to control HTTPS-related server behavior.
### Secure Backup
Application and database files were archived to preserve important information for future recovery.
### Password-Protected Archives
The backup archives were protected with passwords to add an additional layer of protection to stored application and database data.
### Disaster Recovery
Maintaining application and database backups helps preserve critical information for future restoration and recovery scenarios.

---

## 🧪 Environment
| Component | Configuration |
|---|---|
| Operating System | Windows Server 2022 |
| Web Server | Apache |
| Database | MySQL |
| Application Server | XAMPP |
| Web Application | e-Diary Management System (EDMS) |
| HTTPS Port | 443 |
| Archive Tool | 7-Zip |
| Backup Location | `C:\Backup` |

---

## 📚 Key Learnings
- Configured Apache for HTTPS communication.
- Worked with Apache's httpd-ssl.conf configuration.
- Verified HTTPS communication on port 443.
- Modified SSL session cache configuration.
- Updated Apache server administrator information.
- Verified a locally hosted web application through HTTPS.
- Created application backups using 7-Zip.
- Archived database information separately.
- Applied password protection to backup archives.
- Understood the importance of backups for disaster recovery and application security.

---

## 🛡️ Security Relevance
This lab demonstrates practical concepts relevant to:
- Web Application Security
- Secure Configuration
- HTTPS / SSL/TLS
- Data Protection
- Backup Security
- Disaster Recovery
- Security Engineering
- Secure System Administration
These practices contribute to protecting web applications, securing data in transit, and preserving critical application information for recovery.

---

## ✅ Conclusion
This lab demonstrated how to secure a locally hosted web application using HTTPS and how to protect application and database information through password-protected archiving.
The HTTPS configuration helps protect communication between the client and server, while secure archiving helps preserve application data and configuration for backup and recovery purposes.
Together, these practices provide a practical foundation for **secure web application deployment, data protection, and operational security**.

[View the complete lab report (PDF)](./lab-report/Lab_Securing_Web_Applications_with_HTTPS_and_Data_&_Configuration_Archiving.pdf)
