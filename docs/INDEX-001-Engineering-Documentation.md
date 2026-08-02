# Stratus Engineering Documentation Index

**Document ID:** INDEX-001  
**Revision:** 1.1  
**Status:** Draft  
**Classification:** Public  
**Project:** Stratus  
**Author:** Austin Fellows  
**Created:** 2026-06-27  
**Last Updated:** 2026-08-02  

---

# Revision History

| Version | Date | Description | Author |
| --- | --- | --- | --- |
| 1.0 | 2026-06-27 | Initial revision | Austin Fellows |
| 1.1 | 2026-08-02 | Updated documentation index for completed architecture, standards, requirements, and traceability baseline | Austin Fellows |

---

# Table of Contents

1. Purpose
2. Documentation Hierarchy
3. Authoritative Document Set
4. System Specifications and Architecture
5. Requirements
6. Engineering Standards
7. Architecture Decision Records
8. Hardware Decision Records
9. Implementation Documentation
10. Verification and Test Documentation
11. Superseded and Transitional Documents
12. Document Status Definitions
13. Repository Conventions
14. Open Documentation Actions
15. Related Documents

---

# 1. Purpose

This document serves as the master index for engineering documentation associated with the Stratus project.

It provides a single point of entry into the engineering documentation package and identifies the authoritative relationships among:

- Project specifications
- Requirements
- System architecture
- Engineering standards
- Architecture Decision Records
- Hardware Decision Records
- Implementation artifacts
- Verification artifacts
- Test records
- Future revision documentation

This index identifies document ownership and purpose. Detailed technical content remains in the referenced authoritative documents.

---

# 2. Documentation Hierarchy

```text
Project Vision and Philosophy
            │
            ▼
         SPEC-001
            │
            ▼
         REQ-001
            │
            ├── Functional Requirements
            ├── Hardware Requirements
            ├── Software Requirements
            ├── Mechanical Requirements
            └── Electrical Requirements
            │
            ▼
         ARC-001
            │
            ├── SES Series
            ├── ADR Series
            ├── HDR Series
            └── Interface Definitions
            │
            ▼
       Implementation
            │
            ▼
          RTM-001
            │
            ▼
 Verification Procedures and Records
            │
            ▼
      Integration and Flight Test
```

---

# 3. Authoritative Document Set

The following documents form the current Stratus Rev A engineering baseline:

| Document ID | Title | Status |
| --- | --- | --- |
| SPEC-001 | Stratus Rev A System Specification | Draft |
| REQ-001 | Stratus Rev A Requirements Specification | Draft |
| ARC-001 | Stratus System Architecture | Draft |
| BOM-001 | Stratus Rev A Bill of Materials | Draft |
| SES-001 | Stratus Mechanical Engineering Standard | Draft |
| SES-002 | Stratus Electrical Engineering Standard | Draft |
| RTM-001 | Stratus Rev A Requirements Traceability Matrix | Draft |
| INDEX-001 | Stratus Engineering Documentation Index | Draft |

A document marked Draft may still be authoritative for the current development baseline unless explicitly superseded.

---

# 4. System Specifications and Architecture

| Document | Description |
| --- | --- |
| [SPEC-001](specifications/SPEC-001-Stratus-RevA.md) | Defines the Rev A system purpose, objectives, boundaries, and top-level constraints |
| [REQ-001](requirements/REQ-001.md) | Defines the requirements package, conventions, ownership, and master requirements index |
| [ARC-001](design/ARC-001-System-Architecture.md) | Defines the system, hardware, software, execution, timing, memory, interface, and fault-handling architecture |
| [ICD-001](design/ICD-001-Interface-Control-Document.md) | Stratus Rev A Interface Control Document | Defines controlled electrical, software, mechanical, coordinate, connector, and subsystem interfaces |
| [BOM-001](specifications/BOM.md) | Identifies the approved Rev A components and materials |

---

# 5. Requirements

## 5.1 Master Requirements Specification

| Document | Description |
| --- | --- |
| [REQ-001](requirements/REQ-001.md) | Defines requirement categories, writing rules, status, verification methods, traceability, and change control |

## 5.2 Functional Requirements

| Document | Subsystem | Description |
| --- | --- | --- |
| [REQ-FR-001](requirements/flight-functions/FlightControl.md) | Flight Control | Closed-loop stabilization, control behavior, limits, and controller health |
| [REQ-FR-002](requirements/flight-functions/StateEstimation.md) | State Estimation | Sensor processing, attitude estimation, calibration, timing, and estimator validity |
| [REQ-FR-003](requirements/flight-functions/MotorOutput.md) | Motor Output | Motor mixing, output constraints, arming behavior, and ESC command generation |
| [REQ-FR-004](requirements/flight-functions/Communications.md) | Communications | Debugging, diagnostics, telemetry, command reception, protocol behavior, and communication faults |

