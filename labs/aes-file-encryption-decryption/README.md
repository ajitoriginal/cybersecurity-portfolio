# AES File Encryption & Decryption

## Overview

This lab demonstrates the practical implementation of **AES-based file encryption and decryption** across Windows Server 2022 and Kali Linux.

The lab involved encrypting a confidential text file on Windows Server 2022 using **AES Crypt**, securely transferring the encrypted file to Kali Linux using **SCP over SSH**, and decrypting the file on Kali Linux using the **AES Crypt CLI**.

The exercise demonstrates how encryption can protect sensitive information during storage and how secure file transfer mechanisms can be used to move encrypted data between different operating systems.

---

## 🎯 Objectives

- Understand the practical use of **AES encryption** for protecting files.
- Encrypt a confidential text file using AES Crypt.
- Transfer an encrypted file securely between Windows Server and Kali Linux.
- Use **SSH/SCP** for secure file transfer.
- Decrypt the encrypted file using the AES Crypt command-line interface.
- Verify the integrity and accessibility of the decrypted file.

---

## 🖥️ Lab Environment

| Component         | Details              |
| ----------------- | -------------------- |
| Windows System    | Windows Server 2022  |
| Linux System      | Kali Linux           |
| Virtualization    | VMware Workstation   |
| Encryption Tool   | AES Crypt            |
| Secure Transfer   | SSH / SCP            |
| File              | `Confidential.txt` |
| Encryption Format | `.aes`             |

---

## 🛠️ Tools & Technologies

- **AES Crypt**
- **AES Encryption**
- **Windows Server 2022**
- **Kali Linux**
- **SSH**
- **SCP**
- **Linux Terminal**
- **PowerShell**
- **VMware Workstation**

---

## 🔐 Practical Implementation

### 1. Install AES Crypt on Windows Server

AES Crypt was downloaded and installed on the Windows Server 2022 virtual machine.

The tool provides file-level encryption using AES to protect sensitive data.

---

### 2. Create the Confidential File

A text file named:

```text
Confidential.txt
```
was created on Windows Server 2022.
The file contained:
```
password is found.
```
The file was then saved to the system.

---

### 3. Encrypt the File
The `Confidential.txt` file was encrypted using AES Crypt.
The encryption process generated:
```
Confidential.txt.aes
```
A password was provided during the encryption process to protect the file.
The original plaintext file was therefore converted into an encrypted `.aes` file.

---

### 4. Prepare Kali Linux for File Transfer
The Kali Linux virtual machine was opened and the SSH service was started:
```bash
sudo su -
ip a
```
The IP address of the Kali Linux machine was identified.

The SSH service was then started:
```bash
systemctl start ssh
```

---

### 5. Transfer the Encrypted File Using SCP
The encrypted file was transferred from Windows Server 2022 to Kali Linux using SCP:
```bash
scp Confidential.txt.aes kali@192.168.1.9:/home/kali/Desktop
```
The encrypted file was transferred to the Kali Linux Desktop directory.

The received file was verified using:
```bash
cd Desktop
ls
```
The encrypted file was successfully displayed in the directory.

---

### 6. Install AES Crypt on Kali Linux
AES Crypt was downloaded inside the Kali Linux virtual machine.

The downloaded archive was extracted using:
```bash
tar -xzf aescrypt_cli_4.7.0-Linux-x86_64.tar.gz
```
The AES Crypt CLI directory was then accessed:
```bash
cd aescrypt_cli_4.7.0-Linux-x86_64/bin
```

---

### 7. Decrypt the File
The encrypted file was decrypted using the AES Crypt command-line tool:
```bash
./aescrypt -d /home/kali/Desktop/Confidential.txt.aes
```
The encryption password was provided when prompted.

This restored the original:
```
Confidential.txt
```
file.

---

### 8. Verify the Decrypted File
The Kali Linux Desktop directory was accessed:
```bash
cd /home/kali/Desktop
```
The available files were checked:
```bash
ls
```
The contents of the decrypted file were then displayed:
```bash
cat Confidential.txt
```
The original message was successfully recovered:
```
password is found.
```

---

## 🔎 Security Concepts Demonstrated
### AES Encryption
AES provides cryptographic protection for data by converting readable plaintext into ciphertext that cannot be interpreted without the appropriate decryption key/password.
### Data Protection
Encrypting sensitive files helps protect confidential information from unauthorized access if the file is exposed or transferred through an untrusted environment.
### Secure File Transfer
SCP was used to transfer the encrypted file between Windows Server and Kali Linux through SSH.
### SSH
SSH provides a secure communication channel for remote administration and secure data transfer.
### Cross-Platform Security
The exercise demonstrated an end-to-end security workflow involving both Windows and Linux environments.

---

## 📊 Workflow
```
Windows Server 2022
        │
        ▼
Create Confidential.txt
        │
        ▼
AES Encryption
        │
        ▼
Confidential.txt.aes
        │
        │ SCP over SSH
        ▼
Kali Linux
        │
        ▼
AES Crypt CLI
        │
        ▼
Decrypt File
        │
        ▼
Confidential.txt
        │
        ▼
Verify Original Content
```
## 🧪 Observations & Results
| Activity                          | Result               |
| --------------------------------- | -------------------- |
| AES Crypt installation on Windows | Successful           |
| Confidential file creation        | Successful           |
| File encryption                   | Successful           |
| Encrypted `.aes` file creation    | Successful           |
| SSH service on Kali               | Started successfully |
| SCP file transfer                 | Successful           |
| AES Crypt CLI installation        | Successful           |
| File decryption                   | Successful           |
| Decrypted file verification       | Successful           |

The lab successfully demonstrated the complete lifecycle of protecting, transferring, and recovering a confidential file using AES encryption and secure file transfer mechanisms.

---

## 🎓 Key Learnings
- Practical understanding of AES-based file encryption.
- Understanding of plaintext, encrypted files, and decryption.
- Hands-on experience with AES Crypt.
- Practical use of SSH and SCP for secure file transfer.
- Experience transferring files between Windows Server and Kali Linux.
- Familiarity with AES Crypt CLI on Linux.
- Understanding of how encryption can protect sensitive data during storage and transfer.
- Improved practical experience working across Windows and Linux security environments.

---

## 🛡️ Security & Ethical Use
This lab was performed in an isolated virtual lab environment for educational and cybersecurity training purposes.

All encryption, file-transfer, and system-administration activities were performed on systems under authorized control.

The techniques demonstrated here should only be used on systems and data for which appropriate authorization has been obtained.

[View the complete lab report (PDF)](./lab-report/Lab_Encrypting_and_Decrypting_Message_Using_AES.pdf)
