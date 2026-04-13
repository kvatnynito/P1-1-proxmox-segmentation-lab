# pfSense Configuration

## Status
Deployed in Proxmox on April 6, 2026.
Week 2 configuration completed on April 13, 2026.

## Purpose
FW-EDGE01 serves as the lab’s edge firewall/router and enforces segmentation between the WAN, Enterprise LAN, and Vulnerable LAN.

## Interface Mapping
- WAN -> `vmbr0`
- LAN1 -> `vmbr1`
- LAN2 / OPT1 -> `vmbr2`

## Initial Interface IPs
- WAN: upstream/home router via `vmbr0` (DHCP)
- LAN1: `10.10.10.1/24`
- LAN2 / OPT1: `10.20.20.1/24`

## Current State
- pfSense VM has been successfully deployed in Proxmox
- Interfaces have been assigned and verified from the pfSense console
- WAN received an upstream address from the home router
- LAN1 and LAN2 were configured with initial gateway addresses for internal lab routing
- WebConfigurator access was validated
- DHCP services were configured for LAN1 and LAN2

## Notes
- pfSense is acting as the routing and segmentation point between all three zones
- Base deployment, interface assignment, web UI validation, and DHCP setup are complete
- Firewall rule implementation and client validation continue in later phases

## Evidence
![pfSense installation complete](../screenshots/pfsense-install-complete.png)
![pfSense interface assignment](../screenshots/pfsense-interface-assignment.png)
![pfSense console interfaces](../screenshots/pfsense-console-interfaces.png)

![pfSense webUI LAN1 dhcp pool](../screenshots/pfsense-webui-dhcp-pool-LAN1.png)
