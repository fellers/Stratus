# Stratus Electrical Requirements

**Document ID:** REQ-EL-001  
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
| 1.0 | 2026-08-02 | Initial electrical requirements | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Power Architecture Requirements
4. Battery Interface Requirements
5. Voltage-Regulation Requirements
6. Grounding Requirements
7. Wiring Requirements
8. Connector Requirements
9. Sensor Interface Requirements
10. ESC and Motor Interface Requirements
11. Debug and Communication Interface Requirements
12. Protection and Safety Requirements
13. Assembly Requirements
14. Inspection and Test Requirements
15. Expansion Requirements
16. Requirement Summary
17. References
18. Related Documents

---

# 1. Purpose

This document defines the electrical requirements for Stratus Rev A.

These requirements govern power distribution, voltage regulation, grounding, wiring, connectors, soldering, digital interfaces, propulsion interfaces, electrical protection, and verification.

---

# 2. Scope

This document applies to:

- Battery interface
- Primary power wiring
- Regulated electronics power
- Grounds and return paths
- Flight Controller wiring
- IMU wiring
- ESC signals
- Motor conductors
- Debug interfaces
- Communication interfaces
- Connectors
- Harnesses
- Solder joints
- Electrical inspection and testing

Detailed electrical engineering practices are defined in **SES-002**.

---

# 3. Power Architecture Requirements

## REQ-EL-001 — Defined Power Architecture

The electrical design shall define the source and destination of each power rail.

**Verification:**  
Wiring-diagram inspection.

---

## REQ-EL-002 — Power-Rail Identification

Each rail shall identify:

- Nominal voltage
- Maximum expected voltage
- Source
- Loads
- Current capacity
- Ground reference

**Verification:**  
Documentation inspection.

---

## REQ-EL-003 — Propulsion and Electronics Distribution

The design shall provide battery-level power to the ESC and regulated power to logic electronics.

**Verification:**  
Wiring inspection and voltage measurement.

---

## REQ-EL-004 — No Undocumented Power Paths

The released flight configuration shall not rely on undocumented or accidental power paths.

**Verification:**  
Continuity and design inspection.

---

## REQ-EL-005 — Power-Off Assembly

Electrical assembly and connector changes shall be performed with the propulsion battery disconnected.

**Verification:**  
Procedure review.

---

# 4. Battery Interface Requirements

## REQ-EL-006 — Battery Type

Rev A shall support a 4S lithium-polymer battery.

**Verification:**  
Hardware inspection.

---

## REQ-EL-007 — Maximum Battery Voltage

Battery-connected components shall support at least 16.8 V.

**Verification:**  
Component-rating review.

---

## REQ-EL-008 — XT30 Interface

The propulsion battery interface shall use an XT30 connector.

**Verification:**  
Hardware inspection.

---

## REQ-EL-009 — Battery Polarity

Battery polarity shall be consistent throughout the aircraft and documented.

**Verification:**  
Continuity and inspection.

---

## REQ-EL-010 — Battery-Conductor Rating

Battery conductors shall be rated for expected continuous and transient current.

**Verification:**  
Wire-gauge analysis and current test.

---

## REQ-EL-011 — Exposed Conductor Protection

Battery-level conductive surfaces shall be insulated or enclosed against accidental short circuits.

**Verification:**  
Inspection.

---

## REQ-EL-012 — Accessible Disconnect

The battery connector shall remain accessible as the primary propulsion-power disconnect.

**Verification:**  
Assembly inspection.

---

# 5. Voltage-Regulation Requirements

## REQ-EL-013 — Compatible Logic Supply

The Flight Controller and IMU shall receive supply voltage within their approved operating ranges.

**Verification:**  
Voltage measurement.

---

## REQ-EL-014 — Regulator Current Capacity

Each regulator shall provide sufficient current for connected loads with appropriate margin.

**Verification:**  
Load analysis and measurement.

---

## REQ-EL-015 — Startup Stability

Regulated rails shall reach valid operating voltage without causing uncontrolled motor commands.

**Verification:**  
Startup measurement.

---

## REQ-EL-016 — Transient Stability

Regulated rails shall remain within acceptable limits during expected propulsion transients.

**Verification:**  
Oscilloscope measurement.

---

## REQ-EL-017 — Rail Decoupling

Power rails shall use appropriate local decoupling as required by the connected devices and modules.

**Verification:**  
Hardware inspection and manufacturer-document review.

---

## REQ-EL-018 — Voltage Test Access

Critical regulated rails should be accessible for voltage measurement.

**Verification:**  
Hardware inspection.

---

# 6. Grounding Requirements

