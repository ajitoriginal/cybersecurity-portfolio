# Hosting a Web Application on XAMPP

A hands-on lab completed as part of the **Application and Web Application Security** course in the Simplilearn Cyber Security program.
The lab demonstrates how to deploy and host a PHP/MySQL-based web application in a local XAMPP environment using Apache, MySQL, and phpMyAdmin.

---

## 📌 Overview

In this lab, an **e-Diary Management System (e-DMS)** web application was downloaded from GitHub and configured to run locally using the XAMPP stack.
The application was successfully hosted on:

```text
http://localhost/edms
```
The lab involved configuring the application files, preparing the MySQL database, importing the provided SQL database schema/data, and verifying successful application access through the browser.

---

## 🎯 Objectives

* Set up a local web application hosting environment using XAMPP.
* Configure Apache as the local web server.
* Deploy a PHP-based web application under the XAMPP htdocs directory.
* Configure MySQL for the application.
* Create and initialize the application database using phpMyAdmin.
* Import the provided SQL database.
* Access and verify the deployed web application through localhost.
* Understand the basic components involved in hosting a PHP/MySQL web application.

---

## 🛠️ Technologies & Tools

| Technology / Tool | Purpose                                       |
| ----------------- | --------------------------------------------- |
| XAMPP             | Local development and web hosting environment |
| Apache            | Web server                                    |
| PHP               | Server-side application runtime               |
| MySQL             | Database server                               |
| phpMyAdmin        | Database management                           |
| Microsoft Edge    | Web application access                        |
| GitHub            | Source repository for the demo application    |
| Windows           | Lab operating system                          |

## 🏗️ Application Architecture

The lab uses a traditional PHP/MySQL web application architecture:

```
                Browser
                   │
                   ▼
          ┌─────────────────┐
          │     Apache      │
          │   Web Server    │
          └────────┬────────┘
                   │
                   ▼
          ┌─────────────────┐
          │  e-Diary Web    │
          │   Application   │
          │      (PHP)      │
          └────────┬────────┘
                   │
                   ▼
          ┌─────────────────┐
          │     MySQL       │
          │    Database     │
          │     edmsdb      │
          └─────────────────┘
```
phpMyAdmin was used as the database administration interface.

---

## 🔬 Lab Implementation

### 1. Download the Web Application

The e-Diary Management System project was obtained from the following GitHub repository:

```
https://github.com/digitalassetmanagement/WAP_Lesson_01_Demo01.git
```

The project was downloaded as a ZIP archive and extracted locally.

---

### 2. Start Apache Using XAMPP

The XAMPP Control Panel was opened and the Apache service was started.
Apache provides the local web server required to serve the PHP application.
The XAMPP dashboard was verified through:

```
http://localhost/dashboard/
```

---

### 3. Prepare the Application Files

The downloaded project was extracted and the e-DMS application files were located.

The application files were copied into the XAMPP web root:

```
C:\xampp\htdocs\edms
```

This makes the application accessible through the local Apache server.

---

### 4. Prepare the MySQL Database

The project contained an SQL database file:

```
edmsdb.sql
```

The SQL file was located within the project and prepared for database initialization.

MySQL was then started from the XAMPP Control Panel.

---

### 5. Open phpMyAdmin

The following URL was opened:

```
http://localhost/phpmyadmin/
```

A new database was created with the name:

```
edmsdb
```

---

### 6. Import the Database

Inside phpMyAdmin, the Import functionality was used to import:

```
edmsdb.sql
```

The SQL import completed successfully, initializing the database required by the e-Diary Management System.

---

### 7. Access the Web Application

After configuring Apache and MySQL, the application was accessed through:

```
http://localhost/edms
```

The e-Diary Management System login page was displayed successfully.

The lab-provided test credentials were used to authenticate into the application.

---

### 8. Verify Successful Deployment

After authentication, the e-Diary Management System dashboard was successfully displayed.

- This confirmed that:
- Apache was serving the application.
- PHP was processing the application.
- MySQL was available to the application.
- The `edmsdb` database had been initialized successfully.
- The web application was accessible through the local environment.

---

## 🔐 Security Relevance

Although this lab primarily focuses on local web application deployment, it provides an important foundation for application and web application security testing.

- Understanding how a web application is deployed helps security professionals understand:
- Web server configuration
- Application server behavior
- PHP-based applications
- Database connectivity
- Database initialization
- Local web application architecture
- `localhost` environments
- Web application attack surfaces
- Separation between application and database layers
  A correctly configured local environment can also be used as a controlled environment for subsequent security testing and vulnerability assessment.

---

## 🧪 Key Learning Outcomes

Through this lab, I gained practical experience with:

- XAMPP configuration
- Apache web server setup
- PHP application deployment
- MySQL database setup
- phpMyAdmin
- SQL database import
- Local web application hosting
- Basic web application architecture
- Application-to-database connectivity
- Local application verification

---

## ⚠️ Security Notes

- This lab was performed in a controlled/local environment.
- The application was hosted using localhost.
- The credentials shown in the course material are lab/demo credentials and should not be reused in production.
- Production deployments should use secure authentication, strong credentials, appropriate server hardening, secure database configuration, HTTPS, and proper access controls.
- XAMPP is primarily intended for development/testing and should not be treated as a hardened production hosting environment.

---

## 📚 Lab Source

**Course**: Application and Web Application Security
**Platform**: Simplilearn
**Lab**: Hosting a Webapp on XAMPP
**Application**: e-Diary Management System

---

## Course: Application and Web Application Security
Platform: Simplilearn
Lab: Hosting a Webapp on XAMPP
Application: e-Diary Management System

---

## ✅ Result
**Lab Status: Completed Successfully**
The e-Diary Management System was successfully deployed and hosted locally using:
```
Apache + PHP + MySQL + XAMPP
```
The application was successfully accessed through:
```
http://localhost/edms
```
and the application dashboard was successfully loaded.

---

[View the complete lab report (PDF)](./lab-report/Lab_Hosting_a_Webapp_on_XAMPP.pdf)

