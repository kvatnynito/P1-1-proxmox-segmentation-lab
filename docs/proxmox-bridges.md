## Proxmox Network Bridges

This lab uses multiple Proxmox bridges to enforce segmentation between lab zones. The bridge layout below is the configuration currently implemented in the environment.

## Implementation Status
Completed in Proxmox:
- vmbr0 created for WAN/uplink
- vmbr1 created for Enterprise LAN
- vmbr2 created for Vulnerable LAN
- pfSense connected to all three bridges using three virtual NICs

### vmbr0 (WAN)
- Connected to home router
- Provides internet access
- Used exclusively by pfSense WAN interface
- Receives IP via DHCP from ISP router

### vmbr1 (LAN1 - Enterprise)
- Subnet: 10.10.10.0/24
- Gateway: 10.10.10.1 (pfSense)
- Used for:
  - Domain Controller
  - Endpoints
  - SIEM (Splunk)
- Represents a production-like network

### vmbr2 (LAN2 - Vulnerable)
- Subnet: 10.20.20.0/24
- Gateway: 10.20.20.1 (pfSense)
- Used for:
  - Vulnerable systems
  - Attack simulations
  - Vulnerability scanning
- Isolated from LAN1 by default

### Design Purpose

These virtual bridges (aka virtual switches) allow pfSense to act as the central routing and security enforcement point between networks, enabling:

- Network segmentation
- Controlled communication between zones
- Realistic enterprise security scenarios

where pfSense is using 3 NICs to interface these bridges together.
