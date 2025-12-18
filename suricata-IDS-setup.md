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

![Suricata-IDS-setup-1](screenshots/suricata-IDS-setup-1.png) 

---

## ⚙️ Suricata Configuration

### 📄 Configuration File Location

```text
/etc/suricata/suricata.yaml
```
![Suricata-IDS-setup-1](screenshots/suricata-IDS-setup-2.png) 

---

## 🔌 Network Interface Setup

### Identify Active Network Interface

```bash
ip a
```

**Example Output:**

```text
eth0: inet xxx.xxx.x.xx/xx
```

**Selected Interface:**

```text
Interface: eth0
IP Address: xxx.xxx.x.xx
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

## 🧾 Rule Management

### Default Rule Directory

```text
/var/lib/suricata/rules/
```

### Update Rules

```bash
sudo suricata-update
```

### Verify Loaded Rules

```bash
ls /var/lib/suricata/rules/
```

> 📌 Rules used: **Emerging Threats Open**

---

## 🔄 Service Management

### Check Suricata Service Status

```bash
sudo systemctl status suricata
```

### Restart Suricata After Changes

```bash
sudo systemctl restart suricata
```

### Confirm IDS Mode

```bash
sudo journalctl -u suricata
```

Expected behavior:

```text
Suricata running in IDS mode
```

> ℹ️ Suricata defaults to **IDS mode** when started via `suricata.service`.

---

## 🧪 Testing & Validation

### Generate Basic Traffic

```bash
ping google.com
```

### Trigger Detection (Nmap Scan)

```bash
nmap -sS <target-ip>
```

### Monitor Alerts in Real Time

```bash
sudo tail -f /var/log/suricata/eve.json
```


---

## ⚠️ Common Issues & Troubleshooting

| Issue                  | Solution                       |
| ---------------------- | ------------------------------ |
| No alerts generated    | Verify interface configuration |
| Service fails to start | Check YAML syntax              |
| Empty log files        | Confirm traffic is flowing     |
| Wrong interface        | Re-check `ip a` output         |

---

## 🧠 Observations & Lessons Learned

* Suricata runs in IDS mode by default
* Configuration changes require a service restart
* AF_PACKET enables high-performance capture
* Logs provide SOC-ready investigation context

---

## 📈 Next Steps

* Integrate **Zeek** for protocol metadata
* Forward logs to **Wazuh / SIEM**
* Enable PCAP logging
* Tune rules and reduce false positives
* Transition to **IPS mode (NFQUEUE)**

---

## 📚 References

* [https://suricata.io](https://suricata.io)
* [https://docs.suricata.io](https://docs.suricata.io)
* [https://rules.emergingthreats.net](https://rules.emergingthreats.net)

---

## 👤 Author

**Olusegun Fajobi**
Cybersecurity / SOC Analyst
GitHub: `https://github.com/samfajobi`

---




