# Stratus Mechanical Requirements

**Document ID:** REQ-ME-001  
**Revision:** 1.0  
**Status:** Draft  
**Classification:** Public  
**Project:** Stratus  
**Author:** Austin Fellows  
**Created:** 2026-08-02  
**Last Updated:** 2026-08-02  

---

# Revision History

| Version | Date | Description | Author |
| --- | --- | --- | --- |
| 1.0 | 2026-08-02 | Initial mechanical requirements | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Airframe Requirements
4. Modularity Requirements
5. Component-Mounting Requirements
6. Propulsion-Geometry Requirements
7. Battery-Mounting Requirements
8. Sensor-Mounting Requirements
9. Wiring-Accommodation Requirements
10. Additive-Manufacturing Requirements
11. Structural Requirements
12. Serviceability Requirements
13. Expansion Requirements
14. Inspection and Verification Requirements
15. Requirement Summary
16. References
17. Related Documents

---

# 1. Purpose

This document defines the mechanical requirements for Stratus Rev A.

These requirements govern the airframe, mounting interfaces, structural layout, additive-manufactured parts, serviceability, component protection, and physical integration of the aircraft.

---

# 2. Scope

This document applies to:

- Airframe
- Center structure
- Arms
- Motor mounts
- Electronics mounts
- IMU mount
- ESC mount
- Battery mount
- Protective structures
- Landing features
- Cable-routing features
- Fasteners
- Inserts
- Standoffs
- Printed components

Detailed mechanical engineering practices are defined in **SES-001**.

---

# 3. Airframe Requirements

## REQ-ME-001 — Rev A Platform Size

Stratus Rev A shall use a nominal 3.5-inch propeller-class airframe architecture.

**Verification:**  
Design and hardware inspection.

---

## REQ-ME-002 — Quadrotor Geometry

The airframe shall support four motors arranged in a quadrotor configuration.

**Verification:**  
CAD and assembly inspection.

---

## REQ-ME-003 — Aircraft Coordinate System

The mechanical design shall use the project aircraft coordinate convention:

- Positive X forward
- Positive Y right
- Positive Z downward

**Verification:**  
CAD and documentation inspection.

---

## REQ-ME-004 — Defined Center Datum

The airframe shall define a repeatable central datum for mechanical and sensor references.

**Verification:**  
CAD inspection.

---

## REQ-ME-005 — Component Envelope

The airframe shall provide sufficient space for all Rev A components without interference.

**Verification:**  
CAD interference analysis and assembly test.

---

## REQ-ME-006 — Flight-Ready Retention

All flight hardware shall be mechanically retained so it cannot move freely during normal operation.

**Verification:**  
Inspection and vibration test.

---

# 4. Modularity Requirements

## REQ-ME-007 — Modular Architecture

The airframe shall use replaceable mechanical modules where practical.

**Verification:**  
Architecture inspection.

---

## REQ-ME-008 — Replaceable Arms

Individual arms should be replaceable without replacing the complete airframe.

**Verification:**  
Serviceability demonstration.

---

## REQ-ME-009 — Replaceable Motor Mounts

Motor-mount damage should not require replacement of unrelated electronics mounts where practical.

**Verification:**  
Design review.

---

## REQ-ME-010 — Replaceable Electronics

The Flight Controller, IMU, and ESC should be removable independently from the primary structural frame where practical.

**Verification:**  
Disassembly demonstration.

---

## REQ-ME-011 — Non-Destructive Service

Routine component replacement shall not require cutting or permanently damaging structural parts.

**Verification:**  
Maintenance demonstration.

---

## REQ-ME-012 — Standardized Interfaces

Repeated mechanical interfaces shall use standardized fasteners and mounting patterns where practical.

**Verification:**  
CAD and BOM review.

---

# 5. Component-Mounting Requirements

## REQ-ME-013 — Flight Controller Mount

The airframe shall provide a stable mounting interface for the Rev A Flight Controller.

