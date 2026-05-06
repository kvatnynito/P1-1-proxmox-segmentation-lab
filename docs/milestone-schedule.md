# Milestone Schedule

## Purpose

This file is the roadmap source of truth for the Proxmox Segmentation Lab.

Use this file to track:

- milestone order
- milestone goals
- planned VM additions
- completion criteria
- portfolio artifact ideas
- when detection work should begin

This file shows the intended project roadmap. For the current live stopping point, use:

- `docs/current-status.md`

---

# Current Project Position

## Current Milestone

- Milestone 5 — SIEM Intro

## Completed Milestones

- Milestone 1 — Foundation Start
- Milestone 2 — pfSense Working
- Milestone 3 — Internal LAN1 Base
- Milestone 4 — Attack Lab Base

## Current Note

The lab is currently in Milestone 5.

SIEM-SPLUNK01 has been created and Ubuntu Server has been installed. Splunk installation and Splunk Web UI validation are still in progress.

Do not move into Milestone 6 until Splunk is installed, started, reachable through the web interface, and documented.

---

# Phase 1 — Foundation Build

## Milestone 1 — Foundation Start

### Goal

Start the lab and create the pfSense VM.

### Tasks

- Create GitHub repo.
- Create README.
- Check Proxmox.
- Create VM planning documentation.
- Optionally download pfSense ISO.
- Create FW-EDGE01.

### Expected Result

- GitHub repo exists.
- Basic project documentation exists.
- FW-EDGE01 VM exists or is ready for configuration.

### Status

Completed.

---

## Milestone 2 — pfSense Working

### Goal

Get pfSense working as the lab router/firewall.

### Tasks

- Assign WAN/LAN interfaces.
- Access pfSense web UI.
- Configure DHCP and LAN setup.
- Verify basic firewall/router function.

### Expected Result

- pfSense web UI is reachable.
- LAN interfaces are assigned.
- DHCP and gateway behavior are working.
- Basic routing/firewall function is validated.

### Status

Completed.

---

## Milestone 3 — Internal LAN1 Base

### Goal

Build the internal LAN1 enterprise network base.

### Tasks

- Create AD-DC01.
- Connect AD-DC01 to LAN1 / vmbr1.
- Configure static IP for AD-DC01.
- Create TEST-WIN10-LAN1.
- Connect TEST-WIN10-LAN1 to LAN1 / vmbr1.
- Test LAN1 connectivity.
- Later, TEST-WIN10-LAN1 may become AD-WIN10 after domain join.

### Expected LAN1 Systems

- AD-DC01
- TEST-WIN10-LAN1

### Expected Result

- LAN1 has a domain controller base system.
- LAN1 has a Windows endpoint.
- LAN1 connectivity is validated.

### Status

Completed.

---

## Milestone 4 — Attack Lab Base

### Goal

Build the LAN2 attack/vulnerable lab base.

### Tasks

- Create ATTACK-KALI01.
- Connect Kali to LAN2 / vmbr2.
- Create or import VULN-METASPLOITABLE2.
- Connect Metasploitable2 to LAN2 / vmbr2.
- Keep or create TEST-WIN10-LAN2 for segmentation testing.
- Verify Kali can communicate with LAN2 targets.
- Verify LAN2 cannot freely access LAN1 if blocked by firewall rules.

### Expected LAN2 Systems

- ATTACK-KALI01
- VULN-METASPLOITABLE2
- TEST-WIN10-LAN2

### Expected Result

- LAN2 has an attacker/admin VM.
- LAN2 has at least one vulnerable target.
- Segmentation between LAN1 and LAN2 can be tested.

### Status

Completed.

---

## Milestone 5 — SIEM Intro

### Goal

Build the initial Splunk SIEM server.

### Tasks

- Create SIEM-SPLUNK01.
- Connect SIEM-SPLUNK01 to LAN1 / vmbr1.
- Install Ubuntu Server.
- Install Splunk.
- Start Splunk services.
- Access Splunk web UI.
- Document Splunk VM specs and IP address.
- Take screenshot for repo.

