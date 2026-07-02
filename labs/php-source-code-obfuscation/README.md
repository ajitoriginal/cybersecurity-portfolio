
# PHP Source Code Obfuscation

## Objective

The objective of this lab is to understand and implement **PHP source code obfuscation** to make application source code more difficult to read, understand, and reverse engineer.

The lab demonstrates how a PHP web application's source code can be obfuscated while maintaining the application's functionality and verifying that the affected page continues to work correctly.

---

## Environment

| Component            | Details                          |
| -------------------- | -------------------------------- |
| Operating System     | Windows Server 2022              |
| Web Server           | Apache                           |
| Database             | MySQL                            |
| Web Stack            | XAMPP                            |
| Application          | e-Diary Management System (EDMS) |
| Programming Language | PHP                              |
| Browser              | Microsoft Edge                   |
| Target File          | `my-profile.php`               |

---

## Tools Used

- XAMPP
- Apache
- MySQL
- Microsoft Edge
- PHP Obfuscator
- Windows Server 2022
- e-Diary Management System (EDMS)

---

## Methodology

The lab followed the following workflow:

```text
PHP Source Code
       │
       ▼
Open my-profile.php
       │
       ▼
Copy Original Source Code
       │
       ▼
PHP Obfuscator
       │
       ▼
Generate Obfuscated Code
       │
       ▼
Replace Original Source Code
       │
       ▼
Save my-profile.php
       │
       ▼
Start Apache & MySQL
       │
       ▼
Access EDMS Application
       │
       ▼
Login & Open My Profile
       │
       ▼
Verify Application Functionality
```

---

## Implementation
### 1. Access the EDMS Application Directory
The Windows Server 2022 virtual machine was launched and the EDMS application directory was accessed:
```
C:\xampp\htdocs\edms
```
The directory contains the PHP source files used by the e-Diary Management System.

---

### 2. Open the PHP Source File
The following PHP file was selected:
```
my-profile.php
```
The file was opened using Notepad to inspect the existing source code.

---

### 3. Copy the Original Source Code
All existing source code from `my-profile.php` was selected and copied.
The original source code was preserved temporarily so that it could be passed to the PHP obfuscation tool.

---

### 4. Obfuscate the PHP Source Code
A PHP obfuscation tool was opened in Microsoft Edge.
The copied PHP source code was pasted into the obfuscator and the Obfuscate operation was executed.
The resulting code was significantly harder to read and understand compared with the original source code.

---

### 5. Replace the Original Source Code
The generated obfuscated PHP code was copied from the obfuscator.
The original contents of:
```
my-profile.php
```
were replaced with the generated obfuscated code.
The modified file was then saved.

---

### 6. Start XAMPP Services
XAMPP Control Panel was opened and the required services were started:
```
Apache
MySQL
```
These services were required to host and run the EDMS web application locally.

---

### 7. Access the Web Application
The EDMS application was accessed through Microsoft Edge using:
```
http://localhost/edms
```
The login page was opened successfully.

---

### 8. Login to the Application
The lab provided the following dummy credentials:
```
Email: johndoe@gmail.com
Password: Test@123
```
These credentials were used only for the local lab environment.

---

### 9. Open the My Profile Page
After successful authentication, the My Profile page was opened.
This page is linked to:
```
my-profile.php
```
The page loaded successfully after the source code had been obfuscated.

---

## Findings
### Finding 1 — Source Code Obfuscation
The PHP source code was successfully transformed into an obfuscated format.
The resulting code was considerably less readable and more difficult to understand than the original source.
### Finding 2 — Application Functionality Preserved
After replacing the original source code with the obfuscated version, the EDMS application continued to function correctly.
The **My Profile / Update Profile** page loaded successfully.
### Finding 3 — Obfuscation Increases Reverse-Engineering Difficulty
Obfuscation adds complexity to the source code and can make casual inspection and reverse engineering more difficult.
However, obfuscation does not make the source code completely inaccessible to a determined attacker.

---

## Security Impact
Source code obfuscation can provide an additional layer of protection by making application logic more difficult to understand.
Potential benefits include:
- Makes source code harder to read.
- Increases the effort required for reverse engineering.
- Helps protect intellectual property.
- Can make casual code analysis more difficult.
- Adds complexity for attackers attempting to understand application logic.
However, obfuscation should not be considered a replacement for fundamental security controls.
It does not provide complete protection against determined attackers.

---

## Limitations
Source code obfuscation has several limitations:
- Obfuscation does not encrypt the application itself.
- Determined attackers may still reverse engineer or analyze the application.
- Poorly implemented obfuscation can affect maintainability.
- Excessive obfuscation can make debugging more difficult.
- Obfuscation may introduce performance or compatibility considerations.
- Sensitive information such as passwords, API keys, and secrets should never rely on obfuscation for protection.
For stronger security, obfuscation should be combined with secure coding practices and appropriate security controls.

---

## Remediation / Security Recommendations
For production applications:
1. Use obfuscation only as an additional security layer.
2. Never hard-code passwords, API keys, or other secrets in source code.
3. Store sensitive configuration securely.
4. Follow secure coding practices.
5. Apply proper authentication and authorization controls.
6. Use encryption where confidentiality is required.
7. Perform regular vulnerability assessments.
8. Keep dependencies and server software updated.
9. Minimize unnecessary exposure of application source code.
10. Validate that obfuscation does not negatively affect application functionality or maintainability.

---

## Result
The PHP source code of my-profile.php was successfully obfuscated.
The modified application was then tested through the locally hosted EDMS application.
| Test | Result |
|------|--------|
| PHP source code accessed | ✅ Successful |
| Original source code copied | ✅ Successful |
| Source code obfuscated | ✅ Successful |
| Obfuscated code inserted into `my-profile.php` | ✅ Successful |
| Apache started | ✅ Successful |
| MySQL started | ✅ Successful |
| EDMS application accessed | ✅ Successful |
| User login | ✅ Successful |
| My Profile page loaded | ✅ Successful |

---

## Key Learnings
- Understood the concept of PHP source code obfuscation.
- Learned how obfuscation changes the readability of source code.
- Practiced applying obfuscation to an existing PHP application.
- Verified that application functionality can remain intact after obfuscation.
- Understood the difference between obfuscation and actual security controls.
- Learned that obfuscation should be combined with encryption and secure coding practices.
- Understood that obfuscation is primarily a defense-in-depth technique rather than a complete security mechanism.

---

## Security Concepts Covered
- Source Code Obfuscation
- Reverse Engineering Protection
- Application Security
- Secure Coding
- Defense in Depth
- Source Code Protection
- Web Application Security
- PHP Application Security

---

## Ethical Use
This lab was performed in a controlled local virtual machine environment using a deliberately provided web application.
Source code obfuscation and application security techniques should only be applied to systems and applications for which you have explicit authorization.

---

## Conclusion
PHP source code obfuscation was successfully implemented on the EDMS application's my-profile.php file.
The original source code was transformed into an obfuscated form, replaced in the application, and tested through the locally hosted web application. The My Profile page continued to function correctly after the modification.
Obfuscation can make source code more difficult to understand and can increase the effort required for reverse engineering. However, it does not provide complete protection against determined attackers.
Therefore, source code obfuscation should be treated as an additional defense-in-depth measure and used together with encryption, secure coding practices, authentication, authorization, and other application security controls.

---

[View the complete lab report (PDF)](./lab-report/php-source-code-obfuscation.pdf)
