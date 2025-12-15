# network-detection-and-response-system
Building a Network Detection and Response System with Suricata and Zeek.


# Network Detection and Response (NDR) System using Suricata and Zeek

## 📌 Project Overview

This project focuses on building a **Network Detection and Response (NDR)** lab using **Suricata** and **Zeek**, two powerful open-source network security monitoring tools.

The goal of this project is to simulate **real-world SOC network monitoring**, where traffic is continuously inspected, suspicious activity is detected, enriched, and investigated, and actionable security insights are produced.

This lab mirrors how enterprise SOCs detect threats such as:

* Network intrusions
* Malware command-and-control (C2)
* Port scanning and reconnaissance
* Data exfiltration
* Suspicious DNS and HTTP activity

---

## 🎯 Project Objectives

* Understand how **network traffic flows** through detection engines
* Learn the **difference between signature-based and behavioral detection**
* Gain hands-on experience with **Suricata (IDS)** and **Zeek (NSM)**
* Correlate alerts with rich network metadata
* Build SOC-ready investigation and analysis skills

---

## 🏗️ Architecture Overview

```
Network Traffic (Live or PCAP)
        ↓
  Network Interface / PCAP
        ↓
 ┌──────────────────────────┐
 │        Suricata           │
 │  (Intrusion Detection)   │
 │  - Signatures            │
 │  - Alerts                │
 │  - Flow logs             │
 └─────────────┬────────────┘
               ↓
 ┌──────────────────────────┐
 │           Zeek            │
 │  (Network Security       │
 │   Monitoring)            │
 │  - conn.log              │
 │  - dns.log               │
 │  - http.log              │
 │  - ssl.log               │
 └─────────────┬────────────┘
               ↓
     SOC Analysis & Response
```

---

## 🔍 Tool Breakdown

### 🛡️ Suricata – Intrusion Detection System (IDS)

Suricata is responsible for **detecting malicious or suspicious activity** using:

* Signature-based detection (rules)
* Protocol analysis
* Threat intelligence feeds

Suricata answers the question:

> **“Is this network traffic malicious?”**

**Key Outputs:**

* Alerts (`eve.json`)
* Flow records
* DNS and HTTP events

---