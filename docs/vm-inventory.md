# VM Inventory

This document tracks the virtual machine inventory for the Proxmox Segmentation Lab. This includes current deployment status, intended network placement, and its role within the environment.

---

## Current Deployment Status

### Deployed in Milestone 1

#### FW-EDGE01
- **Role:** pfSense edge firewall/router
- **Status:** Deployed and operational
- **Network placement:**
  - NIC1 → `vmbr0` (WAN)
  - NIC2 → `vmbr1` (LAN1 Enterprise)
  - NIC3 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Primary routing and segmentation point between WAN, LAN1, and LAN2. Web UI access validated and DHCP configured for LAN1 and LAN2.

### Deployed in Milestone 2

#### AD-WIN10
- **Role:** Windows 10 enterprise workstation
- **Status:** Deployed for internal endpoint validation
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** First deployed internal endpoint, used to validate LAN1 connectivity, pfSense Web UI access, and DHCP behavior.

#### TEST-WIN10-LAN2
- **Role:** Windows 10 validation endpoint
- **Status:** Deployed for LAN2 validation
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Used to validate DHCP assignment and basic connectivity on the LAN2 / vulnerable segment.

### Deployed in Milestone 3

#### AD-DC01
- **Role:** Active Directory Domain Controller, DNS
- **Status:** Deployed and network validated
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** First enterprise server deployed on LAN1. Configured with static IP `10.10.10.10`, gateway `10.10.10.1`, and DNS `10.10.10.1`. Connectivity to pfSense and external resources was validated after correcting the DNS entry.

### Deployed in Milestone 4

#### ATTACK-KALI01
- **Role:** Attacker simulation system
- **Status:** Deployed and network validated
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** Kali VM used to establish the attack-side baseline on the isolated vulnerable segment.

#### VULN-METASPLOITABLE2
- **Role:** Intentionally vulnerable Linux target
- **Status:** Deployed and network validated
- **Network placement:**
  - NIC1 → `vmbr2` (LAN2 Vulnerable)
- **Notes:** First vulnerable target deployed on LAN2. Communication with `ATTACK-KALI01` was validated within the isolated segment.

### Deployed in Milestone 5

#### SIEM-SPLUNK01
- **Role:** Splunk server
- **Status:** Deployed and operational
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** Ubuntu Server-based Splunk host configured with static IP `10.10.10.20`. Splunk was installed successfully and Web UI access was confirmed from LAN1.

### Planned for Later Phases

---

## LAN1 — Enterprise / Blue Team Zone

#### AD-DC01
- **Role:** Active Directory Domain Controller, DNS
- **Status:** Deployed
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
- **Status:** Deployed
- **Network placement:**
  - NIC1 → `vmbr1` (LAN1 Enterprise)
- **Notes:** Used for centralized log search, triage, and detection workflows.

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
- **Status:** Deployed
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
- `FW-EDGE01` was deployed in Milestone 1 and is operational as the lab edge firewall/router.
- `AD-WIN10` was deployed in Milestone 2 for LAN1 validation and DHCP testing.
- `TEST-WIN10-LAN2` was deployed in Milestone 2 for LAN2 validation.
- `AD-DC01` was deployed in Milestone 3 as the first enterprise server on LAN1.
- `ATTACK-KALI01` and `VULN-METASPLOITABLE2` were deployed in Milestone 4 to establish the attack and vulnerable segment on LAN2.
- `SIEM-SPLUNK01` was deployed in Milestone 5 as the first SIEM server on LAN1.
- Additional systems will be deployed in later phases as the lab build progresses.
- Inventory entries may be refined as implementation details change.