## REQ-EL-019 — Common Logic Reference

The Flight Controller, IMU, ESC-control interface, and development interfaces shall share a valid ground reference unless explicitly isolated.

**Verification:**  
Continuity test.

---

## REQ-EL-020 — Controlled Return Paths

High-current return paths shall be arranged to minimize disturbance of sensitive sensor and logic references.

**Verification:**  
Design review and noise measurement.

---

## REQ-EL-021 — IMU Ground Connection

The IMU shall use a short and reliable ground connection to the Flight Controller electrical reference.

**Verification:**  
Wiring inspection.

---

## REQ-EL-022 — Debug Ground

External debug and test equipment shall connect to system ground unless the instrument is electrically isolated.

**Verification:**  
Bench procedure and connection inspection.

---

## REQ-EL-023 — Ground-Loop Review

Unnecessary parallel ground paths shall be avoided where they may produce noise or unintended current flow.

**Verification:**  
Design review.

---

# 7. Wiring Requirements

## REQ-EL-024 — Stranded Conductors

Flight wiring subject to vibration or flexing shall use stranded copper conductors.

**Verification:**  
Inspection.

---

## REQ-EL-025 — Wire-Gauge Selection

Wire gauge shall be selected according to:

- Maximum current
- Length
- Voltage drop
- Temperature rise
- Connector rating
- Flexibility

**Verification:**  
Engineering review.

---

## REQ-EL-026 — Preferred Wire Gauges

Rev A should use the following preferred conductor sizes where appropriate:

| Gauge | Intended Use |
| --- | --- |
| 18 AWG | Primary battery and high-current power |
| 22 AWG | Moderate-current regulated power |
| 24 AWG | Low-current power and digital signals |

**Verification:**  
Harness inspection.

---

## REQ-EL-027 — Power Color Convention

Red or orange shall identify positive power and black shall identify ground where mixed-color wiring is available.

**Verification:**  
Inspection.

---

## REQ-EL-028 — Ground Color Reservation

Black wire should not be used for non-ground functions in mixed-color harnesses.

**Verification:**  
Inspection.

---

## REQ-EL-029 — Wire-Length Control

Wires shall be long enough for assembly and strain relief but shall avoid unnecessary excess length.

**Verification:**  
Harness inspection.

---

## REQ-EL-030 — Propeller Exclusion

No wire shall enter a propeller operating envelope.

**Verification:**  
Mechanical and electrical inspection.

---

## REQ-EL-031 — Abrasion Protection

Wiring contacting printed or structural surfaces shall be protected where abrasion is possible.

**Verification:**  
Inspection.

---

## REQ-EL-032 — Strain Relief

Wiring shall not transfer uncontrolled mechanical load directly to solder joints or connector terminals.

**Verification:**  
Inspection and light pull test.

---

# 8. Connector Requirements

## REQ-EL-033 — Connector Rating

Each connector shall be rated for the voltage and current of its circuit.

**Verification:**  
Component review.

---

## REQ-EL-034 — Polarized Power Connectors

Power connectors shall be polarized where practical.

**Verification:**  
Inspection.

---

## REQ-EL-035 — Signal Connector Orientation

Unkeyed signal connectors shall have documented orientation and pin numbering.

**Verification:**  
Documentation and hardware inspection.

---

## REQ-EL-036 — Connector Retention

Connectors used in flight shall have sufficient retention for expected vibration.

**Verification:**  
Inspection and vibration testing.

---

## REQ-EL-037 — Connector Interchange Prevention

Physically interchangeable connectors carrying incompatible voltages or functions should be avoided.

**Verification:**  
Design review.

---

## REQ-EL-038 — Serviceable Connections

Frequently replaced modules should use serviceable connectors where practical.

**Verification:**  
Architecture and assembly review.

---

# 9. Sensor Interface Requirements

## REQ-EL-039 — IMU SPI Interface

The IMU shall connect to the Flight Controller through SPI.

**Verification:**  
Wiring inspection and communication test.

---

## REQ-EL-040 — IMU Required Signals

The IMU connection shall provide:

- Compatible power
- Ground
- SCK
- MOSI
- MISO
- Chip select

**Verification:**  
Pinout and continuity test.

---

## REQ-EL-041 — IMU Interrupt Provision

At least one IMU interrupt signal should be connected or made available.

**Verification:**  
Wiring inspection.

---

## REQ-EL-042 — Chip-Select Default State

The IMU chip-select line shall remain in its inactive state during reset and initialization unless communication is intentionally occurring.

**Verification:**  
Logic-analyzer measurement.

---