### Expected Baseline Systems By End of Milestone 5

- FW-EDGE01
- AD-DC01
- TEST-WIN10-LAN1
- TEST-WIN10-LAN2
- ATTACK-KALI01
- VULN-METASPLOITABLE2
- SIEM-SPLUNK01

### Completion Criteria

Milestone 5 is complete only when:

- SIEM-SPLUNK01 exists.
- Ubuntu Server is installed.
- Splunk is installed.
- Splunk service starts successfully.
- Splunk Web UI is reachable.
- Splunk VM specs and IP address are documented.
- Installation notes are added to the repo.
- Screenshot or validation evidence is saved.

### Portfolio Artifact Ideas

- `docs/milestone-05-splunk-server-setup.md`
- `docs/milestone-05-splunk-install-validation.md`

### Status

In progress.

---

## Milestone 6 — Logging Foundation

### Goal

Make logs actually flow into Splunk.

### Core Rule

Do not add more VMs during this milestone unless Splunk logging is working first.

### Tasks

- Confirm Splunk is installed.
- Confirm Splunk Web UI is reachable.
- Configure Splunk to receive pfSense syslog.
- Configure pfSense logs to forward to SIEM-SPLUNK01.
- Verify pfSense firewall logs appear in Splunk.
- Configure Windows logging from TEST-WIN10-LAN1.
- Prefer Splunk Universal Forwarder for the first Windows source unless there is a reason to use Windows Event Forwarding.
- Verify Windows logs appear in Splunk.
- Document log sources in GitHub.

### Expected Log Source Map

| Source | Destination | Method | Port | Status |
|---|---|---|---:|---|
| FW-EDGE01 / pfSense | SIEM-SPLUNK01 | Syslog | UDP 514 | Planned |
| TEST-WIN10-LAN1 | SIEM-SPLUNK01 | Splunk Universal Forwarder | TCP 9997 | Planned |

### Completion Criteria

Milestone 6 is complete only when:

- pfSense forwards logs to SIEM-SPLUNK01.
- Splunk displays pfSense logs.
- TEST-WIN10-LAN1 sends logs to Splunk.
- Splunk displays Windows logs.
- GitHub documentation includes source IPs, ports, screenshots, and validation searches.

### Portfolio Artifact Ideas

- `docs/milestone-06-logging-foundation.md`
- `docs/milestone-06-splunk-pfsense-syslog-setup.md`
- `docs/milestone-06-windows-forwarder-onboarding.md`

### Status

Planned.

---

## Milestone 7 — LAN1 File Server Logging

### Goal

Expand LAN1 enterprise logging.

### Tasks

- Create LAN1-FILE01.
- Connect LAN1-FILE01 to LAN1 / vmbr1.
- Configure static IP.
- Join LAN1-FILE01 to the domain if AD is ready.
- Create basic SMB file share.
- Generate test user activity:
  - successful logon
  - failed logon
  - file access
  - file creation
  - file deletion
- Send LAN1-FILE01 Windows logs to Splunk.
- Verify file server logs appear in Splunk.
- Document screenshots and findings.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| LAN1-FILE01 | File server / SMB logging practice | LAN1 / vmbr1 | Planned Milestone 7 |

### Why This Matters

This VM creates realistic enterprise logs, including SMB access, authentication events, permissions mistakes, failed logons, and later ransomware-style simulation opportunities.

### Portfolio Artifact Ideas

- `docs/milestone-07-file-server-logging-lab.md`
- `docs/milestone-07-smb-activity-validation.md`

### Status

Planned.

---

## Milestone 8 — IDS Setup with Suricata

### Goal

Add IDS visibility using Suricata.

### Tasks

- Install Suricata on pfSense.
- Enable selected rules.
- Configure Suricata interfaces carefully.
- Generate basic test alerts.
- Send or review Suricata alerts.
- Document rule categories and screenshots.