**Verification:**  
Assembly inspection.

---

## REQ-ME-014 — Flight Controller Access

The Flight Controller mount shall preserve access to required:

- USB connection
- SWD connection
- Power connections
- Signal connections
- Reset or boot controls where used

**Verification:**  
Assembly demonstration.

---

## REQ-ME-015 — ESC Mount

The airframe shall provide a secure mount for the four-in-one ESC.

**Verification:**  
Assembly inspection.

---

## REQ-ME-016 — ESC Cooling

The ESC mount shall not unnecessarily obstruct cooling surfaces or airflow.

**Verification:**  
Design inspection and temperature testing.

---

## REQ-ME-017 — Fastener Compatibility

Mounting features shall use fasteners compatible with the actual component hole sizes and board construction.

**Verification:**  
Assembly inspection.

---

## REQ-ME-018 — Electronics Clearance

Mounted electronics shall have clearance from conductive fasteners, solder joints, and structural surfaces that could cause damage or short circuits.

**Verification:**  
Inspection.

---

## REQ-ME-019 — Connector Clearance

Mechanical components shall provide sufficient space to insert, remove, and route required connectors.

**Verification:**  
Assembly demonstration.

---

# 6. Propulsion-Geometry Requirements

## REQ-ME-020 — Motor Position Accuracy

Motor centers shall be positioned according to the approved airframe geometry.

**Verification:**  
Dimensional inspection.

---

## REQ-ME-021 — Motor-Mount Compatibility

Each motor mount shall match the selected motor mounting pattern.

**Verification:**  
CAD and hardware inspection.

---

## REQ-ME-022 — Motor Fastener Retention

Motor fasteners shall provide secure engagement without contacting motor windings.

**Verification:**  
Assembly inspection.

---

## REQ-ME-023 — Propeller Clearance

Each propeller shall clear:

- Airframe components
- Wiring
- Battery
- Electronics
- Adjacent propellers
- Future protective features

**Verification:**  
CAD analysis and physical rotation test.

---

## REQ-ME-024 — Deflection Allowance

Propeller clearance shall include reasonable allowance for manufacturing tolerance, structural deflection, and minor deformation.

**Verification:**  
Design review.

---

## REQ-ME-025 — Motor-Wire Routing

Motor wiring shall be routable without contact with propellers or motor bells.

**Verification:**  
Assembly inspection.

---

# 7. Battery-Mounting Requirements

## REQ-ME-026 — Battery Retention

The battery mount shall retain the selected 4S 850 mAh battery during expected aircraft motion and landing loads.

**Verification:**  
Retention test.

---

## REQ-ME-027 — Battery Removal

The battery shall be removable for charging, inspection, and replacement.

**Verification:**  
Serviceability demonstration.

---

## REQ-ME-028 — Battery-Strap Compatibility

The airframe shall support at least one secure battery strap or equivalent retention mechanism.

**Verification:**  
Assembly inspection.

---

## REQ-ME-029 — Battery Protection

The battery location should reduce exposure to:

- Propeller contact
- Sharp fasteners
- Abrasive surfaces
- Pinching
- Direct impact

**Verification:**  
Design and assembly inspection.

---

## REQ-ME-030 — Center-of-Mass Adjustment

The battery mount should permit limited adjustment to support aircraft center-of-mass balancing.

**Verification:**  
Adjustment demonstration.

---

## REQ-ME-031 — Battery Connector Access

The battery connector shall remain accessible without disassembling unrelated modules.

**Verification:**  
Assembly demonstration.

---

# 8. Sensor-Mounting Requirements

## REQ-ME-032 — IMU Position

The IMU should be mounted near the aircraft center of rotation where practical.

**Verification:**  
CAD inspection.

---

## REQ-ME-033 — IMU Orientation

The IMU mount shall maintain a known orientation relative to the airframe.

**Verification:**  
Inspection and axis documentation.

---

## REQ-ME-034 — IMU Rotation Prevention