## REQ-EL-043 — IMU Signal Routing

IMU signals shall be kept reasonably short and routed away from motor phase conductors where practical.

**Verification:**  
Harness inspection.

---

## REQ-EL-044 — Logic-Level Compatibility

All IMU signals shall be compatible with the Flight Controller logic levels.

**Verification:**  
Datasheet and interface review.

---

# 10. ESC and Motor Interface Requirements

## REQ-EL-045 — Four ESC Control Signals

The Flight Controller shall provide one independently controlled signal for each ESC channel.

**Verification:**  
Wiring and signal test.

---

## REQ-EL-046 — ESC Ground Reference

ESC control signals shall have a valid ground reference to the Flight Controller.

**Verification:**  
Continuity test.

---

## REQ-EL-047 — Non-Commanding Reset Level

Motor-control lines shall remain at a defined non-commanding electrical level during reset and startup.

**Verification:**  
Logic-analyzer or oscilloscope measurement.

---

## REQ-EL-048 — Motor Phase Conductors

Each motor shall connect to its ESC channel using three conductors rated for expected current.

**Verification:**  
Harness inspection.

---

## REQ-EL-049 — Motor-Conductor Retention

Motor phase wiring shall be mechanically secured and protected from propeller or motor-bell contact.

**Verification:**  
Inspection.

---

## REQ-EL-050 — Motor Direction Adjustability

The electrical configuration shall permit motor direction correction by approved phase-wire exchange or control configuration.

**Verification:**  
Bench test without propellers.

---

# 11. Debug and Communication Interface Requirements

## REQ-EL-051 — SWD Signals

The debug interface shall provide:

- SWDIO
- SWCLK
- Ground
- Target-voltage reference
- Reset where practical

**Verification:**  
Pinout inspection and debugging demonstration.

---

## REQ-EL-052 — Debug Voltage Compatibility

The debugger and target shall use compatible logic voltage.

**Verification:**  
Voltage measurement.

---

## REQ-EL-053 — Debug Power Clarification

Documentation shall distinguish target-voltage reference pins from debugger power-output pins.

**Verification:**  
Documentation inspection.

---

## REQ-EL-054 — Multiple-Power-Source Prevention

The target shall not be unintentionally powered from multiple sources unless the electrical design explicitly supports it.

**Verification:**  
Bench procedure and wiring inspection.

---

## REQ-EL-055 — Development UART

The hardware shall provide transmit, receive, and ground connections for a development UART.

**Verification:**  
Continuity and functional test.

---

## REQ-EL-056 — UART Logic Compatibility

The development UART shall use logic levels compatible with the Flight Controller and connected adapter.

**Verification:**  
Voltage and datasheet inspection.

---

## REQ-EL-057 — Test-Equipment Compatibility

Test-equipment connections shall remain within the electrical ratings of the Flight Controller and attached modules.

**Verification:**  
Bench procedure review.

---

# 12. Protection and Safety Requirements

## REQ-EL-058 — Initial Current Limiting

Initial power-up should use a current-limited supply, smoke stopper, or equivalent protection where practical.

**Verification:**  
Bring-up procedure review.

---

## REQ-EL-059 — Reverse-Polarity Prevention

The electrical design shall minimize the likelihood of reverse-polarity connection.

**Verification:**  
Interface inspection.

---

## REQ-EL-060 — Short-Circuit Inspection

The assembly shall be checked for shorts between positive power and ground before first battery connection.

**Verification:**  
Resistance or continuity measurement.

---

## REQ-EL-061 — LiPo Safety

LiPo batteries shall be charged, stored, inspected, and retired according to accepted LiPo safety practices.

**Verification:**  
Procedure review and battery inspection.

---

## REQ-EL-062 — Damaged Battery Prohibition

Swollen, punctured, overheated, or otherwise damaged batteries shall not be used.

**Verification:**  
Pre-use inspection.

---

## REQ-EL-063 — Propeller-Free Electrical Bring-Up

Electrical motor-output tests shall initially be performed without installed propellers.

**Verification:**  
Test procedure observation.

---

## REQ-EL-064 — Thermal Damage Prohibition

Wiring, connectors, or PCBs showing significant heat damage shall not be used for flight until repaired or replaced and reverified.

**Verification:**  
Inspection.

---

# 13. Assembly Requirements

## REQ-EL-065 — Solder-Joint Quality

Solder joints shall be mechanically secure, electrically continuous, and free of bridges or loose strands.

**Verification:**  
Visual inspection and continuity test.

---

## REQ-EL-066 — Exposed-Conductor Control

Soldered connections shall not leave unnecessary exposed conductor.

