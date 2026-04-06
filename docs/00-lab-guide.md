# Lab Build Guide (Start Here)

This guide provides the recommended build order for the Proxmox Segmentation Lab. It is intended to keep implementation, validation, and documentation aligned as the lab progresses.

---

## Current Build Stage

**Current focus:** Week 2 — pfSense validation, LAN configuration, and DHCP preparation for the first internal endpoint.

At this stage, the Proxmox bridge layout and pfSense deployment are already in place. The next goal is to validate network behavior and prepare `LAN1` for the first Windows client system.

---

## Recommended Build Order

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
Defines the representative addressing plan for internal lab segments, including gateways, DHCP scope planning, and reserved ranges.

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

For each phase:

1. implement the change in Proxmox or pfSense  
2. validate the result  
3. capture screenshots or evidence  
4. update the related documentation  

This keeps the repository accurate as the lab evolves.