The IMU mount shall prevent unintended rotation or ambiguous installation.

**Verification:**  
Assembly inspection.

---

## REQ-ME-035 — IMU Vibration Control

The IMU mount shall avoid unnecessary structural flexibility and should permit future vibration-isolation refinement.

**Verification:**  
Design review and sensor-data testing.

---

## REQ-ME-036 — IMU Accessibility

The IMU shall remain accessible for inspection, replacement, and wiring changes.

**Verification:**  
Serviceability demonstration.

---

# 9. Wiring-Accommodation Requirements

## REQ-ME-037 — Protected Routing

Mechanical routing features shall protect wiring from:

- Propellers
- Sharp edges
- Pinch points
- Abrasion
- Motor bells
- Excessive movement

**Verification:**  
Assembly inspection.

---

## REQ-ME-038 — Bend Radius

Cable routing shall avoid unnecessarily sharp bends at connectors and solder joints.

**Verification:**  
Inspection.

---

## REQ-ME-039 — Strain Relief

The mechanical design shall provide or permit strain relief near vulnerable connectors and solder joints.

**Verification:**  
Inspection.

---

## REQ-ME-040 — Harness Serviceability

Wiring shall be removable or replaceable without destructive airframe modification where practical.

**Verification:**  
Serviceability demonstration.

---

## REQ-ME-041 — Signal Separation Accommodation

The airframe should permit physical separation between high-current propulsion wiring and sensitive sensor wiring.

**Verification:**  
Routing inspection.

---

# 10. Additive-Manufacturing Requirements

## REQ-ME-042 — Printable Rev A Structure

Primary Rev A custom mechanical parts shall be manufacturable using fused-filament fabrication unless another process is approved.

**Verification:**  
Manufacturing demonstration.

---

## REQ-ME-043 — Support Reduction

Parts should be designed to minimize unnecessary support material.

**Verification:**  
Slicer and manufacturing review.

---

## REQ-ME-044 — Defined Print Orientation

Flight-intent printed parts shall have a documented print orientation.

**Verification:**  
Manufacturing record inspection.

---

## REQ-ME-045 — Critical Interface Calibration

Critical printed holes and insert bores shall be validated using test parts or dimensional inspection.

**Verification:**  
Coupon or part measurement.

---

## REQ-ME-046 — Parametric Design

Critical mounting patterns and envelopes should be controlled by named CAD parameters.

**Verification:**  
CAD inspection.

---

## REQ-ME-047 — Source Model Retention

Editable CAD source files shall be retained for all custom flight-intent parts.

**Verification:**  
Repository inspection.

---

## REQ-ME-048 — Manufacturing Revision

Manufacturing exports shall identify the applicable part revision.

**Verification:**  
Filename and repository inspection.

---

# 11. Structural Requirements

## REQ-ME-049 — Propulsion Load Path

Motor thrust and torque shall be transferred through intentional structural load paths.

**Verification:**  
Design review.

---

## REQ-ME-050 — Landing Load Resistance

The airframe shall tolerate normal takeoff, landing, and handling loads without structural failure.

**Verification:**  
Bench and flight testing.

---

## REQ-ME-051 — Fastener Load Support

Fastener locations shall include sufficient surrounding material to support expected loads.

**Verification:**  
CAD and physical inspection.

---

## REQ-ME-052 — Insert Retention

Heat-set inserts shall remain secure during normal assembly and service.

**Verification:**  
Installation and pullout inspection.

---

## REQ-ME-053 — No Known Structural Damage

Parts with cracks, major warping, delamination, or failed inserts shall not be used for flight.

**Verification:**  
Preflight inspection.

---

## REQ-ME-054 — Weight Awareness

Mechanical parts shall avoid unnecessary mass while preserving structural integrity, serviceability, and manufacturability.

**Verification:**  
Design and mass review.

---

# 12. Serviceability Requirements

## REQ-ME-055 — Common Tool Access

