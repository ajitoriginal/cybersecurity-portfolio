
# File Hash Integrity Verification

## Overview

This lab demonstrates how cryptographic file hashes can be used to verify file integrity across different operating systems.

The exercise uses a **Windows Server 2022** virtual machine and a **Kali Linux** virtual machine to:

- Create a text file and calculate its SHA-256 hash.
- Transfer the file securely from Windows Server to Kali Linux using SCP over SSH.
- Calculate the hash again on Kali Linux to verify file integrity.
- Rename the file and confirm that renaming does not change its hash.
- Modify the file contents and calculate the hash again to demonstrate that the hash changes when the file is altered.

---

## Objectives

- Understand the purpose of cryptographic file hashing.
- Calculate SHA-256 hashes on Windows and Linux.
- Transfer files securely between virtual machines using SCP.
- Verify file integrity using matching hash values.
- Understand the effect of file renaming and content modification on hashes.

---

## Lab Environment

| Component           | Details             |
| ------------------- | ------------------- |
| Windows Environment | Windows Server 2022 |
| Linux Environment   | Kali Linux          |
| Virtualization      | VMware              |
| Hash Algorithm      | SHA-256             |
| File                | `101.txt`         |
| Transfer Protocol   | SCP over SSH        |

---

## Tools & Commands Used

### Windows Server / PowerShell

```powershell
ls
```
Lists files in the current directory.
```powershell
Get-FileHash 101.txt -Algorithm SHA256
```
Calculates the SHA-256 hash of 101.txt.
### Kali Linux
```bash
systemctl start ssh
```
Starts the SSH service.
```bash
ip a
```
Displays network interface and IP address information.
```bash
sha256sum 101.txt
```
Calculates the SHA-256 hash of the file.
```bash
mv 101.txt 102.txt
```
Renames the file.
```bash
sha256sum 102.txt
```
Calculates the SHA-256 hash after renaming.
```bash
nano 102.txt
```
Opens the file for editing.
### Secure File Transfer
```bash
scp 101.txt labuser@<KALI-IP>:/home/kali/Documents
```
Transfers the file from Windows Server to the Kali Linux machine using SCP over SSH.
- Replace `<KALI-IP>` with the IP address assigned to the Kali Linux virtual machine.

---

## Lab Procedure
### 1. Create the File on Windows Server
A text file named `101.txt` was created on the Windows Server 2022 virtual machine containing:
```
abcde
```
The file was then located using PowerShell.
### 2. Calculate the Initial SHA-256 Hash
The following PowerShell command was used:
```powershell
Get-FileHash 101.txt -Algorithm SHA256
```
This generated the SHA-256 hash of the original file.
The hash value was recorded as the baseline for later integrity verification.

---

### 3. Prepare Kali Linux for File Transfer
The Kali Linux virtual machine was started and the SSH service was enabled:
```bash
systemctl start ssh
```
The Kali Linux IP address was then identified using:
```bash
ip a
```

---

### 4. Transfer the File Using SCP
From Windows Server, the file was transferred to Kali Linux using:
```bash
scp 101.txt labuser@<KALI-IP>:/home/kali/Documents
```
SCP uses SSH to provide secure file transfer between systems.

---

### 5. Verify the Transferred File
On Kali Linux, the transferred file was located using:
```bash
ls
```
The SHA-256 hash was then calculated:
```bash
sha256sum 101.txt
```
The resulting hash was compared with the original SHA-256 hash generated on Windows Server.

A matching hash indicates that the file contents remained unchanged during transfer.

---

### 6. Rename the File
The transferred file was renamed:
```bash
mv 101.txt 102.txt
```
The hash was then calculated again:
```bash
sha256sum 102.txt
```
The hash remained the same because renaming the file does not modify its contents.
This demonstrates that a file hash is based on the file's data rather than its filename.

---

### 7. Modify the File Contents
The renamed file was opened using:
```bash
nano 102.txt
```
The contents of the file were modified and saved.
The SHA-256 hash was then calculated again:
```bash
sha256sum 102.txt
```
The resulting hash was different from the original hash.
This demonstrates that modifying even the contents of a file changes its cryptographic hash.

---

## Key Findings
### File Transfer
The SHA-256 hash calculated on Windows Server was used as a baseline and compared with the hash calculated after transferring the file to Kali Linux.

A matching hash confirms that the file contents were preserved during the transfer.
### File Renaming
Renaming:
```
101.txt → 102.txt
```
did not change the SHA-256 hash because the file contents remained unchanged.
### File Modification
After modifying the contents of `102.txt`, the SHA-256 hash changed.
This demonstrates the usefulness of cryptographic hashes for detecting file modifications.

---

## Security Concepts Demonstrated
- Cryptographic hashing
- SHA-256
- File integrity verification
- Data integrity
- Secure file transfer
- SSH
- SCP
- Windows PowerShell
- Linux command-line utilities
- Integrity monitoring

---

## Security Relevance
File hashing is commonly used in cybersecurity to verify the integrity of files and detect unauthorized modifications.

Hash values can be used to:

- Verify downloaded files.
- Validate files transferred between systems.
- Detect unauthorized file modifications.
- Support malware and forensic analysis.
- Verify software and security tool integrity.
- Establish known-good file baselines.

A changed hash does not by itself explain why a file changed; it indicates that the file's contents are no longer identical to the content represented by the original hash.

---

## Lab Workflow

```
Windows Server 2022
        │
        │ Create 101.txt
        ▼
Calculate SHA-256 Hash
        │
        │ SCP over SSH
        ▼
Kali Linux
        │
        ├── Verify SHA-256 Hash
        │
        ├── Rename 101.txt → 102.txt
        │
        └── Modify File Contents
                │
                ▼
        Calculate SHA-256 Again
                │
                ▼
        Hash Value Changes
```

---

## Skills Demonstrated
- HA-256 Hashing
- File Integrity Verification
- Linux Command Line
- Windows PowerShell
- SSH
- SCP
- Secure File Transfer
- Basic Cryptography
- Security Operations Fundamentals

---

## Conclusion
This lab provided practical experience with SHA-256 hashing and file integrity verification across Windows Server and Kali Linux.

The exercise demonstrated that transferring or renaming a file without changing its contents preserves the hash, while modifying the file contents produces a different hash.

These concepts form a fundamental part of cybersecurity practices involving data integrity, secure file transfer, forensic analysis, and detection of unauthorized changes.

[View the complete lab report (PDF)](./lab-report/Lab_Understanding_and_Calculating_File_Hashes_Using_Windows_Server_and_Kali_Linux.pdf)
