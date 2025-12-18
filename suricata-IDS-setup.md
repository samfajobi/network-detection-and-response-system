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







