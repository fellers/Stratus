# Stratus Hardware Requirements

**Document ID:** REQ-HW-001  
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
| 1.0 | 2026-08-02 | Initial hardware requirements | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Hardware Architecture
4. Flight Controller Requirements
5. Sensor Requirements
6. Propulsion Requirements
7. Power-System Requirements
8. Communication and Debug Requirements
9. Expansion Requirements
10. Environmental and Reliability Requirements
11. Safety Requirements
12. Verification Requirements
13. Requirement Summary
14. References
15. Related Documents

---

# 1. Purpose

This document defines the hardware requirements for Stratus Rev A.

These requirements govern the selection, integration, operation, and verification of the physical electronic and electromechanical components used by the aircraft.

---

# 2. Scope

This document applies to:

- Flight Controller
- Microcontroller
- Inertial Measurement Unit
- Electronic Speed Controller
- Motors
- Propellers
- Battery
- Voltage regulation
- Debug interfaces
- Communication interfaces
- Expansion interfaces
- Supporting electronic hardware

Mechanical construction requirements are defined in **REQ-ME-001**.

Electrical assembly and wiring requirements are defined in **REQ-EL-001** and **SES-002**.

---

# 3. Hardware Architecture

## REQ-HW-001 — Modular Hardware Architecture

Stratus hardware shall be organized into replaceable subsystems with defined mechanical and electrical interfaces.

**Verification:**  
Architecture and integration review.

---

## REQ-HW-002 — Rev A Development Hardware

Rev A may use commercially available development boards and breakout modules to validate the system architecture before development of a custom Flight Controller PCB.

**Verification:**  
Design inspection.

---

## REQ-HW-003 — Hardware Documentation

Each hardware subsystem shall have sufficient documentation to identify:

- Manufacturer
- Part number
- Electrical ratings
- Interface type
- Pinout
- Mechanical envelope
- Firmware dependencies
- Known limitations

**Verification:**  
Documentation inspection.

---

## REQ-HW-004 — Hardware Compatibility

All interconnected hardware shall be electrically, mechanically, and functionally compatible.

**Verification:**  
Interface review and functional test.

---

# 4. Flight Controller Requirements

## REQ-HW-005 — Processor Architecture

The Flight Controller shall use an ARM Cortex-M-class microcontroller suitable for deterministic embedded flight-control execution.

**Verification:**  
Component inspection.

---

## REQ-HW-006 — Rev A Microcontroller

Stratus Rev A shall use an STM32H743-class microcontroller platform unless superseded by an approved Architecture Decision Record.

**Verification:**  
BOM and hardware inspection.

---

## REQ-HW-007 — Floating-Point Support

The microcontroller shall provide hardware floating-point support suitable for state-estimation and control calculations.

**Verification:**  
Datasheet inspection and firmware build verification.

---

## REQ-HW-008 — Program Memory

The Flight Controller shall provide sufficient nonvolatile program memory for:

- Platform support
- Device drivers
- State estimation
- Flight control
- Motor output
- Communications
- Diagnostics
- Future Rev A expansion

**Verification:**  
Memory-map review and build-size measurement.

---

## REQ-HW-009 — Data Memory

The Flight Controller shall provide sufficient RAM for:

- Runtime state
- Fixed-capacity communication buffers
- Sensor buffers
- Control data
- Diagnostic data
- Stack
- DMA buffers

**Verification:**  
Memory analysis.

---

## REQ-HW-010 — Hardware Timers

The Flight Controller shall provide hardware timers sufficient for:

- Monotonic timekeeping
- Periodic scheduling
- Motor-output generation
- Performance measurement
- Timeouts

**Verification:**  
Peripheral allocation review.

---

## REQ-HW-011 — SPI Availability

The Flight Controller shall provide at least one SPI peripheral compatible with the selected IMU.

**Verification:**  
Pinout and peripheral inspection.

---

## REQ-HW-012 — UART Availability

The Flight Controller shall provide at least one UART for development diagnostics and at least one additional communication path or expansion option.

**Verification:**  
Peripheral and pinout inspection.

---

## REQ-HW-013 — Debug Access

The Flight Controller shall expose SWDIO, SWCLK, ground, and target-voltage reference.

Access to reset should also be provided.

**Verification:**  
Hardware inspection and debugger connection test.

---

## REQ-HW-014 — USB Support

The Flight Controller shall support USB operation sufficient for firmware programming, recovery, or future communication where supported by the selected board.

**Verification:**  
Functional demonstration.

---

## REQ-HW-015 — Safe Output State

Flight Controller pins connected to motor-control inputs shall remain in a non-commanding state during reset and early startup.

**Verification:**  
Oscilloscope or logic-analyzer measurement.

---

# 5. Sensor Requirements

## REQ-HW-016 — Primary IMU

Stratus Rev A shall use an ICM-20602 six-axis IMU unless superseded by an approved hardware decision.

**Verification:**  
BOM and hardware inspection.

---

## REQ-HW-017 — IMU Measurements

The IMU shall provide:

- Three-axis angular-rate measurements
- Three-axis acceleration measurements

