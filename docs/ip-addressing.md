# IP Addressing

## Portfolio Addressing Note
This repository uses representative private IP addressing for portfolio documentation. Public/WAN-facing details are intentionally omitted.

---

## Internal Network Addressing Plan

| Segment | Purpose | Subnet | Default Gateway | Notes |

| LAN1 | Enterprise / Blue Team | `10.10.10.0/24` | `10.10.10.1` | Internal enterprise-style systems |

| LAN2 | Vulnerable / Testing | `10.20.20.0/24` | `10.20.20.1` | Vulnerable systems and testing targets |

---

## Gateway Assignments

### LAN1
- Network: `10.10.10.0/24`
- Gateway: `10.10.10.1`
- Gateway device: `FW-EDGE01` (pfSense)

### LAN2
- Network: `10.20.20.0/24`
- Gateway: `10.20.20.1`
- Gateway device: `FW-EDGE01` (pfSense)

---

## DHCP Ranges

### LAN1 DHCP Scope
- Range: `10.10.10.100` - `10.10.10.199`
- Intended use: Windows endpoints and other DHCP-based client systems

### LAN2 DHCP Scope
- Range: `10.20.20.100` - `10.20.20.199`
- Intended use: Vulnerable lab systems and test devices where static addressing is not required

---

## Static / Reserved Address Space

Lower addresses are reserved for infrastructure, servers, and manually assigned systems.

### LAN1 Reserved Range
- `10.10.10.2` - `10.10.10.99`

### LAN2 Reserved Range
- `10.20.20.2` - `10.20.20.99`

---

## Current Assigned Systems

### LAN1
- `FW-EDGE01` interface: `10.10.10.1`
- `AD-DC01`: `10.10.10.10`
- `SIEM-SPLUNK01`: `10.10.10.20`
- `AD-WIN10`: DHCP client from LAN1 scope

### LAN2
- `FW-EDGE01` interface: `10.20.20.1`
- `TEST-WIN10-LAN2`: DHCP client from LAN2 scope
- `ATTACK-KALI01`: LAN2 connected
- `VULN-METASPLOITABLE2`: LAN2 connected

---

## Milestone Relevance

This addressing plan supports early repository milestones by defining:

- the subnet for `LAN1`
- the subnet for `LAN2`
- pfSense gateway IPs for each segment
- the DHCP ranges for endpoint validation
- the reserved address space for infrastructure systems

It now reflects current static assignments for deployed infrastructure and server systems.

---

## Notes

- This addressing scheme is intentionally simple and readable for portfolio presentation.
- `10.10.10.0/24` and `10.20.20.0/24` are used to clearly separate enterprise and vulnerable segments.
- WAN/home network addressing is not documented here.
- Some client systems use DHCP during validation, while core infrastructure systems use static addressing.
- Address assignments may be refined as additional lab systems are deployed.
