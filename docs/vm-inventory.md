# VM Inventory

This document tracks the virtual machine inventory for the Proxmox Segmentation Lab. This includes current deployment status, intended network placement, and its role within the environment.

---

## Current Deployment Status

### Deployed in Week 1

#### FW-EDGE01
- **Role:** pfSense edge firewall/router
- **Status:** Deployed
- **Network placement:**
  - NIC1 → `vmbr0` (WAN)
  - NIC2 → `vmbr1` (LAN1 Enterprise)
  - NIC3 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Primary routing and segmentation point between WAN, LAN1, and LAN2.

### Deployed in Week 2

#### AD-WIN10
- **Role:** Windows 10 enterprise workstation
- **Status:** Deployed
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **IP assignment:** DHCP from pfSense LAN1
- **Notes:** First internal Windows endpoint used to validate LAN1 connectivity, DHCP, and future domain/telemetry workflows.

### Planned for Later Phases

---

## LAN1 — Enterprise / Blue Team Zone

#### AD-DC01
- **Role:** Active Directory Domain Controller, DNS
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** Provides domain services, authentication, DNS, and future Group Policy support.

#### AD-WIN11
- **Role:** Windows 11 enterprise workstation
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** Secondary domain-joined endpoint for user activity simulation and telemetry generation.

#### AD-FS01
- **Role:** File server
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** Intended for SMB share testing, file access activity, and access control scenarios.

#### SIEM-SPLUNK01
- **Role:** Splunk server
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** Intended for centralized log search, triage, and detection workflows.

#### SEC-KALI01
- **Role:** Attacker simulation system
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise) or dual-homed later as needed
- **Notes:** Used to generate controlled attacker activity for validation and testing.

---

## LAN2 — Vulnerable / Testing Zone

#### VULN-METASPLOITABLE2
- **Role:** Intentionally vulnerable Linux target
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Used for exploitation, segmentation validation, and known-bad telemetry generation.

#### VULN-DVWA
- **Role:** Deliberately vulnerable web application target
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Used for web attack testing and logging visibility validation.

#### VULN-WIN2019
- **Role:** Intentionally unpatched Windows Server target
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Used for Windows exploitation, lateral movement simulation, and event analysis.

#### VULN-OPENVAS
- **Role:** Vulnerability scanner
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Used for scan / remediate / rescan workflow testing.

#### VULN-UBU-OLD
- **Role:** Outdated Linux target
- **Status:** Planned
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Used to simulate legacy Linux risk and misconfiguration scenarios.

---

## Overall Notes
- `FW-EDGE01` is the only system currently deployed in the lab.
- `AD-WIN10` is the first deployed internal endpoint for Week 2 validation.
- Additional systems will be deployed in later phases as the lab build progresses.
- Inventory entries may be refined as implementation details change.
