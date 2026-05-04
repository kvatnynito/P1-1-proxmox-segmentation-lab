# Lab Build Guide (Start Here)

This guide provides the recommended build order for the Proxmox Segmentation Lab. It is intended to keep implementation, validation, and documentation aligned as the lab progresses.

---

## Current Build Stage

**Current focus:** Milestone 5 complete — pfSense is operational, internal enterprise and vulnerable segment systems have been deployed, and Splunk is running on LAN1.

At this stage, the Proxmox bridge layout, pfSense deployment, internal endpoint validation, enterprise server deployment, LAN2 attack lab base, and Splunk deployment are all in place. The next goal is to begin log forwarding and ingestion validation for the next repository milestone.

---

## Build Order

## Phase 1 — Infrastructure Setup

### 1. Proxmox Bridges
Defines the virtual network foundation for the lab.

Document:
- `proxmox-bridges.md`

### 2. pfSense Deployment
Documents the deployment of `FW-EDGE01`, interface assignments, and initial routing role in the environment.

Document:
- `pfsense-config.md`

---

## Phase 2 — Network Configuration

### 3. IP Addressing
Defines the representative addressing plan for internal lab segments, including gateways, DHCP scope planning, reserved ranges, and current assigned systems.

Document:
- `ip-addressing.md`

### 4. Firewall Policy
Documents the intended segmentation and inter-zone access model enforced through pfSense.

Document:
- `firewall-policy.md`

---

## Phase 3 — Systems Deployment

### 5. VM Inventory
Tracks the planned and deployed systems for each lab segment, including current status and intended network placement.

Document:
- `vm-inventory.md`

---

## Phase 4 — Build Notes / Observations

### 6. Build Notes
Captures implementation notes, lessons learned, issues encountered, and validation observations during the lab build.

Document:
- `build-notes.md`

---

## Architecture Reference

Reference materials:
- `architecture.md`
- `diagrams/repo1-network-diagram.png`

---

## Purpose

This build order helps ensure:

- the network foundation is built first
- segmentation is documented before later systems are introduced
- VM placement matches the intended zone design
- implementation steps are reproducible
- documentation stays aligned with actual lab progress

---

## Suggested Workflow

For each milestone:

1. implement the change in Proxmox or pfSense  
2. validate the result  
3. capture screenshots or evidence  
4. update the related documentation  

This is to ensure the repository stays accurate as the lab progresses.
