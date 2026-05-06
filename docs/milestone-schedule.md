# Milestone Schedule

## Purpose

This file is the roadmap source of truth for the Proxmox Segmentation Lab.

Use this file to track:

- milestone order
- milestone goals
- planned VM additions
- completion criteria
- portfolio artifact ideas

This file shows the intended project roadmap for P1-1 only. For the current live stopping point, use:

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
- Milestone 5 — SIEM Intro

## Current Note

P1-1 is complete at Milestone 5.

The segmented lab now includes:

- `FW-EDGE01`
- `AD-DC01`
- `TEST-WIN10-LAN1`
- `TEST-WIN10-LAN2`
- `ATTACK-KALI01`
- `VULN-METASPLOITABLE2`
- `SIEM-SPLUNK01`

Splunk Enterprise has been installed on `SIEM-SPLUNK01`, and Splunk Web UI access was validated from LAN1.

Telemetry onboarding, Windows log forwarding, WEF, Sysmon, multi-platform ingestion validation, and additional telemetry-supporting VM expansion continue in `P1-2-wef-sysmon-to-wazuh-elastic-splunk`.

---

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

Completed.

---

# Milestone Tracker Reference

Use the milestone tracker in `README.md` as the public-facing progress summary.

Use this file as the detailed internal roadmap and milestone-definition reference.

If `README.md` and this file ever disagree, update both so milestone status, stopping point, and next action stay aligned.

For P1-1, the milestone tracker ends at Milestone 5.

---

# Final VM Build Map

## Built in P1-1

| VM Name | Role |
|---|---|
| FW-EDGE01 | pfSense firewall/router |
| AD-DC01 | Domain Controller |
| TEST-WIN10-LAN1 | LAN1 Windows endpoint / future AD-WIN10 |
| TEST-WIN10-LAN2 | LAN2 Windows endpoint |
| ATTACK-KALI01 | Kali attack/admin VM |
| VULN-METASPLOITABLE2 | Vulnerable Linux target |
| SIEM-SPLUNK01 | Splunk SIEM server |

## Planned Beyond P1-1

The following systems are not tracked as P1-1 milestones. They may be added later as part of P1-2 when they support telemetry, detection, or investigation workflows:

- `LAN1-FILE01`
- `SCAN-OPENVAS01`
- `VULN-DVWA01`
- `AD-WIN11`
- `TEST-WIN2019-LAN2`
- `VULN-WEBGOAT01`
- `VULN-UBU-OLD`

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
| `FW-EDGE01` | Current |
| `SIEM-SPLUNK01` | Current |
| `LAN1-FILE01` | Planned in P1-2 |
| `VULN-WEBGOAT01` | Optional in P1-2 |

Rule:

- The diagram can be ambitious, but it must stay honest.
- Do not imply a VM is already built if it is only planned.

---

# Milestone Update Rules

When a milestone is completed, update:

- `README.md`
- `docs/current-status.md`
- `docs/milestone-schedule.md`
- `docs/build-notes.md`
- `docs/vm-inventory.md`
- `docs/ip-addressing.md`
- any affected firewall, pfSense, Splunk, or network documentation
- screenshots under `screenshots/`

Do not mark a milestone complete unless the completion criteria are met and validation evidence exists.

A milestone is not complete just because a VM exists. It is complete when the intended function works and evidence has been documented.

Examples:

- Milestone 5 is not complete just because `SIEM-SPLUNK01` exists.
- Milestone 5 is complete when Splunk is installed, running, reachable, and documented.

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
docs/milestone-05-splunk-install-validation.md
```

---

# Validation Standard

Every major lab task should include proof.

Good validation examples:

- Ping test
- Web UI access
- Static IP confirmation
- Screenshot
- Short explanation of what the result proves

Bad validation examples:

- "It worked"
- "Configured"
- "Done"
- "Installed"
