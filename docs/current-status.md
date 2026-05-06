# Current Status

## Current Milestone

- Milestone 6 — Logging Foundation

## Completed Milestones

- Milestone 1 — Foundation Start
- Milestone 2 — pfSense Working
- Milestone 3 — Internal LAN1 Base
- Milestone 4 — Attack Lab Base
- Milestone 5 — SIEM Intro

## Current Focus

Milestone 6 focuses on making logs flow into Splunk.

Primary goals:

- Confirm Splunk is installed and reachable.
- Configure Splunk to receive pfSense syslog.
- Configure pfSense to forward logs to SIEM-SPLUNK01.
- Verify pfSense firewall logs appear in Splunk.
- Configure Windows log forwarding from TEST-WIN10-LAN1.
- Verify Windows logs appear in Splunk.
- Document log source IPs, ports, searches, and screenshots.

## Last Completed Task

- SIEM-SPLUNK01 VM was created.
- Ubuntu Server was installed on SIEM-SPLUNK01.
- System update/upgrade was completed.
- SIEM-SPLUNK01 was confirmed on static IP `10.10.10.20`.
- LAN1 gateway, outbound IP reachability, and DNS resolution were validated.
- Splunk Enterprise 10.2.3 was installed from a Linux `.deb` package.
- Splunk was configured to run as the `splunk` service user.
- Splunk boot-start was enabled through `systemd`.
- Splunk Web UI was validated from TEST-WIN10-LAN1 at `http://10.10.10.20:8000`.

## Current Task In Progress

- Milestone 6 has not started yet. The next task is to configure Splunk to receive pfSense syslog.

## Next Safe Step

- Confirm `Splunkd` is active on SIEM-SPLUNK01.
- Create the first Splunk network input for pfSense syslog.
- Configure pfSense remote logging to send firewall logs to SIEM-SPLUNK01.
- Validate pfSense events in Splunk before beginning Windows forwarding.

## Known Blockers

- pfSense syslog forwarding has not started.
- Windows log forwarding has not started.
- A sanitized Splunk Web UI screenshot should be used for GitHub evidence; troubleshooting screenshots that show Proxmox management details should not be published.

## Active Systems

| System | Role | Network | Status |
|---|---|---|---|
| FW-EDGE01 | pfSense firewall/router | vmbr0 / vmbr1 / vmbr2 | Current |
| AD-DC01 | Domain Controller | LAN1 / vmbr1 | Current |
| TEST-WIN10-LAN1 | Windows LAN1 endpoint / future AD-WIN10 | LAN1 / vmbr1 | Current |
| TEST-WIN10-LAN2 | Windows LAN2 endpoint | LAN2 / vmbr2 | Current |
| ATTACK-KALI01 | Kali attack/admin VM | LAN2 / vmbr2 | Current |
| VULN-METASPLOITABLE2 | Vulnerable Linux target | LAN2 / vmbr2 | Current |
| SIEM-SPLUNK01 | Splunk SIEM server | LAN1 / vmbr1 | Current |

## Current Log Source Status

| Source | Destination | Method | Port | Status |
|---|---|---|---:|---|
| FW-EDGE01 / pfSense | SIEM-SPLUNK01 | Syslog | UDP 514 | Planned for Milestone 6 / Not started |
| TEST-WIN10-LAN1 | SIEM-SPLUNK01 | Splunk Universal Forwarder | TCP 9997 | Planned for Milestone 6 / Not started |

## Milestone 6 Completion Criteria

Milestone 6 is complete only when:

- pfSense forwards logs to SIEM-SPLUNK01.
- Splunk displays pfSense logs.
- TEST-WIN10-LAN1 sends logs to Splunk.
- Splunk displays Windows logs.
- GitHub documentation includes source IPs, ports, screenshots, and validation searches.

## Session Notes

Use this section to record where work stopped.

### Latest Session Note

- Milestone 5 is complete.
- SIEM-SPLUNK01 has Ubuntu Server installed with static IP `10.10.10.20`.
- Splunk Enterprise 10.2.3 was installed from the official Linux `.deb` package.
- Splunk was started as the `splunk` service user after root startup was rejected by Splunk 10.2.
- `/opt/splunk` ownership was set to `splunk:splunk`.
- Splunk boot-start was enabled with `systemd`.
- Splunk Web UI was reached from TEST-WIN10-LAN1 at `http://10.10.10.20:8000`.
- WinSCP/SFTP from the outside Windows host was not used for the installer because the host-to-LAN1 path was blocked by the lab segmentation/pfSense path.
- Direct `wget` from SIEM-SPLUNK01 worked because the VM had validated outbound internet and DNS.

## Next Session Resume Point

Start Milestone 6 by confirming Splunk is active:

```bash
sudo systemctl status Splunkd
```

Then configure Splunk to receive pfSense syslog and validate pfSense events in Splunk before starting Windows log forwarding.

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
