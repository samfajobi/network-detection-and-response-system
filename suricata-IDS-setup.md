# 🛡️ Suricata Intrusion Detection System (IDS) Setup & Configuration

## 📌 Project Overview

This document provides a step-by-step guide for installing and configuring **Suricata in Intrusion Detection System (IDS) mode** on a Linux system.

The objective is to deploy Suricata for **passive network traffic monitoring**, alert generation, and security investigation without blocking traffic.
This setup reflects **real-world SOC deployments** commonly used in enterprise environments.

---

## 🖥️ Lab Environment

| Component         | Details             |
| ----------------- | ------------------- |
| Operating System  | Ubuntu `24.0`      |
| Suricata Version  | `8.0.2`             |
| Deployment Mode   | IDS                 |
| Network Interface | `...`              |
| Traffic Source    | Live traffic / PCAP |

---

## 📦 Installation

### Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### Install Suricata

```bash
sudo apt install suricata -y
```

### Verify Installation

```bash
suricata --build-info
```

> ✅ Confirm that Suricata is compiled with **AF_PACKET** support.

---

## ⚙️ Suricata Configuration

### 📄 Configuration File Location

```text
/etc/suricata/suricata.yaml
```

---

## 🔌 Network Interface Setup

### Identify Active Network Interface

```bash
ip a
```

**Example Output:**

```text
eth0: inet 192.168.1.10/24
```

**Selected Interface:**

```text
Interface: eth0
IP Address: 192.168.1.10
```

---

## 🧠 IDS Mode Configuration (AF_PACKET)

Edit the Suricata configuration file:

```bash
sudo nano /etc/suricata/suricata.yaml
```

Configure `af-packet`:

```yaml
af-packet:
  - interface: eth0
    cluster-id: 99
    cluster-type: cluster_flow
```

### Explanation

* `interface` → Network interface to monitor
* `cluster-id` → Enables load balancing
* `cluster_flow` → Ensures traffic flows stay together
* IDS mode → **Passive detection only**

---

## 📂 Logging Configuration

### Enable JSON Logging (eve.json)

Ensure the following is enabled:

```yaml
outputs:
  - eve-log:
      enabled: yes
      filetype: regular
      filename: eve.json
```

### Log Directory

```text
/var/log/suricata/
```

Key log files:

* `eve.json` → Alerts & events
* `fast.log` → Quick alerts
* `stats.log` → Performance stats

---






