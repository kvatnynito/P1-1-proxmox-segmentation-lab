# Proxmox Network Bridges

This lab uses multiple Proxmox network bridges to enforce segmentation between lab zones. These bridges function as virtual switches and provide the network foundation for the environment.

---

## Implementation Status

Completed in Proxmox:

- `vmbr0` created for WAN/uplink
- `vmbr1` created for LAN1 Enterprise
- `vmbr2` created for LAN2 Vulnerable
- `FW-EDGE01` connected to all three bridges using three virtual NICs

---

## Bridge Layout

### `vmbr0` (WAN / Uplink)
- Connected to the home/upstream router
- Provides upstream network access
- Used by the pfSense WAN interface
- Receives IP addressing from the upstream DHCP environment

### `vmbr1` (LAN1 — Enterprise)
- Subnet: `10.10.10.0/24`
- Gateway: `10.10.10.1` (pfSense)
- Intended systems:
  - Domain Controller
  - Windows endpoints
  - SIEM / monitoring systems such as Splunk
- Represents the primary internal enterprise-style network segment

### `vmbr2` (LAN2 — Vulnerable)
- Subnet: `10.20.20.0/24`
- Gateway: `10.20.20.1` (pfSense)
- Intended systems:
  - Vulnerable systems
  - Attack simulation targets
  - Vulnerability scanning tools
- Represents a separate testing and vulnerable segment

---

## Relationship to pfSense

`FW-EDGE01` uses three virtual NICs to connect to these bridges:

- WAN → `vmbr0`
- LAN1 → `vmbr1`
- LAN2 → `vmbr2`

This makes pfSense the central routing and policy enforcement point between the lab zones.

---

## Design Purpose

This bridge design supports:

- network segmentation
- centralized routing through pfSense
- controlled communication between zones
- realistic enterprise-style lab scenarios
- future firewall policy testing between trusted and untrusted segments

---

## Week 2 Relevance

For Week 2, these bridges provide the required network foundation for:

- validating pfSense interface assignments
- enabling DHCP-backed internal connectivity
- placing the first Windows endpoint on `vmbr1`
- preparing for later segmentation and firewall-rule testing