### Important Rule

Do not enable every rule. Avoid false-positive overload.

### Portfolio Artifact Ideas

- `docs/milestone-08-suricata-ids-setup.md`
- `docs/milestone-08-suricata-basic-alerts.md`

### Status

Planned.

---

## Milestone 9 — First Attack Detection

### Goal

Run the first basic attack detection workflow.

### Tasks

- Learn basic Nmap scan types.
- Run scans from ATTACK-KALI01 against VULN-METASPLOITABLE2.
- Run scans from ATTACK-KALI01 against TEST-WIN10-LAN2.
- Observe firewall logs in Splunk.
- Observe Suricata alerts.
- Investigate scan activity in Splunk.
- Document one detection story.

### Portfolio Artifact Ideas

- `docs/milestone-09-nmap-scan-investigation.md`

### Status

Planned.

---

## Milestone 10 — Vulnerability Scanning

### Goal

Add vulnerability scanning.

### Tasks

- Create SCAN-OPENVAS01.
- Connect SCAN-OPENVAS01 to LAN2 / vmbr2.
- Install Greenbone/OpenVAS.
- Configure scanner.
- Scan VULN-METASPLOITABLE2.
- Scan TEST-WIN10-LAN2.
- Export or screenshot scan results.
- Review pfSense/Splunk/Suricata logs generated by scanning.
- Document findings.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| SCAN-OPENVAS01 | Vulnerability scanner | LAN2 / vmbr2 | Planned Milestone 10 |

### Naming Note

Use `SCAN-OPENVAS01`, not `VULN-OPENVAS01`.

OpenVAS is the scanner, not the victim.

### Portfolio Artifact Ideas

- `docs/milestone-10-openvas-scanner-setup.md`
- `docs/milestone-10-vulnerability-scan-results.md`
- `docs/milestone-10-openvas-scan-log-review.md`

### Status

Planned.

---

## Milestone 11 — DVWA Vulnerable Web App

### Goal

Add a vulnerable web application target.

### Tasks

- Create VULN-DVWA01.
- Connect VULN-DVWA01 to LAN2 / vmbr2.
- Install Ubuntu Server.
- Install Docker.
- Deploy DVWA.
- Confirm DVWA web UI is reachable from ATTACK-KALI01.
- Generate basic web traffic.
- Verify web traffic appears in firewall/Splunk logs.
- Document install and screenshots.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| VULN-DVWA01 | Deliberately vulnerable web application | LAN2 / vmbr2 | Planned Milestone 11 |

### Portfolio Artifact Ideas

- `docs/milestone-11-dvwa-setup.md`
- `docs/milestone-11-dvwa-traffic-validation.md`

### Status

Planned.

---

## Milestone 12 — DVWA Web Attack Detection

### Goal

Detect DVWA attack activity.

### Tasks

- Perform beginner DVWA exercises.
- Generate web attack traffic:
  - command injection
  - SQL injection
  - brute force login
- Review Suricata alerts.
- Review pfSense logs.
- Review Splunk logs.
- Document one web attack investigation.

### Portfolio Artifact Ideas

- `docs/milestone-12-dvwa-web-attack-detection.md`

### Status

Planned.

---

## Milestone 13 — Add AD-WIN11 Endpoint

### Goal

Add a second LAN1 endpoint.

### Tasks

- Create AD-WIN11.
- Connect AD-WIN11 to LAN1 / vmbr1.
- Join AD-WIN11 to domain.
- Install Splunk Universal Forwarder or configure Windows log collection.
- Generate endpoint activity:
  - logon
  - failed logon
  - PowerShell usage
  - file share access
- Verify logs in Splunk.
- Document endpoint onboarding.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| AD-WIN11 | Second domain-joined Windows endpoint | LAN1 / vmbr1 | Planned Milestone 13 |

### Portfolio Artifact Ideas

