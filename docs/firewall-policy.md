# Firewall Policy

## Status
Planned for the lab build.

This document explains how traffic is intended to move between the different parts of the lab once firewall rules are fully configured in pfSense.

---

## Purpose

The goal of this firewall policy is to keep the lab organized and realistic.

In a real environment, not every system should be able to talk to every other system freely. Some systems are more trusted, and some are intentionally less trusted. This lab follows that same idea.

pfSense is the system that sits in the middle and controls what is allowed and what is blocked.

---

## Network Zones

### WAN
This is the outside connection. It represents the home/upstream network that gives the lab internet access.

### LAN1
This is the main internal network. It is meant to represent the safer, more trusted side of the environment.

This is where systems like the following are expected to live:
- Domain Controller
- user workstations
- monitoring tools
- file server

### LAN2
This is the testing and vulnerable side of the lab.

This network is meant for systems that are intentionally less secure, such as:
- vulnerable machines
- testing targets
- scanning tools

Because of that, this side should not be trusted the same way as LAN1.

---

## Security Stance

The main idea is simple:

- trusted systems should be protected
- vulnerable systems should be contained
- communication between networks should only happen when there is a reason for it

In other words, the lab should not allow open communication everywhere by default.

---

## Intended Rule Model

### LAN1 → WAN
**Policy:** Allow  
**Purpose:** Enable package updates, downloads, and required outbound connectivity for enterprise-side systems.

### LAN2 → WAN
**Policy:** Restricted allow or deny, depending on scenario  
**Purpose:** Support controlled testing while limiting unnecessary outbound access from vulnerable systems.

### LAN2 → LAN1
**Policy:** Deny by default  
**Purpose:** Reduce lateral movement risk from vulnerable systems into the enterprise segment.

### LAN1 → LAN2
**Policy:** Limited allow as needed  
**Purpose:** Permit only scenario-driven access such as:
- administration
- validation testing
- vulnerability scanning
- controlled analyst access

---

## Intended Traffic Behavior

### LAN1 to WAN
Devices on the enterprise side should be allowed to reach outward when needed.

This would support things like:
- updates
- downloads
- package installs
- normal internet access for lab setup

### LAN2 to WAN
Devices on the vulnerable side should have more limited outbound access.

Depending on the lab scenario, this may be allowed in a restricted way or blocked when not needed.

### LAN2 to LAN1
This should be blocked by default.

The vulnerable side should not be able to freely access the enterprise side. This helps simulate basic containment and reduces the chance of easy movement from less trusted systems into more important ones.

### LAN1 to LAN2
This may be allowed only when needed for lab work.

Examples might include:
- administration
- testing
- scanning
- troubleshooting

The idea is that access should be intentional, not automatic.

---

## Why is this implemented

This policy helps the lab feel more like a real environment.

Instead of putting all systems on one flat network, it creates separation between:
- normal internal systems
- monitoring systems
- vulnerable targets

That makes it easier to practice:
- segmentation concepts
- access control
- safe testing
- future detection and investigation workflows

---

## Week 2 Relevance

For Week 2, this policy is still the intended design rather than a fully tested final state.

Right now, the focus is on:
- confirming pfSense is connected to the correct networks
- validating the internal network setup
- preparing for DHCP and endpoint testing

Firewall rule testing will come after the base network setup is working.

---

## Future Updates

Later, this document can be expanded to include:
- actual firewall rules created in pfSense
- screenshots of those rules
- examples of what was allowed
- examples of what was blocked
- notes from testing between LAN1 and LAN2
