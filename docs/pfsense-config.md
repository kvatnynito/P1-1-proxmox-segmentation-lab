# pfSense Configuration

## Status
Deployed in Proxmox on April 6, 2026.

## Interface Mapping
- WAN -> vmbr0
- LAN1 -> vmbr1
- LAN2 -> vmbr2

## Initial Interface IPs
- LAN1: 10.10.10.1/24
- LAN2: 10.20.20.1/24
- WAN: upstream/home router via vmbr0

## Notes
- pfSense is acting as the routing and segmentation point between all three zones.
- At this stage, the VM has been deployed and interfaces assigned.
- Web UI validation and DHCP setup are part of Week 2.

## Evidence
- screenshots/pfsense-interfaces.png
- screenshots/pfsense-console-assignment.png
- screenshots/pfsense-install-complete.png
