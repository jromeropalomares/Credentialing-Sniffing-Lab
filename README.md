# Credentialing-Sniffing-Lab
Wireshark-based network traffic analysis identifying plaintext credential exposure in Telnet PCAP
# Credential Sniffing Lab – Telnet Traffic Analysis

**Author: Julissa Romero-Palomares**

---

## Overview

In this lab, I analyzed a packet capture (PCAP) file using Wireshark to investigate network traffic and identify potential security vulnerabilities. The primary objective was to reconstruct a Telnet session and demonstrate how unencrypted protocols expose sensitive information.

---

## Tools Used

* Wireshark

---

## File Analyzed

* telnet-cooked.pcap

---

## Key Findings

### 1. TCP Connection Establishment

* Observed a standard TCP 3-way handshake (SYN, SYN-ACK, ACK)
* Identified communication between:

  * **192.168.0.2 (client)**
  * **192.168.0.1 (server)**

---

### 2. Telnet Protocol Detection

* Detected Telnet traffic over **port 23**
* Observed Telnet negotiation messages (authentication options, terminal settings)
* Confirmed that communication was occurring over an unencrypted protocol

---

### 3. Credential Exposure (Critical Finding)

Using Wireshark’s **“Follow TCP Stream”** feature, I reconstructed the Telnet session and identified plaintext credentials:

* **Username:** fake
* **Password:** user

**Impact:**
Because Telnet does not use encryption, credentials are transmitted in plaintext. An attacker monitoring network traffic could intercept this data and gain unauthorized access to the system.

---

### 4. Packet & Traffic Analysis

* Analyzed packet details including:

  * Source and destination IP addresses
  * Port numbers
  * Sequence and acknowledgment numbers
* Observed **PSH, ACK flags**, indicating active data transmission

---

### 5. Network Behavior Observations

* Detected **TCP retransmissions**, suggesting possible packet loss or network delay
* Observed **malformed packet indicators**, likely due to transmission or parsing anomalies
* Identified proper session termination using **FIN/ACK flags**

---

## Evidence Files

* `telnet-cooked.pcap` – original packet capture file used for analysis
* `TCP_stream_content.txt` – reconstructed Telnet session showing plaintext credentials
* `TCP_stream_graph.pdf` – visualization of TCP data flow over time

---

## Reproducibility

To reproduce this analysis:

1. Open the `.pcap` file in Wireshark
2. Apply the following display filter:

   ```
   telnet
   ```
3. Right-click any Telnet packet
4. Select:

   ```
   Follow → TCP Stream
   ```
5. View reconstructed session data in ASCII format

---

## What I Learned

* How to analyze PCAP files using Wireshark
* How TCP connections are established and terminated
* How to reconstruct network sessions from packet data
* How insecure protocols like Telnet expose sensitive information
* The importance of encryption in secure communications

---

## Skills Demonstrated

* Network traffic analysis
* Packet inspection
* Protocol analysis (TCP/IP, Telnet)
* Security vulnerability identification
* Digital forensics fundamentals

---
