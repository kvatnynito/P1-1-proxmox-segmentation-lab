# VM Inventory

This document tracks the virtual machine inventory for the Proxmox Segmentation Lab.

## Current Deployment Status

### Deployed
- **FW-EDGE01** — pfSense edge firewall/router
  - NIC1 → `vmbr0` (WAN)
  - NIC2 → `vmbr1` (LAN1 Enterprise)
  - NIC3 → `vmbr2` (LAN2 Vulnerable)

### Planned
The following systems are part of the intended lab design and will be deployed in later build phases.

---

## Edge Router

- **FW-EDGE01** — pfSense edge firewall/router  
  **Role:** Routes traffic between WAN, LAN1, and LAN2 while enforcing segmentation and firewall policy.  
  **Network placement:**
  - NIC1 → `vmbr0` (WAN)
  - NIC2 → `vmbr1` (LAN1 Enterprise)
  - NIC3 → `vmbr2` (LAN2 Vulnerable)

---

## LAN1 — Enterprise / Blue Team (Production-like Zone)

- **AD-DC01** *(Windows Server)* — Domain Services, DNS  
  **Why it’s included:** I wanted a realistic enterprise identity backbone for domain authentication, DNS, and policy-driven testing.

- **AD-WIN10 / AD-WIN11** *(Domain-joined endpoints)* — User workstations  
  **Why it’s included:** These are my “real user” machines to generate authentic endpoint activity for monitoring and investigations, including logons, process execution, PowerShell activity, and Sysmon/WEF telemetry.

- **AD-FS01** *(File Server — optional but recommended)* — SMB shares, NTFS permissions  
  **Why it’s included:** File servers create the kind of everyday east-west traffic enterprises actually have, and they’re useful for access auditing scenarios such as SMB authentication, share access, and permission changes.

- **SIEM-SPLUNK01** *(Splunk Free — optional)*  
  **Why it’s included:** I use this to centralize logs and practice investigation workflows such as searching, filtering, pivoting, and repeatable triage.

- **SEC-KALI01** *(Attacker simulation — optional)*  
  **Why it’s included:** This gives me a controlled way to generate adversary-like activity so I can validate segmentation rules and detection coverage without touching anything outside the lab.

---

## LAN2 — Vulnerable / Testing (Intentionally Insecure Zone)

- **VULN-METASPLOITABLE2**  
  **Why it’s included:** It’s a consistent, repeatable vulnerable target that lets me test segmentation controls and generate known-bad telemetry.

- **VULN-DVWA / WebGoat**  
  **Why it’s included:** These provide web application attack practice targets so I can generate realistic web attack signals and evaluate logging and detection visibility.

- **VULN-WIN2019** *(Unpatched)*  
  **Why it’s included:** I wanted a Windows target that supports exploitation and lateral movement practice while giving me Windows event and Sysmon investigation opportunities.

- **VULN-OPENVAS** *(Scanner)*  
  **Why it’s included:** This supports a vulnerability management workflow: scan, review findings, remediate, and rescan to confirm improvements.

- **VULN-UBU-OLD** *(Outdated Linux)*  
  **Why it’s included:** I use an intentionally outdated Linux system to simulate legacy risk and test hardening gaps and detection visibility.

---

## Notes
- **FW-EDGE01** is currently deployed.
- Remaining systems listed here are planned as part of the lab roadmap for Repo 1.
- Inventory may be adjusted during implementation based on system resources and lab priorities.
