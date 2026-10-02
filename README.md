# Katlego Adult Learning Centre — Network Design Project

**Course:** CMPG 325 — Computer Networks (Individual Project)
**Student Number:** 46967494
**Project ID:** CMPG325-2026-025
**Client ID:** CLI-025

## Project Overview
This repository documents the design, implementation, and testing of a
computer network for Katlego Adult Learning Centre (Rustenburg), a
community-based adult education institution in the North West Province.

The project covers the full lifecycle from client requirements analysis
through network design, IP addressing, Packet Tracer implementation,
configuration of the assigned technical challenge (Port Security), and
final testing and reflection.

## Assigned Parameters
- **Addressing block:** 192.168.22.0/24
- **Assigned technical challenge:** Port Security (switchport access control)
- **Design constraint:** Server room access restricted to authorised IT staff only
- **Change request (CR11):** Accommodate VoIP handsets on the existing design

## Repository Structure
| Folder | Contents |
|---|---|
| `01-client-requirements` | Client background, scope, and functional requirements |
| `02-network-design` | Physical and logical topology diagrams |
| `03-ip-addressing` | VLSM-based IP addressing plan |
| `04-packet-tracer` | Final .pkt implementation file |
| `05-configuration` | Device configuration evidence |
| `06-testing` | Connectivity and functionality test results |
| `07-troubleshooting` | Issues encountered and how they were resolved |
| `08-reflection` | Final project reflection |

## Project Timeline
- Project start: 14 August 2026
- Milestone 1 (Client Design Review): 28 August 2026
- Milestone 2 (Client Implementation Review): 2 October 2026
- Final submission: 16 October 2026

## Academic Integrity
This is an individual project completed in accordance with the CMPG 325
project brief and the NWU AI Policy.

#CONTINUE TO MILESTONE 2

A hierarchical campus network designed in Milestone 1 and implemented and tested in Cisco Packet Tracer in Milestone 2. The assigned feature is **Port Security**.

## Contents

| Item | Description |
|---|---|
| `46967494_MILESTONE_2.pkt` | Packet Tracer simulation (full network, configured) |
| `Milestone2_Report.pdf` | Milestone 2 documentation with testing evidence |
| `evidence/` | Numbered testing screenshots (referenced in the report) |

## Design summary

- Router-on-a-stick inter-VLAN routing (Cisco 1941, `Gi0/0` with five sub-interfaces)
- Core switch plus three access switches grouped by function (Classrooms/Library, Computer Lab, Admin/Reception)
- Five VLANs with VLSM addressing in `192.168.22.0/24`

| VLAN | Segment | Network | Gateway |
|---|---|---|---|
| 10 | Classrooms and Library | 192.168.22.32/28 | 192.168.22.33 |
| 20 | Computer Lab | 192.168.22.0/27 | 192.168.22.1 |
| 30 | Admin | 192.168.22.48/28 | 192.168.22.49 |
| 40 | Voice | 192.168.22.64/29 | 192.168.22.65 |
| 99 | Management and server room | 192.168.22.72/29 | 192.168.22.73 |

## Milestone 2 features

- **DHCP** for VLANs 10, 20, 30 and 40 (static printer at 192.168.22.50, static management addressing in VLAN 99)
- **Voice VLAN** on the Reception phone port (`switchport voice vlan 40`, DHCP option 150)
- **Port Security** (assigned feature) on every access port: sticky MAC, maximum 1 (2 on the phone port), violation action `shutdown`
- **Restricted access ACL**: VLANs 10, 20 and 40 are denied access to the server room segment 192.168.22.72/29; Admin (VLAN 30) is the deliberate exception

## Testing evidence

| Test | Evidence |
|---|---|
| Same-VLAN connectivity | `evidence_01` |
| Inter-VLAN routing | `evidence_02` |
| Restricted access blocked (Classroom, Lab) and ACL hit counts | `evidence_03`, `evidence_03b`, `evidence_03c` |
| Admin exception | `evidence_04` |
| Port Security: before, violation, err-disabled, recovery | `evidence_05a` to `evidence_05d` |
| Configuration verification | `evidence_06` to `evidence_08` |
| DHCP leases | `evidence_09`, `evidence_13` |
| Port Security status per switch | `evidence_10` to `evidence_12` |
| VoIP phone reachable | `evidence_14` |

## Deviations from the plan

- SW3 is a Catalyst 3560-24PS (PoE) instead of a 2960-24PC.
- The phone is on SW3 `Fa0/6` and the Reception PC on `Fa0/5`.
- SW3 uplinks to core `Fa0/4`.

See the report for the problems found and how each was fixed.
