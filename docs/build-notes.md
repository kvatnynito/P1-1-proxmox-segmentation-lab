# Build Notes

## Milestone 1 - pfSense deployment completed
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
- WebConfigurator access needed to be verified from the correct internal network path.
- DHCP configuration should be done only after confirming the intended subnet and gateway design.

## Milestone 2 - pfSense validation completed
- Confirmed pfSense WebConfigurator access from the internal network
- Validated WAN, LAN1, and LAN2 interface behavior
- Configured DHCP scopes for LAN1 and LAN2
- Confirmed pfSense is ready to support internal VM deployment

## Lessons Learned
- Interface assignment and console verification are useful before relying on web UI configuration.
- DHCP configuration should align with the documented IP plan to keep later VM deployment consistent.

## Milestone 3 - AD-DC01 deployment and connectivity validation completed
- Created `AD-DC01` in Proxmox and connected it to `vmbr1`
- Installed Windows Server 2022
- Loaded VirtIO storage and network drivers during setup
- Configured static IP settings:
  - IP -> `10.10.10.10`
  - Gateway -> `10.10.10.1`
  - DNS -> `10.10.10.1`
- Validated connectivity to pfSense at `10.10.10.1`
- Validated outbound connectivity by IP and DNS
- Corrected the DNS server entry from `10.10.10.0` to `10.10.10.1`

## Lessons Learned
- Windows Server installation in Proxmox may require both VirtIO storage and NIC drivers before the system is fully usable.
- A simple DNS typo can break name resolution even when routing and gateway connectivity are working correctly.
- Static addressing for core infrastructure systems keeps later lab stages more predictable.

## Milestone 4 - LAN2 attack lab base completed
- Created `ATTACK-KALI01` and connected it to `vmbr2`
- Created `VULN-METASPLOITABLE2` and connected it to `vmbr2`
- Verified both systems received LAN2 network addressing
- Validated communication between Kali and Metasploitable on the isolated vulnerable segment
- Confirmed LAN2 behavior is intentionally segmented and deny-by-default outside approved paths

## Lessons Learned
- Older vulnerable systems may require different compatibility choices than modern VMs, including import workflow, boot mode, or NIC model adjustments.
- Communication testing inside LAN2 is useful for proving the attack lab base works before introducing scans or exploitation activity.
- Deny-by-default behavior on the vulnerable segment is a design feature, not a problem to work around.

## Milestone 5 - Splunk deployment completed
- Created `SIEM-SPLUNK01` in Proxmox and connected it to `vmbr1`
- Installed Ubuntu Server
- Configured static IP settings:
  - IP -> `10.10.10.20`
  - Gateway -> `10.10.10.1`
  - DNS -> `10.10.10.1`
- Verified connectivity to pfSense, outbound IP reachability, and DNS resolution
- Downloaded the official Splunk Enterprise 10.2.3 Linux `.deb` package directly from `SIEM-SPLUNK01` using `wget`
- Installed Splunk Enterprise on Ubuntu using `dpkg`
- Confirmed Splunk 10.2 rejected default root startup
- Confirmed the `splunk` service user existed
- Changed `/opt/splunk` ownership to `splunk:splunk`
- Started Splunk as the `splunk` service user
- Enabled Splunk to start at boot using a `systemd` service running as `splunk:splunk`
- Confirmed Splunk Web UI access from TEST-WIN10-LAN1 at `http://10.10.10.20:8000`

## Lessons Learned
- Setting a static IP before installing Splunk keeps management and later forwarding targets consistent.
- Splunk is much easier to work with when installed on a lightweight dedicated Linux server rather than overcomplicating the operating system layer.
- Confirming the web UI from a LAN1 client is the clearest proof that the SIEM host is operational and reachable.
- Host-to-VM file transfer with WinSCP/SFTP was not the cleanest install path because the Windows host was outside the lab LAN1 path and pfSense segmentation blocked unsolicited access into LAN1.
- SSH on SIEM-SPLUNK01 was installed but initially stopped; starting `ssh.service` confirmed the service worked locally, but routing and firewall placement still mattered.
- Direct `wget` from SIEM-SPLUNK01 was the better approach because the VM already had validated outbound internet access and DNS resolution.
- Splunk 10.2 should run as the dedicated `splunk` service user instead of root, so ownership and boot-start configuration need to match that service account.