## 5.3 Engineering-Domain Requirements

| Document | Domain | Description |
| --- | --- | --- |
| [REQ-HW-001](requirements/hardware/HardwareRequirements.md) | Hardware | Flight Controller, IMU, propulsion, power, debug, expansion, reliability, and hardware safety |
| [REQ-SW-001](requirements/software/SoftwareRequirements.md) | Software | Architecture, platform, drivers, timing, memory, faults, safety, testing, and maintenance |
| [REQ-ME-001](requirements/mechanical/MechanicalRequirements.md) | Mechanical | Airframe, mounting, geometry, manufacturing, structure, serviceability, and inspection |
| [REQ-EL-001](requirements/electrical/ElectricalRequirements.md) | Electrical | Power, grounding, wiring, connectors, sensor and ESC interfaces, protection, and electrical testing |

## 5.4 Requirements Traceability

| Document | Description |
| --- | --- |
| [RTM-001](requirements/RequirementsTraceabilityMatrix.md) | Connects requirements to architecture, decisions, implementation destinations, verification methods, and planned evidence |

---

# 6. Engineering Standards

| Document | Description |
| --- | --- |
| [SES-001](standards/SES-001-Hardware.md) | Mechanical design, fastening, inserts, mounting, additive manufacturing, serviceability, CAD, and inspection standards |
| [SES-002](standards/SES-002-Wiring.md) | Power, grounding, wiring, connectors, soldering, harnessing, routing, debug, electrical safety, and inspection standards |

Engineering standards define recurring implementation practices.

They do not replace requirements or component-selection decision records.

---

# 7. Architecture Decision Records

| Document | Description |
| --- | --- |
| [ADR-001](decisions/adr/ADR-001-STM32H743-Architecture.md) | STM32H743 Architecture |
| [ADR-002](decisions/adr/ADR-002-RevA-Platform-Size.md) | Rev A Platform Size |
| [ADR-003](decisions/adr/ADR-003-Modular-Airframe-Architecture.md) | Modular Airframe Architecture |
| [ADR-004](decisions/adr/ADR-004-Custom-Flight-Software.md) | Custom Flight Software |
| [ADR-005](decisions/adr/ADR-005-Flight-Stack-Strategy.md) | Flight Stack Strategy |
| [ADR-006](decisions/adr/ADR-006-NUCLEO-F401RE-Debugger.md) | Use the NUCLEO-F401RE onboard ST-LINK/V2-1 as the Rev A external development debugger |

Architecture Decision Records explain major system-level design choices and their consequences.

Add relative Markdown links to the table once the exact filenames and directory paths are confirmed.

---

# 8. Hardware Decision Records

| Document | Description |
| --- | --- |
| [HDR-001](decisions/hdr/HDR-001-ICM20602-IMU.md) | ICM-20602 IMU |
| [HDR-002](decisions/hdr/HDR-002-HappyModel-EX1404-Motors.md) | HappyModel EX1404 Motors |
| [HDR-003](decisions/hdr/HDR-003-AeroSelfie-45A-ESC.md) | Aero Selfie 45A Four-in-One ESC |
| [HDR-004](decisions/hdr/HDR-004-Gemfan-Hurricane-3520-Propellers.md) | Gemfan Hurricane 3520 Propellers |
| [HDR-005](decisions/hdr/HDR-005-4S-850mAh-Power-System.md) | 4S 850 mAh Power System |
| [HDR-006](decisions/hdr/HDR-006-Mechanical-Hardware-Standard.md) | Mechanical Hardware Selection |
| [HDR-007](decisions/hdr/HDR-007-Wiring-Materials-Standard.md) | Wiring Materials Selection |

Hardware Decision Records explain why specific components, materials, and hardware conventions were selected.

Add relative Markdown links to the table once the exact filenames and directory paths are confirmed.

---

# 9. Implementation Documentation

The following implementation artifacts are expected to become authoritative as development progresses:

| Artifact | Purpose | Status |
| --- | --- | --- |
| Board Interface Definition | MCU pins, peripherals, connectors, signals, and electrical interfaces | Planned |
| Firmware Architecture Detail | Concrete module and directory organization | Planned |
| Software Execution Model | Exact task rates, scheduling rules, ISR behavior, and timing budgets | Partially defined in ARC-001 |
| Communication Protocol Definition | Message framing, fields, identifiers, integrity, and versioning | Planned |
| Wiring Diagram | Complete aircraft power and signal wiring | Planned |
| Harness Definitions | Wire gauge, colors, lengths, connectors, and pin assignments | Planned |
| CAD Assembly Documentation | Part relationships, datums, mounting interfaces, and revision ownership | Planned |
| Assembly Procedure | Controlled aircraft assembly sequence | Planned |
| Bring-Up Procedure | Ordered electrical and firmware integration process | Planned |
| Configuration Record | Tested hardware, firmware, and mechanical configuration | Planned |

