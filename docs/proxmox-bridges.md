## Proxmox Network Bridges

To support network segmentation, multiple Proxmox bridges are used:

- vmbr0 (WAN)
  - Connected to home router
  - Used by pfSense WAN interface

- vmbr1 (LAN1 - Enterprise)
  - 10.10.10.0/24
  - Used for domain, endpoints, and SIEM

- vmbr2 (LAN2 - Vulnerable)
  - 10.20.20.0/24
  - Used for vulnerable systems and testing

These bridges allow pfSense to route and enforce segmentation between zones.