**Verification:**  
Inspection.

---

## REQ-EL-067 — Heat-Shrink Insulation

Heat-shrink tubing or equivalent insulation shall protect exposed inline joints and splices.

**Verification:**  
Inspection.

---

## REQ-EL-068 — Crimp Tooling

Crimp terminals shall be installed using tooling suitable for the terminal family.

**Verification:**  
Process and pull-test review.

---

## REQ-EL-069 — Splice Minimization

Splices shall be minimized in flight harnesses.

**Verification:**  
Harness inspection.

---

## REQ-EL-070 — Harness Documentation

Flight harnesses shall document:

- Source
- Destination
- Signal
- Wire gauge
- Color
- Connector
- Pin assignment

**Verification:**  
Documentation inspection.

---

# 14. Inspection and Test Requirements

## REQ-EL-071 — Pre-Power Inspection

Before first power application, inspect:

- Polarity
- Connector orientation
- Solder joints
- Loose strands
- Exposed conductors
- Wire routing
- Voltage ratings
- Ground continuity
- Power-to-ground resistance

**Verification:**  
Inspection checklist.

---

## REQ-EL-072 — Regulated-Rail Measurement

Regulated rails shall be measured before connecting sensitive loads where practical.

**Verification:**  
Voltage measurement.

---

## REQ-EL-073 — Interface Continuity Test

Signal and power interfaces shall be checked for intended continuity and unintended shorts.

**Verification:**  
Continuity test.

---

## REQ-EL-074 — Incremental Electrical Bring-Up

Electrical interfaces shall be verified incrementally before integrated propulsion testing.

**Verification:**  
Bring-up record.

---

## REQ-EL-075 — Post-Test Inspection

Following abnormal behavior, high-current testing, or impact, electrical assemblies shall be inspected for damage.

**Verification:**  
Inspection record.

---

## REQ-EL-076 — Power-Noise Measurement

Power-rail noise and voltage droop should be measured during propulsion testing.

**Verification:**  
Oscilloscope record.

---

# 15. Expansion Requirements

## REQ-EL-077 — Navigation-Sensor Power Provision

The electrical architecture should permit future power and communication for navigation sensors.

**Verification:**  
Architecture review.

---

## REQ-EL-078 — Radio Integration Provision

The electrical architecture should permit future radio integration using an available communication interface and compatible power rail.

**Verification:**  
Architecture review.

---

## REQ-EL-079 — Custom PCB Migration

Electrical interface definitions shall support migration to a custom Flight Controller PCB.

**Verification:**  
Architecture review.

---

## REQ-EL-080 — Battery Monitoring Expansion

The design should permit future battery-voltage and current monitoring.

**Verification:**  
Architecture review.

---

# 16. Requirement Summary

| Requirement Range | Area |
| --- | --- |
| REQ-EL-001 through REQ-EL-005 | Power architecture |
| REQ-EL-006 through REQ-EL-012 | Battery interface |
| REQ-EL-013 through REQ-EL-018 | Voltage regulation |
| REQ-EL-019 through REQ-EL-023 | Grounding |
| REQ-EL-024 through REQ-EL-032 | Wiring |
| REQ-EL-033 through REQ-EL-038 | Connectors |
| REQ-EL-039 through REQ-EL-044 | Sensor interface |
| REQ-EL-045 through REQ-EL-050 | ESC and motor interface |
| REQ-EL-051 through REQ-EL-057 | Debug and communications |
| REQ-EL-058 through REQ-EL-064 | Protection and safety |
| REQ-EL-065 through REQ-EL-070 | Assembly |
| REQ-EL-071 through REQ-EL-076 | Inspection and testing |
| REQ-EL-077 through REQ-EL-080 | Expansion |

---

# 17. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Requirements Index
- **ARC-001** — Stratus System Architecture
- **SES-002** — Electrical Engineering Standard
- **BOM-001** — Bill of Materials
- **HDR-001** — ICM-20602 IMU
- **HDR-003** — Aero Selfie 45A ESC
- **HDR-005** — 4S Power System
- **HDR-007** — Wiring Materials Standard
- **REQ-HW-001** — Hardware Requirements

---

# 18. Related Documents

## Upstream

- SPEC-001
- ARC-001
- REQ-001

## Peer

- REQ-HW-001 — Hardware Requirements
- REQ-SW-001 — Software Requirements
- REQ-ME-001 — Mechanical Requirements
- SES-002 — Electrical Engineering Standard

## Downstream

- Wiring diagrams
- Harness definitions
- Connector pinouts
- Electrical bring-up procedures
- Electrical verification records