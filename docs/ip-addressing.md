# IP Addressing

## Portfolio Addressing Note
This repository uses representative private IP addressing for portfolio documentation. Public/WAN-facing details are intentionally omitted.

---

## Internal Network Addressing Plan

| Segment | Purpose | Subnet | Default Gateway | Notes |
|---|---|---:|---:|---|
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

## Planned DHCP Ranges

### LAN1 DHCP Scope
- Proposed range: `10.10.10.100` - `10.10.10.199`
- Intended use: Windows endpoints and other DHCP-based client systems

### LAN2 DHCP Scope
- Proposed range: `10.20.20.100` - `10.20.20.199`
- Intended use: Vulnerable lab systems and test devices where static addressing is not required

---

## Planned Static / Reserved Address Space

Lower addresses are reserved for infrastructure, servers, and manually assigned systems as the lab build progresses.

### LAN1 Reserved Range
- `10.10.10.2` - `10.10.10.99`

Examples of future systems:
- `AD-DC01`
- `AD-FS01`
- `SIEM-SPLUNK01`
- additional monitoring or management systems

### LAN2 Reserved Range
- `10.20.20.2` - `10.20.20.99`

Examples of future systems:
- `VULN-WIN2019`
- `VULN-OPENVAS`
- additional vulnerable or scanning systems

---

## Current Week 2 Relevance

This addressing plan supports the current Week 2 build goals by defining:

- the subnet for `LAN1`
- the subnet for `LAN2`
- pfSense gateway IPs for each segment
- the DHCP ranges planned for initial endpoint deployment

The first expected internal client validation is a Windows endpoint on `LAN1` receiving DHCP from pfSense.

---

## Notes

- This addressing scheme is intentionally simple and readable for portfolio presentation.
- `10.10.10.0/24` and `10.20.20.0/24` are used to clearly separate enterprise and vulnerable segments.
- WAN/home network addressing is not documented here.
- Address assignments may be refined as additional lab systems are deployed.