Routine assembly and maintenance shall use common metric hand tools where practical.

**Verification:**  
Maintenance demonstration.

---

## REQ-ME-056 — Fastener Access

Frequently serviced fasteners shall remain accessible without excessive disassembly.

**Verification:**  
Inspection.

---

## REQ-ME-057 — Independent Motor Replacement

Each motor should be replaceable without removing the complete electronics stack.

**Verification:**  
Serviceability demonstration.

---

## REQ-ME-058 — Wear-Item Replacement

Battery straps, landing features, guards, and sacrificial parts should be independently replaceable.

**Verification:**  
Design review.

---

## REQ-ME-059 — Assembly Sequence

Assemblies with order-dependent installation shall have a documented assembly sequence.

**Verification:**  
Documentation review.

---

# 13. Expansion Requirements

## REQ-ME-060 — GPS Mounting Provision

The mechanical architecture should permit future mounting of a GNSS receiver and antenna.

**Verification:**  
Architecture review.

---

## REQ-ME-061 — Camera Mounting Provision

The architecture should permit future integration of a camera.

**Verification:**  
Architecture review.

---

## REQ-ME-062 — Companion-Computer Provision

The architecture should permit future integration of a lightweight companion computer or payload module.

**Verification:**  
Architecture review.

---

## REQ-ME-063 — Custom PCB Compatibility

Future custom Flight Controller integration should not require complete replacement of the validated airframe architecture.

**Verification:**  
Architecture review.

---

# 14. Inspection and Verification Requirements

## REQ-ME-064 — Preflight Mechanical Inspection

Before flight, inspect:

- Fasteners
- Arms
- Motor mounts
- Propeller clearance
- Battery retention
- Electronics retention
- Wiring clearance
- Printed-part condition
- Sensor orientation

**Verification:**  
Checklist completion.

---

## REQ-ME-065 — Post-Impact Inspection

Following a hard landing or impact, affected structural and mounting components shall be inspected before further flight.

**Verification:**  
Inspection record.

---

## REQ-ME-066 — Dimensional Verification

Critical interfaces shall be dimensionally verified before integration.

**Verification:**  
Measurement record.

---

# 15. Requirement Summary

| Requirement Range | Area |
| --- | --- |
| REQ-ME-001 through REQ-ME-006 | Airframe |
| REQ-ME-007 through REQ-ME-012 | Modularity |
| REQ-ME-013 through REQ-ME-019 | Component mounting |
| REQ-ME-020 through REQ-ME-025 | Propulsion geometry |
| REQ-ME-026 through REQ-ME-031 | Battery mounting |
| REQ-ME-032 through REQ-ME-036 | Sensor mounting |
| REQ-ME-037 through REQ-ME-041 | Wiring accommodation |
| REQ-ME-042 through REQ-ME-048 | Additive manufacturing |
| REQ-ME-049 through REQ-ME-054 | Structure |
| REQ-ME-055 through REQ-ME-059 | Serviceability |
| REQ-ME-060 through REQ-ME-063 | Expansion |
| REQ-ME-064 through REQ-ME-066 | Inspection and verification |

---

# 16. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Requirements Index
- **ARC-001** — Stratus System Architecture
- **SES-001** — Mechanical Engineering Standard
- **BOM-001** — Bill of Materials
- **ADR-002** — Rev A Platform Size
- **ADR-003** — Modular Airframe Architecture
- **HDR-002** — Motor Selection
- **HDR-004** — Propeller Selection
- **HDR-006** — Mechanical Hardware Standard

---

# 17. Related Documents

## Upstream

- SPEC-001
- ARC-001
- REQ-001

## Peer

- REQ-HW-001 — Hardware Requirements
- REQ-SW-001 — Software Requirements
- REQ-EL-001 — Electrical Requirements
- SES-001 — Mechanical Engineering Standard

## Downstream

- CAD models
- Manufacturing exports
- Assembly procedures
- Mechanical inspection records