## The **heart of how SOC analysts actually monitor Suricata in real time**

# 📁 Breakdown of Important Suricata Log Files

## 1️⃣ `eve.json` (MOST IMPORTANT)

📍 `/var/log/suricata/eve.json`

### What it logs

* Alerts
* Drops (IPS mode)
* DNS queries
* HTTP requests
* TLS handshakes
* Flows & metadata

### Why it matters

✔ Machine-readable
✔ Used by SIEMs (Wazuh, Splunk, ELK)
✔ Full context
✔ Real-time monitoring

✅ **Primary SOC log**

---

## 2️⃣ `fast.log` (Human-readable alerts)

📍 `/var/log/suricata/fast.log`

Example:

```text
04/15/2025-14:22:01 [**] [1:2024216:3] ET SCAN Nmap Scripting Engine [**]
```

### What it logs

* **Alerts only**
* No DNS / HTTP / flow context

### Why it exists

* Quick glance
* Legacy Snort-style viewing

⚠️ **Not enough for investigations**

---

## 3️⃣ `stats.log` (Performance & health)

📍 `/var/log/suricata/stats.log`

### What it logs

* Packets seen
* Packets dropped
* Decode errors
* CPU & memory usage

### Why SOCs use it

* Detect packet loss
* Performance tuning
* IPS health monitoring

---

## 4️⃣ `suricata.log` (Engine status)

📍 `/var/log/suricata/suricata.log`

### What it logs

* Startup errors
* Rule loading issues
* Interface problems

### Use case

* Troubleshooting
* Not for detection

---

## 5️⃣ `http.log`, `dns.log`, etc. (If enabled separately)

In older configs or special setups:

* Protocol-specific logs may exist
* In modern Suricata, these are usually **inside `eve.json`**

---

# 🧪 Why You Check `eve.json` *Before* Simulating an Attack

Before attacking, SOC analysts confirm:

✔ Suricata is running
✔ Traffic is visible
✔ Events are being logged
✔ Rules are firing

Example workflow:

```bash
sudo tail -f /var/log/suricata/eve.json
```

Then:

```bash
nmap -sS target
```

You immediately see:

* Flow events
* Alerts
* Drops (if IPS)

This confirms:

> “Suricata is actually seeing the traffic.”

---

# 🧠 Mapping Logs to SOC Tasks

| File           | SOC Use                                  |
| -------------- | ---------------------------------------- |
| `eve.json`     | Detection, investigation, SIEM ingestion |
| `fast.log`     | Quick alert confirmation                 |
| `stats.log`    | Performance & health                     |
| `suricata.log` | Troubleshooting                          |

---

# 🎯 Key Insight (Very Important)

> **If you understand `eve.json`, you understand Suricata.**

Everything else is:

* A filtered view
* A summary
* Or for debugging

---

# TL;DR (Memorize This)

* `eve.json` = full, structured, real-time security telemetry
* `fast.log` = quick alert summary
* `stats.log` = performance
* SOCs watch **`eve.json` live** before, during, and after attacks

---
