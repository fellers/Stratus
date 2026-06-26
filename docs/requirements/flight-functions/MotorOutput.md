

# Motor Output Requirements

**Document ID:** REQ-FR-003

**Parent Document:** REQ-001

**Requirement Category:** Functional Requirements

**Subsystem:** Motor Output

---

# Purpose

This document defines the functional requirements for the Motor Output capability within Stratus Rev A.

The Motor Output function is responsible for translating flight control outputs into motor commands that can be delivered to the Propulsion subsystem.

---

# Requirements

| ID | Requirement |
| --- | --- |
| FR-MO-001 | The system shall generate individual motor commands for each propulsion motor. |
| FR-MO-002 | The system shall convert Flight Control outputs into motor-specific commands using a defined motor mixing strategy. |
| FR-MO-003 | The system shall constrain motor commands within the allowable command range of the Propulsion subsystem. |
| FR-MO-004 | The system shall provide a minimum motor command state suitable for initialization, arming, and safe idle operation. |
| FR-MO-005 | The system shall provide a zero-thrust motor command state suitable for disarmed and fault conditions. |
| FR-MO-006 | The system shall update motor commands at a rate sufficient to support closed-loop flight stabilization. |
| FR-MO-007 | The system shall prevent motor command output before the system has completed required initialization checks. |
| FR-MO-008 | The system shall transition motor commands to a predefined safe state when a critical flight-control fault is detected. |
| FR-MO-009 | The system shall support future migration from simple motor command protocols to higher-performance digital motor command protocols without fundamental redesign of the Flight Control software. |

---

# Notes

Motor Output requirements define system behavior and do not prescribe the specific motor command protocol used by the implementation.

Protocol-level details, timing, signal generation, and electrical interfaces shall be documented in the applicable architecture and engineering standards documents.

---

# Related Documents

## Upstream

- REQ-001
- SPEC-001

## Peer

- REQ-FR-001
- REQ-FR-002

## Supporting

- ARC-001
- SES-002
- HDR-002
- HDR-003
- HDR-004