- `docs/milestone-13-ad-win11-onboarding.md`
- `docs/milestone-13-windows-endpoint-log-validation.md`

### Status

Planned.

---

## Milestone 14 — Windows Server Target

### Goal

Add a Windows Server target for LAN2.

### Tasks

- Create TEST-WIN2019-LAN2.
- Connect TEST-WIN2019-LAN2 to LAN2 / vmbr2.
- Install Windows Server 2019 evaluation.
- Configure static IP.
- Enable selected services for testing:
  - RDP
  - SMB/file sharing
  - local users
- Generate Windows Server logs.
- Send logs to Splunk if desired.
- Document baseline configuration.

### Naming Rule

Name it first as `TEST-WIN2019-LAN2`.

Later, when intentionally weakened, document it as `VULN-WIN2019`.

Do not call it vulnerable before it is actually misconfigured.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| TEST-WIN2019-LAN2 | Windows Server test target | LAN2 / vmbr2 | Planned Milestone 14 |
| VULN-WIN2019 | Intentionally weakened Windows Server target | LAN2 / vmbr2 | Future state after misconfiguration |

### Portfolio Artifact Ideas

- `docs/milestone-14-windows-server-target-setup.md`
- `docs/milestone-14-windows-server-log-baseline.md`

### Status

Planned.

---

## Milestone 15 — Optional WebGoat Target

### Goal

Add an optional second vulnerable web training app.

### Tasks

- Create VULN-WEBGOAT01.
- Connect VULN-WEBGOAT01 to LAN2 / vmbr2.
- Install Ubuntu Server.
- Install Docker.
- Deploy WebGoat.
- Confirm access from ATTACK-KALI01.
- Generate basic web traffic.
- Document setup.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| VULN-WEBGOAT01 | Vulnerable web training app | LAN2 / vmbr2 | Optional Milestone 15 |

### Status

Optional / Planned.

---

## Milestone 16 — Optional Outdated Linux Target

### Goal

Add an optional outdated Linux target.

### Tasks

- Create VULN-UBU-OLD.
- Connect VULN-UBU-OLD to LAN2 / vmbr2.
- Install older Ubuntu version.
- Configure selected services.
- Avoid full hardening.
- Scan with OpenVAS.
- Review vulnerability results.
- Document findings.

### Add This VM

| VM Name | Role | Network | Status |
|---|---|---|---|
| VULN-UBU-OLD | Outdated Linux target | LAN2 / vmbr2 | Optional Milestone 16 |

### Status

Optional / Planned.

---

# Phase 2 — Detection and Response Direction

True detection-and-response cycles should start around Milestone 12 or Milestone 13.

This shift is intentional:

- More infrastructure was added to the build plan.
- The lab should not fake detection work before telemetry and targets exist.
- Better to shift the timeline than pretend the environment is ready.

## Detection Cycle Format

Each detection milestone should include:

1. One attack or simulated suspicious activity.
2. One detection.
3. One investigation.
4. One GitHub update.

## Example Detection Rotation

| Milestone | Focus |
|---|---|
| Milestone 12 | DVWA web attack detection |
| Milestone 13 | Windows endpoint log analysis |
| Milestone 14 | Windows Server scanning/logging |
| Milestone 15 | WebGoat web traffic detection |
| Milestone 16 | OpenVAS scan investigation |
| Milestone 17 | Brute force detection |
| Milestone 18 | Lateral movement simulation |
| Milestone 19 | File share abuse investigation |
| Milestone 20 | Firewall rule validation |
| Milestone 21 | Suricata alert tuning |

---

# Final VM Build Map

## Already Built / Current

| VM Name | Role |
|---|---|
| FW-EDGE01 | pfSense firewall/router |
| AD-DC01 | Domain Controller |
| TEST-WIN10-LAN1 | LAN1 Windows endpoint / future AD-WIN10 |
| TEST-WIN10-LAN2 | LAN2 Windows endpoint |
| ATTACK-KALI01 | Kali attack/admin VM |
| VULN-METASPLOITABLE2 | Vulnerable Linux target |
| SIEM-SPLUNK01 | Splunk SIEM server |