Implementation artifacts shall link back to the applicable requirements and architecture.

---

# 10. Verification and Test Documentation

| Artifact | Purpose | Status |
| --- | --- | --- |
| RTM-001 | Requirements allocation and verification planning | Draft |
| Verification and Validation Plan | Defines the overall verification strategy | Planned |
| Flight Controller Programming and Debug Test | Verifies SWD, DFU, reset, and debugger behavior | Planned |
| IMU SPI Bring-Up Test | Verifies identity, configuration, and sensor data | Planned |
| ESC and Motor Mapping Test | Verifies output channels and motor direction without propellers | Planned |
| Electrical Pre-Power Inspection | Verifies polarity, continuity, shorts, and workmanship | Planned |
| Power-Rail and Transient Test | Verifies voltage regulation and propulsion-induced disturbances | Planned |
| Mechanical Fit and Clearance Inspection | Verifies mounting, access, and propeller clearance | Planned |
| Scheduler Timing Test | Verifies periodic execution and timing margins | Planned |
| Safe-State and Arming Test | Verifies non-commanding startup and fault behavior | Planned |
| Communications Parser Test | Verifies framing, validation, recovery, and integrity handling | Planned |
| Integration Test Reports | Records subsystem integration results | Planned |
| Flight Test Procedures | Defines controlled flight-test steps and acceptance criteria | Planned |
| Flight Test Reports | Records test configuration, results, and anomalies | Planned |
| Build Logs | Records manufacturing and assembly configuration | Planned |
| Flight Logs | Records aircraft telemetry and flight behavior | Planned |

---

# 11. Superseded and Transitional Documents

## 11.1 Transitional-Document Rule

A superseded document retained for link compatibility shall clearly state:

- That it is superseded
- Which documents replace it
- That new requirements shall not be added to it
- The date of supersession

---

# 12. Document Status Definitions

| Status | Meaning |
| --- | --- |
| Draft | Under development and not formally baselined |
| Active | Applicable to the current project revision |
| Planned | Intended but not yet authored or completed |
| Deferred | Intentionally postponed |
| Superseded | Replaced by another authoritative artifact |
| Deprecated | Retained for historical reference but no longer used |
| Approved | Reviewed and accepted for the stated baseline |
| Verified | Demonstrated to satisfy the applicable requirements |

---

# 13. Repository Conventions

## 13.1 Authoritative Source

Each document ID shall map to one authoritative file.

Duplicate authoritative documents shall not use the same document ID.

## 13.2 Relative Links

Markdown documents shall use relative repository links.

Links shall target the authoritative file rather than duplicate or exported copies.

## 13.3 Filenames

Readable filenames may be used when the formal document ID is present in the document metadata.

Examples:

```text
FlightControl.md          → REQ-FR-001
StateEstimation.md        → REQ-FR-002
MotorOutput.md            → REQ-FR-003
Communications.md         → REQ-FR-004
HardwareRequirements.md   → REQ-HW-001
```

## 13.4 Revision Control

Material document changes shall update:

- Revision
- Last Updated
- Revision History

## 13.5 Empty Files

Empty scaffold files shall be:

- Populated
- Removed
- Marked as intentionally reserved
- Converted into explicit redirect pages

Unexplained empty authoritative documents are not permitted in the completed baseline.

---

# 14. Open Documentation Actions

| Action ID | Action | Priority | Status |
| --- | --- | --- | --- |
| DOC-ACT-001 | Confirm exact repository paths for SPEC-001, ARC-001, BOM-001, SES files, ADRs, and HDRs | High | Open |
| DOC-ACT-002 | Add working links for all ADR and HDR records | High | Open |
| DOC-ACT-003 | Run a repository-wide Markdown link check | High | Open |
| DOC-ACT-004 | Convert or remove FunctionalRequirements.md | High | Open |
| DOC-ACT-005 | Convert or remove NonFunctionalRequirements.md | High | Open |
| DOC-ACT-006 | Audit Interfaces.md and determine whether it is authoritative, transitional, or empty | High | Open |
| DOC-ACT-007 | Audit remaining empty scaffold files | High | Open |
| DOC-ACT-008 | Verify all document IDs are unique | High | Open |
| DOC-ACT-009 | Expand RTM-001 with individual FC, SE, and MO requirement rows | Medium | Open |
| DOC-ACT-010 | Create initial bring-up and verification procedures | Medium | Open |

---

# 15. Related Documents

## Upstream

- README.md
- SPEC-001

## Peer

- REQ-001
- ARC-001
- BOM-001
- RTM-001
- SES-001
- SES-002

## Supporting

- REQ-FR Series
- REQ-HW Series
- REQ-SW Series
- REQ-ME Series
- REQ-EL Series
- ADR Series
- HDR Series

## Downstream

- Implementation documentation
- Verification procedures
- Test records
- Integration reports
- Flight-test documentation