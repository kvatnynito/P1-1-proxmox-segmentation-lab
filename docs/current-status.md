# Current Status

## Current Milestone

- Milestone 5 — SIEM Intro

## Completed Milestones

- Milestone 1 — Foundation Start
- Milestone 2 — pfSense Working
- Milestone 3 — Internal LAN1 Base
- Milestone 4 — Attack Lab Base

## Current Focus

Milestone 5 focuses on building the initial Splunk SIEM server.

Primary goals:

- Confirm SIEM-SPLUNK01 exists.
- Confirm Ubuntu Server is installed on SIEM-SPLUNK01.
- Install Splunk on SIEM-SPLUNK01.
- Start Splunk services.
- Confirm Splunk Web UI is reachable.
- Document Splunk VM specs, IP address, install notes, and screenshots.

## Last Completed Task

- SIEM-SPLUNK01 VM was created.
- Ubuntu Server was installed on SIEM-SPLUNK01.
- System update/upgrade was completed.
- A snapshot was planned before installing Splunk.

## Current Task In Progress

- Installing Splunk on SIEM-SPLUNK01.

## Next Safe Step

- Confirm the VM is powered on and reachable.
- Confirm the Splunk installer package is available on SIEM-SPLUNK01.
- Install Splunk Enterprise.
- Start Splunk for the first time.
- Accept the license agreement.
- Create the Splunk admin account.
- Confirm Splunk Web UI is reachable from a LAN1 system.

## Known Blockers

- Splunk installation is not yet confirmed complete.
- Splunk Web UI reachability is not yet confirmed.
- pfSense syslog forwarding should not begin until Splunk is installed and reachable.
- Windows log forwarding should not begin until Splunk is installed and reachable.

## Active Systems

| System | Role | Network | Status |
|---|---|---|---|
| FW-EDGE01 | pfSense firewall/router | vmbr0 / vmbr1 / vmbr2 | Current |
| AD-DC01 | Domain Controller | LAN1 / vmbr1 | Current |
| TEST-WIN10-LAN1 | Windows LAN1 endpoint / future AD-WIN10 | LAN1 / vmbr1 | Current |
| TEST-WIN10-LAN2 | Windows LAN2 endpoint | LAN2 / vmbr2 | Current |
| ATTACK-KALI01 | Kali attack/admin VM | LAN2 / vmbr2 | Current |
| VULN-METASPLOITABLE2 | Vulnerable Linux target | LAN2 / vmbr2 | Current |
| SIEM-SPLUNK01 | Splunk SIEM server | LAN1 / vmbr1 | In progress |

## Current Log Source Status

| Source | Destination | Method | Port | Status |
|---|---|---|---:|---|
| FW-EDGE01 / pfSense | SIEM-SPLUNK01 | Syslog | UDP 514 | Planned for Milestone 6 / Not started |
| TEST-WIN10-LAN1 | SIEM-SPLUNK01 | Splunk Universal Forwarder | TCP 9997 | Planned for Milestone 6 / Not started |

## Milestone 5 Completion Criteria

Milestone 5 is complete only when:

- SIEM-SPLUNK01 exists.
- Ubuntu Server is installed.
- Splunk is installed.
- Splunk service starts successfully.
- Splunk Web UI is reachable.
- Splunk VM specs and IP address are documented.
- Installation notes are added to the repo.
- Screenshot or validation evidence is saved.

## Session Notes

Use this section to record where work stopped.

### Latest Session Note

- Currently in the middle of Milestone 5.
- SIEM-SPLUNK01 has Ubuntu Server installed.
- System update/upgrade has been completed.
- Splunk has not been fully installed or validated yet.
- Next session should resume with Splunk installation on SIEM-SPLUNK01.

## Next Session Resume Point

Start by confirming SIEM-SPLUNK01 is powered on, reachable, and ready for Splunk installation.

Then continue with installing Splunk Enterprise and validating Splunk Web UI access.

Do not proceed to Milestone 6 logging tasks until Splunk is installed and reachable.

## Documentation To Update As Work Progresses

- `docs/current-status.md`
- `docs/build-notes.md`
- `docs/vm-inventory.md`
- `docs/ip-addressing.md`
- `docs/architecture.md`
- `docs/00-lab-guide.md`
- screenshots under `screenshots/`

## Git Checkpoint Reminder

Before ending a work session:

1. Update this file with the latest stopping point.
2. Update any affected documentation files.
3. Run `git status`.
4. Run `git diff`.
5. Commit meaningful documentation updates.
6. Push changes to GitHub if the updates are portfolio-safe.