## Added to Schedule

| VM Name | Planned Milestone | Role |
|---|---:|---|
| LAN1-FILE01 | Milestone 7 | File server / SMB logging |
| SCAN-OPENVAS01 | Milestone 10 | Vulnerability scanner |
| VULN-DVWA01 | Milestone 11 | Vulnerable web app |
| AD-WIN11 | Milestone 13 | Second LAN1 endpoint |
| TEST-WIN2019-LAN2 | Milestone 14 | Windows Server target |
| VULN-WEBGOAT01 | Milestone 15 | Optional vulnerable web app |
| VULN-UBU-OLD | Milestone 16 | Optional outdated Linux target |

## Build Priority If Time or Hardware Gets Tight

Build in this order:

1. LAN1-FILE01
2. VULN-DVWA01
3. SCAN-OPENVAS01
4. AD-WIN11
5. TEST-WIN2019-LAN2
6. VULN-WEBGOAT01
7. VULN-UBU-OLD

Reason:

- This order gives the most logging and portfolio value first.

---

# Diagram Status Labels

The network diagram can include current, planned, and optional systems, but each system must have a clear status label.

Use these labels:

- Current
- Planned
- Optional
- Future

Examples:

| System | Diagram Label |
|---|---|
| LAN1-FILE01 | Planned Milestone 7 |
| VULN-DVWA01 | Planned Milestone 11 |
| VULN-WEBGOAT01 | Optional Milestone 15 |

Rule:

- The diagram can be ambitious, but it must stay honest.
- Do not imply a VM is already built if it is only planned.

---

# Milestone Update Rules

When a milestone is completed, update:

- `docs/current-status.md`
- `docs/milestone-schedule.md`
- `docs/build-notes.md`
- `docs/vm-inventory.md`
- `docs/ip-addressing.md`
- any affected firewall, pfSense, Splunk, logging, or network documentation
- screenshots under `screenshots/`

Do not mark a milestone complete unless the completion criteria are met and validation evidence exists.

A milestone is not complete just because a VM exists. It is complete when the intended function works and evidence has been documented.

Examples:

- Milestone 5 is not complete just because SIEM-SPLUNK01 exists.
- Milestone 5 is complete when Splunk is installed, running, reachable, and documented.
- Milestone 6 is not complete just because pfSense forwarding was configured.
- Milestone 6 is complete when logs are visible in Splunk and documented.

---

# Documentation Expectations Per Milestone

Each milestone should produce or update at least one GitHub artifact.

Common documentation files to update:

- `README.md`
- `docs/current-status.md`
- `docs/milestone-schedule.md`
- `docs/build-notes.md`
- `docs/vm-inventory.md`
- `docs/ip-addressing.md`
- `docs/architecture.md`
- `docs/firewall-policy.md`
- `docs/pfsense-config.md`
- `docs/proxmox-bridges.md`

Milestone-specific artifacts should use this naming pattern:

```text
docs/milestone-XX-topic-name.md
```

Examples:

```text
docs/milestone-05-splunk-server-setup.md
docs/milestone-06-logging-foundation.md
docs/milestone-06-pfsense-syslog-to-splunk.md
docs/milestone-06-windows-logs-to-splunk.md
docs/milestone-09-nmap-scan-investigation.md
docs/milestone-12-dvwa-web-attack-detection.md
```

---

# Validation Standard

Every major lab task should include proof.

Good validation examples:

- Ping test
- Web UI access
- Static IP confirmation
- Firewall log entry
- Splunk search result
- Windows Event Log entry
- Suricata alert
- OpenVAS scan result
- Screenshot
- Short explanation of what the result proves

Bad validation examples:

- "It worked"
- "Configured"
- "Done"
- "Installed"

