# Architecture

## Overview

This lab is designed as a small segmented environment built in Proxmox.

The main idea is to avoid placing every system on one flat network. Instead, the environment is separated into different zones so that systems can be grouped by purpose and trust level. This makes the lab more realistic and supports safer testing, better organization, and clearer future monitoring workflows.

At the center of the design is `FW-EDGE01` (pfSense), which acts as the main routing and control point between the lab networks.

---

## Core Design

The lab is built around three main network connections:

- `vmbr0` — WAN / upstream connection
- `vmbr1` — LAN1 Enterprise
- `vmbr2` — LAN2 Vulnerable

pfSense connects to all three of these bridges using three virtual NICs.

This allows pfSense to:

- provide upstream access
- route traffic between internal networks
- enforce separation between zones
- support future firewall-rule testing

---

## Network Zones

### WAN
This is the outside-facing side of the lab.

It connects pfSense to the home or upstream network and provides internet access when needed for setup, updates, and package installation.

### LAN1
This is the enterprise side of the lab.

It is intended for systems that represent a more normal internal business environment, such as:

- domain services
- user workstations
- monitoring systems
- file services

This side is treated as the more trusted internal segment.

### LAN2
This is the vulnerable and testing side of the lab.

It is intended for systems that are purposely less secure or are used for testing, such as:

- vulnerable targets
- scanning tools
- systems used for attack simulation

This side is treated as a lower-trust segment and is meant to stay separate from LAN1 unless access is intentionally allowed.

---

## Routing and Control

pfSense is the central point that ties the lab together.

Rather than allowing systems to move freely between segments, pfSense is intended to control how traffic moves between the networks. This supports the overall goal of segmentation and makes it possible to test both allowed and blocked traffic patterns later in the build.

---

## Why This Design Was Chosen

This architecture was chosen to support several goals:

- build a more realistic homelab
- practice segmentation instead of using one flat network
- separate trusted and vulnerable systems
- prepare for future logging, monitoring, and investigation workflows
- create a reusable foundation for the next portfolio projects

In other words, this repo is not just about standing up VMs. It is about building the network structure that the rest of the lab depends on.

---

## Current Stage

At the current stage of the build:

- Proxmox bridges have been created
- pfSense has been deployed
- WAN, LAN1, and LAN2 have been assigned
- internal addressing has been planned
- DHCP and first endpoint validation are the next major steps

This means the architecture foundation is in place, even though the full lab is still being built out.

---

## Related Documents

For more detail, see:

- `proxmox-bridges.md`
- `pfsense-config.md`
- `ip-addressing.md`
- `vm-inventory.md`
- `firewall-policy.md`
