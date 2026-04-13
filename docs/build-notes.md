# Build Notes

## 2026-04-06 - pfSense deployment completed
- Created pfSense VM in Proxmox
- Attached 3 NICs:
  - WAN -> vmbr0
  - LAN1 -> vmbr1
  - LAN2 -> vmbr2
- Completed initial interface assignment
- Set LAN1 to 10.10.10.1/24
- Set LAN2 to 10.20.20.1/24

## Observations
- pfSense interface naming inside the VM required careful verification against the NIC order in Proxmox.
- Because this is a VM install, the ISO must be detached after installation to avoid booting back into the installer.

## Issues / Lessons Learned
- Need to verify WebConfigurator access from the correct network path.
- DHCP configuration should be done only after confirming the intended subnet/gateway design.

## 2026-04-13 - Week 2 pfSense validation completed
- Confirmed pfSense WebConfigurator access from the internal network
- Validated WAN, LAN1, and LAN2 interface behavior
- Configured DHCP scopes for LAN1 and LAN2
- Confirmed pfSense is ready to support internal VM deployment

## Lessons Learned
- Interface assignment and console verification are useful before relying on web UI configuration
- DHCP configuration should align with the documented IP plan to keep later VM deployment consistent
