# Suricata Configuration: Why It Matters!!!

Suricata does **not magically start detecting threats** the moment it’s installed.  
Its effectiveness depends heavily on **how it is configured**.

The `suricata.yaml` file defines **how, where, and what** Suricata monitors on a network.

Below are some **key aspects controlled by the Suricata configuration**:

---

## 🔹 Network Interface Selection
Suricata must be **explicitly told which network interface to monitor**.

Without this:
- No traffic is inspected  
- No alerts are generated  

This is why identifying the correct interface (for example, using `ip a`) is critical before running Suricata.

---