**Verification:**  
Datasheet review and functional test.

---

## REQ-HW-018 — IMU Interface

The primary IMU shall communicate with the Flight Controller through SPI.

**Verification:**  
Wiring inspection and communication test.

---

## REQ-HW-019 — IMU Logic Compatibility

The IMU interface shall be electrically compatible with the Flight Controller logic voltage.

**Verification:**  
Datasheet and interface review.

---

## REQ-HW-020 — IMU Interrupt Support

The hardware should provide access to at least one IMU interrupt or data-ready output.

**Verification:**  
Pinout inspection.

---

## REQ-HW-021 — Sensor Orientation

The IMU shall be mounted in a known and documented orientation relative to the aircraft coordinate system.

**Verification:**  
Mechanical and documentation inspection.

---

## REQ-HW-022 — Sensor Replacement

The Rev A IMU module should be replaceable without replacement of the complete airframe.

**Verification:**  
Serviceability demonstration.

---

# 6. Propulsion Requirements

## REQ-HW-023 — Motor Quantity

Stratus Rev A shall use four brushless motors.

**Verification:**  
Hardware inspection.

---

## REQ-HW-024 — Rev A Motors

Rev A shall use HappyModel EX1404 motors unless superseded by an approved hardware decision.

**Verification:**  
BOM and hardware inspection.

---

## REQ-HW-025 — Electronic Speed Controller

Rev A shall use a four-channel ESC capable of independently controlling all four motors.

**Verification:**  
Component inspection and functional test.

---

## REQ-HW-026 — Rev A ESC

Rev A shall use the Aero Selfie 45A four-in-one ESC unless superseded by an approved hardware decision.

**Verification:**  
BOM and hardware inspection.

---

## REQ-HW-027 — ESC Voltage Rating

The ESC shall be rated for the maximum voltage of the selected 4S battery.

**Verification:**  
Manufacturer specification review.

---

## REQ-HW-028 — ESC Current Capability

The ESC shall provide sufficient continuous and transient current capacity for the selected motors and propellers.

**Verification:**  
Component analysis and propulsion test.

---

## REQ-HW-029 — Independent Motor Channels

Each motor shall be controlled through an independently addressable ESC channel.

**Verification:**  
Motor-mapping test.

---

## REQ-HW-030 — Propeller Compatibility

Propellers shall be compatible with:

- Motor shaft and mounting arrangement
- Motor operating range
- Frame size
- Required rotation direction
- Expected battery voltage

**Verification:**  
Mechanical inspection and controlled propulsion testing.

---

## REQ-HW-031 — Rev A Propellers

Rev A shall use Gemfan Hurricane 3520 propellers unless superseded by an approved hardware decision.

**Verification:**  
BOM and hardware inspection.

---

## REQ-HW-032 — Propeller Removal During Bench Test

Propellers shall be removable so motor control can be tested safely without installed propellers.

**Verification:**  
Inspection and test procedure review.

---

# 7. Power-System Requirements

## REQ-HW-033 — Battery Configuration

Stratus Rev A shall use a 4S lithium-polymer battery.

**Verification:**  
Battery inspection.

---

## REQ-HW-034 — Rev A Battery Capacity

The baseline Rev A battery capacity shall be approximately 850 mAh unless changed through an approved design decision.

**Verification:**  
BOM inspection.

---

## REQ-HW-035 — Battery Connector

The propulsion battery interface shall use an XT30 connector.

**Verification:**  
Hardware inspection.

---

## REQ-HW-036 — Maximum Battery Voltage

All battery-connected hardware shall tolerate at least 16.8 V.

**Verification:**  
Component-rating review.

---

## REQ-HW-037 — Electronics Regulation

The hardware shall provide regulated power compatible with the Flight Controller, IMU, and supporting electronics.

**Verification:**  
Voltage measurement.

---

## REQ-HW-038 — Regulator Capacity

The regulated power source shall support all connected electronics with sufficient current margin for startup and expected expansion.

**Verification:**  
Load analysis and current measurement.

---

## REQ-HW-039 — Power Stability

The electronics supply shall remain within acceptable limits during normal motor operation and expected propulsion transients.

**Verification:**  
Oscilloscope measurement during propulsion testing.

---

## REQ-HW-040 — Battery Monitoring Provision

The hardware should provide a method for measuring battery voltage using the Flight Controller.

**Verification:**  
Design inspection and future functional test.

---

## REQ-HW-041 — Common Ground Reference

The Flight Controller, IMU, ESC control interface, and communication interfaces shall share a valid electrical reference unless explicitly isolated.

**Verification:**  
Continuity and interface inspection.

---

# 8. Communication and Debug Requirements

## REQ-HW-042 — SWD Debugger Compatibility

The Flight Controller shall be compatible with a genuine ST-Link debugger.

**Verification:**  
Programming and debugging demonstration.

---

## REQ-HW-043 — External Debug Connection

The debug interface shall support connection without requiring permanent modification of the Flight Controller.

**Verification:**  
Connection demonstration.

---

## REQ-HW-044 — Diagnostic UART Access

