
# HTTP Traffic Analysis Using Wireshark

## Overview

This lab demonstrates the capture and analysis of HTTP network traffic using **Wireshark** in a Kali Linux environment.

The exercise involved generating HTTP traffic, filtering captured packets, resolving the target domain to an IP address, and inspecting the communication across the **IPv4, TCP, and HTTP protocol layers**.

The lab also demonstrates the security implications of **unencrypted HTTP communication**, where network traffic can potentially be observed and analyzed in transit.

---

## Objectives

- Capture HTTP traffic using Wireshark.
- Analyze client-server communication patterns.
- Filter HTTP packets based on a target IP address.
- Perform DNS resolution using `dig`.
- Inspect IPv4 and TCP packet information.
- Analyze HTTP request and response data.
- Understand the security implications of unencrypted HTTP traffic.
- Configure Wireshark for network/IP address resolution.

---

## Environment

| Component         | Details                   |
| ----------------- | ------------------------- |
| Operating System  | Kali Linux                |
| Network Interface | `eth0`                  |
| Packet Analyzer   | Wireshark                 |
| Browser           | Firefox ESR               |
| DNS Utility       | `dig`                   |
| Protocol Analyzed | HTTP                      |
| Target Domain     | `honeypot.cloudbaba.in` |
| Resolved IP       | `203.163.247.52`        |

---

## Technologies & Tools

- **Kali Linux**
- **Wireshark**
- **Firefox ESR**
- **dig**
- **HTTP**
- **TCP/IP**

---

## Practical Implementation

### 1. Launch Kali Linux

The lab was performed inside a Kali Linux virtual machine.

After logging into the system, Wireshark was launched to begin packet capture.

---

### 2. Start Wireshark Capture

Wireshark was opened and the `eth0` network interface was selected for packet capture.

The interface was monitored while generating HTTP traffic from the browser.

---

### 3. Generate HTTP Traffic

Firefox ESR was opened and the provided lab resource was accessed:

```text
http://honeypot.cloudbaba.in/rat/
```
The njrat_2.zip resource was accessed to generate HTTP communication between the Kali Linux system and the remote server.

---

### 4. Filter HTTP Traffic
After generating the traffic, the Wireshark display filter was used to isolate HTTP packets:
```
http
```
This reduced the packet view to HTTP-related communication and made the client-server interaction easier to analyze.

---

### 5. Resolve the Target Domain
The target domain was resolved using the `dig` command:
```bash
dig honeypot.cloudbaba.in
```
The DNS response identified the server IP address used for further packet filtering.
```
203.163.247.52
```

---

### 6. Filter Traffic by Target IP
The HTTP traffic was further narrowed down using the following Wireshark display filter:
```
http && ip.addr == 203.163.247.52
```
This filter displays HTTP packets where the specified IP address is involved in the communication.

---

### 7. Analyze IPv4 Information
An HTTP packet was opened and the Internet Protocol Version 4 section was expanded.

This allowed inspection of information such as:

- Source IP address
- Destination IP address
- IP-level packet information
- Communication direction

---

### 8. Analyze TCP Information
The **Transmission Control Protocol** section was expanded to inspect the transport-layer information associated with the HTTP communication.
The analysis included TCP-related packet information such as:

- Source and destination ports
- Sequence information
- Acknowledgment information
- TCP flags
- Stream information

This demonstrates how HTTP communication is transported over TCP.

---

### 9. Analyze HTTP Packet Data
The **Hypertext Transfer Protocol** section was expanded to inspect the application-layer information contained in the packet.

The captured traffic provided visibility into HTTP communication between the client and server.

Because HTTP is unencrypted, packet captures can expose application-layer information to someone capable of monitoring the network traffic.

---

### 10. Enable Network/IP Address Resolution
Wireshark preferences were opened and the following option was enabled:
**Preferences → Name Resolution → Resolve network (IP) addresses**
This allows Wireshark to resolve IP addresses into recognizable network or host information where resolution is available.

---

## Security Concepts Demonstrated
### HTTP Traffic Inspection
Wireshark can capture and decode network packets across multiple protocol layers, allowing security analysts to investigate communication between hosts.
### DNS Resolution
The `dig` utility can be used to determine DNS information associated with a domain before investigating corresponding network traffic.
### IP-Based Traffic Filtering
Wireshark display filters can significantly reduce the amount of traffic under investigation.
Example:
```
http && ip.addr == 203.163.247.52
```
This is useful when investigating traffic associated with a particular host.
### TCP Analysis
Examining the TCP layer provides insight into how application traffic is transported between endpoints.
### Unencrypted HTTP
HTTP traffic is transmitted without encryption. Consequently, captured traffic can potentially expose HTTP requests, responses, headers, and other application-layer information.

This highlights the importance of using **HTTPS/TLS** for protecting web communications.

---

## Observations & Results
The lab successfully demonstrated the following:

- HTTP traffic was captured using Wireshark.
- HTTP packets were isolated using display filters.
- DNS information for the target domain was obtained using `dig`.
- The resolved server IP was used to narrow the packet capture.
- IPv4 and TCP protocol details were inspected.
- HTTP packet contents and communication details were analyzed.
- Wireshark network/IP address resolution was configured.
- The exercise demonstrated the visibility of information transmitted through unencrypted HTTP.

Understanding packet-level communication helps security analysts identify suspicious connections, investigate incidents, and understand how systems communicate over a network.

---

## Key Learning Outcomes
Through this lab, I gained practical experience in:

- Capturing network packets with Wireshark.
- Filtering traffic using Wireshark display filters.
- Resolving domains using `dig`.
- Investigating IPv4 and TCP communication.
- Inspecting HTTP requests and responses.
- Understanding protocol-layer relationships.
- Recognizing the security risks associated with unencrypted HTTP.
- Using packet analysis as part of a cybersecurity investigation.

---

[View the complete lab report (PDF)](./lab-report/Lab_Capturing_and_Analyzing_HTTP_Traffic_in_Wireshark.pdf)
