## Proxmox Network Bridges

To support network segmentation, this lab uses multiple Proxmox bridges to simulate separate network zones.

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

These bridges allow pfSense to act as the central routing and security enforcement point between networks, enabling:

- Network segmentation
- Controlled communication between zones
- Realistic enterprise security scenarios