The diagnostic UART shall be physically accessible during bench development.

**Verification:**  
Hardware inspection.

---

## REQ-HW-045 — Communication Expansion

The hardware shall provide at least one available interface suitable for future radio or telemetry integration.

Suitable interfaces may include:

- UART
- SPI
- USB
- CAN
- Another documented digital interface

**Verification:**  
Peripheral allocation review.

---

# 9. Expansion Requirements

## REQ-HW-046 — Navigation-Sensor Expansion

The hardware architecture should support future integration of navigation sensors.

Potential devices include:

- GNSS receiver
- Magnetometer
- Barometer
- Optical-flow sensor
- Range sensor

**Verification:**  
Architecture review.

---

## REQ-HW-047 — Companion-Computer Expansion

The architecture should permit future communication with a companion computer.

**Verification:**  
Interface review.

---

## REQ-HW-048 — Custom PCB Migration

The Rev A hardware architecture shall permit migration to a custom Flight Controller PCB without fundamental redesign of the higher-level software architecture.

**Verification:**  
Architecture review.

---

## REQ-HW-049 — Test-Point Access

Critical development signals and power rails should remain accessible for measurement.

**Verification:**  
Hardware inspection.

---

# 10. Environmental and Reliability Requirements

## REQ-HW-050 — Vibration Environment

Hardware and connections shall remain functional under vibration produced by the Rev A propulsion system.

**Verification:**  
Integrated propulsion and flight testing.

---

## REQ-HW-051 — Operating Temperature

Hardware shall operate within the expected ambient and internally generated temperature range of Rev A testing.

**Verification:**  
Component-rating review and temperature measurement.

---

## REQ-HW-052 — Connector Retention

Flight connectors shall remain mated during expected vibration and handling.

**Verification:**  
Inspection and vibration testing.

---

## REQ-HW-053 — Replaceable Modules

Major Rev A electronic modules should be replaceable without replacement of the complete aircraft.

**Verification:**  
Serviceability demonstration.

---

# 11. Safety Requirements

## REQ-HW-054 — No Unintended Propulsion

Hardware behavior during reset, firmware programming, debugger attachment, and startup shall not intentionally command motor rotation.

**Verification:**  
Bench test without propellers.

---

## REQ-HW-055 — Polarity Protection Through Interface Design

Power connectors shall be polarized or otherwise designed to minimize accidental reverse connection.

**Verification:**  
Inspection.

---

## REQ-HW-056 — Insulated Battery Conductors

Battery-level conductors and terminals shall be insulated against unintended contact.

**Verification:**  
Inspection.

---

## REQ-HW-057 — Safe Bench-Power Compatibility

The hardware shall permit current-limited bench bring-up where practical.

**Verification:**  
Bench demonstration.

---

## REQ-HW-058 — Damaged Hardware Removal

Hardware showing heat damage, cracked insulation, swollen battery cells, exposed conductors, or damaged connectors shall not be used for flight.

**Verification:**  
Preflight inspection.

---

# 12. Verification Requirements

## REQ-HW-059 — Incremental Bring-Up

Hardware shall be verified incrementally in the following general order:

1. Visual inspection
2. Continuity and short-circuit checks
3. Regulated power validation
4. Flight Controller programming
5. Debug operation
6. GPIO
7. Communication interfaces
8. IMU communication
9. ESC signaling without propellers
10. Motor mapping and direction
11. Integrated propulsion
12. Flight testing

**Verification:**  
Bring-up record review.

---

## REQ-HW-060 — Hardware Configuration Record

The tested hardware configuration shall be recorded by revision.

**Verification:**  
Configuration-record inspection.

---

# 13. Requirement Summary

| Requirement Range | Area |
| --- | --- |
| REQ-HW-001 through REQ-HW-004 | Architecture |
| REQ-HW-005 through REQ-HW-015 | Flight Controller |
| REQ-HW-016 through REQ-HW-022 | Sensors |
| REQ-HW-023 through REQ-HW-032 | Propulsion |
| REQ-HW-033 through REQ-HW-041 | Power |
| REQ-HW-042 through REQ-HW-045 | Communications and debug |
| REQ-HW-046 through REQ-HW-049 | Expansion |
| REQ-HW-050 through REQ-HW-053 | Environment and reliability |
| REQ-HW-054 through REQ-HW-058 | Safety |
| REQ-HW-059 through REQ-HW-060 | Verification |

---

# 14. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Requirements Index
- **ARC-001** — Stratus System Architecture
- **BOM-001** — Bill of Materials
- **SES-001** — Mechanical Engineering Standard
- **SES-002** — Electrical Engineering Standard
- **HDR-001** through **HDR-007**
- **REQ-FR-001** through **REQ-FR-004**

---

# 15. Related Documents

## Upstream

- SPEC-001
- ARC-001
- REQ-001

## Peer

- REQ-SW-001 — Software Requirements
- REQ-ME-001 — Mechanical Requirements
- REQ-EL-001 — Electrical Requirements

## Downstream

- Hardware interface definitions
- Wiring diagrams
- Bring-up procedures
- Hardware verification records