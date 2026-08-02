# Stratus Rev A System Specification

**Document ID:** SPEC-001  
**Revision:** 1.1  
**Status:** Draft  
**Classification:** Public  
**Project:** Stratus  
**Author:** Austin Fellows  
**Created:** 2026-06-26  
**Last Updated:** 2026-08-02  

---

# Revision History

| Version | Date | Description | Author |
| --- | --- | --- | --- |
| 1.0 | 2026-06-26 | Initial revision | Austin Fellows |
| 1.1 | 2026-08-02 | Updated requirements, architecture, interface-control, traceability, standards, and decision-record references | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Mission
3. Scope
4. System Overview
5. Design Philosophy
6. High-Level Requirements
7. System Architecture
8. Hardware Configuration
9. Software Configuration
10. Interfaces
11. Performance Objectives
12. Revision Goals
13. Future Roadmap
14. Verification and Acceptance
15. References
16. Related Documents

---

# 1. Purpose

This document defines the system-level specification for **Stratus Rev A**, the initial hardware revision of the Stratus autonomous aerial robotics platform.

The purpose of this specification is to establish a single authoritative source describing the intended capabilities, architecture, operational objectives, and engineering boundaries of the system.

It serves as the governing reference for subsequent engineering activities, including:

- Requirements development
- System architecture
- Hardware selection
- Software development
- Mechanical design
- Electrical integration
- Interface definition
- System integration
- Verification
- Flight testing
- Future platform revisions

This specification intentionally avoids detailed implementation information.

Implementation-specific requirements, interfaces, decisions, and engineering practices are maintained in supporting documents, including:

- Requirements specifications
- System architecture documents
- Interface Control Documents
- Architecture Decision Records
- Hardware Decision Records
- Engineering standards
- Bills of materials
- Requirements traceability records
- Verification procedures and results

Unless superseded by a later revision, this document shall serve as the primary system-level engineering reference for Stratus Rev A.

---

# 2. Mission

The mission of the Stratus project is to design, develop, and validate a modular autonomous aerial robotics platform through first-principles engineering.

Stratus is intended to serve as a long-term engineering platform that enables the exploration and application of:

- Embedded systems
- Flight control
- Robotics
- Mechanical design
- Electronics
- Systems engineering
- Autonomous systems
- Verification and validation

The project prioritizes understanding and ownership of each subsystem over rapid integration of existing commercial flight-control solutions.

Revision A establishes the foundational architecture upon which future revisions will be built.

Its primary objective is to validate the core hardware and software architecture while establishing the engineering standards, documentation, interfaces, and development practices necessary to support increasingly capable autonomous aircraft.

The long-term vision of Stratus is to evolve into a fully autonomous and modular aerial robotics platform capable of supporting advanced sensing, navigation, mission planning, and future research initiatives without requiring fundamental architectural redesign.

---

# 3. Scope

This specification defines the capabilities, architecture, and engineering objectives of **Stratus Rev A**.

Revision A is intended to establish the foundational hardware, software, and systems-engineering practices that will support future platform evolution.

The primary focus of this revision is to validate the core architecture and engineering processes rather than maximize flight performance or operational capability.

## 3.1 Included Scope

The scope of Revision A includes:

- Development of a modular quadcopter platform
- Use of a custom-designed, primarily 3D-printable airframe
- Implementation of a custom embedded flight software stack
- Integration of an STM32H743-class Flight Controller
- Integration of a six-axis inertial measurement unit
- Implementation of state estimation
- Implementation of closed-loop attitude stabilization
- Implementation of four-channel motor-output control
- Integration of a four-motor brushless propulsion system
- Integration of a 4S battery and power system
- Development programming and debugging through SWD
- Development diagnostics through UART
- Establishment of telemetry and command-handling architecture
- Establishment of engineering requirements
- Establishment of engineering standards
- Establishment of architecture and hardware decision records
- Establishment of interface-control documentation
- Establishment of requirements traceability
- Demonstration of stable autonomous hover

## 3.2 Excluded Scope

The following capabilities are outside the required scope of Revision A:

- GPS-assisted navigation
- Position hold
- Waypoint navigation
- Computer vision
- Onboard environmental perception
- Autonomous mission planning
- Swarm coordination
- Cellular communication
- Satellite communication
- Long-range operational radio control
- Custom Flight Controller PCB
- Advanced payload integration
- Production certification
- Commercial deployment

## 3.3 Future Compatibility

Where practical, Revision A shall establish architectural and physical interfaces that allow future capabilities to be incorporated without requiring fundamental redesign of the core platform.

Potential future additions include:

- GNSS
- Magnetometer
- Barometer
- Optical flow
- Range sensing
- Operational radio
- Companion computer
- Camera
- Custom Flight Controller PCB
- Autonomous navigation
- Mission management

---

# 4. System Overview

Stratus Rev A is a modular autonomous quadcopter designed to serve as the foundational platform for the long-term Stratus engineering program.

The system integrates mechanical, electrical, electronic, and software subsystems into a cohesive architecture intended to support autonomous flight while remaining maintainable, extensible, testable, and reusable.

The platform is designed around a modular systems architecture in which individual subsystems may be independently developed, tested, replaced, and improved with limited impact on unrelated systems.

This design approach supports:

- Incremental development
- Controlled integration
- Simplified troubleshooting
- Component replacement
- Future subsystem upgrades
- Reuse across future revisions

At a high level, Stratus Rev A consists of the following major subsystems:

- Flight Controller
- Inertial Sensing
- State Estimation
- Flight Control
- Motor Output
- Propulsion
- Power Distribution
- Mechanical Structure
- Communications
- System Supervision
- Development and Debug Interfaces

These subsystems operate together to provide the capabilities required for:

- Sensor acquisition
- State estimation
- Flight stabilization
- Motor-command generation
- Fault handling
- Development diagnostics
- Future external command and telemetry

Detailed subsystem responsibilities and interactions are defined in **ARC-001**.

Exact controlled interfaces are defined in **ICD-001**.

---

# 5. Design Philosophy

The Stratus project is guided by engineering principles intended to promote maintainability, extensibility, technical understanding, and disciplined development.

## 5.1 First-Principles Engineering

Whenever practical, systems shall be designed and implemented from first principles rather than assembled entirely from existing integrated flight solutions.

Existing technologies may be studied and referenced; however, implementation ownership remains a primary project objective.

---

## 5.2 Modularity

Subsystems shall be designed as independent, well-defined modules with controlled interfaces.

Modularity shall support:

- Independent development
- Independent testing
- Replacement
- Upgrade
- Reuse
- Fault isolation
- Reduced coupling

---

## 5.3 Documentation-Driven Development

Engineering decisions should be documented before implementation whenever practical.

Specifications, requirements, architecture documents, interface definitions, standards, and decision records shall preserve design intent and support traceability.

---

## 5.4 Architecture Before Optimization

Architectural correctness, safety, maintainability, and extensibility shall take precedence over premature optimization.

Performance improvements should occur after the applicable architecture and behavior are understood and measured.

---

## 5.5 Progressive Complexity

Each hardware or software revision should introduce capabilities while minimizing unnecessary changes to validated subsystems.

New functionality should build upon established interfaces and architecture rather than replace them without justification.

---

## 5.6 Educational Value

Engineering decisions should maximize learning opportunities across:

- Embedded systems
- Robotics
- Control theory
- Electronics
- Mechanical engineering
- Systems engineering
- Software architecture
- Verification

When multiple technically acceptable solutions exist, educational value may be considered as a decision factor.

---

## 5.7 Standardization

Mechanical hardware, electrical interfaces, wiring, software architecture, documentation, and verification practices shall follow established project standards where practical.

Consistent standards reduce ambiguity, improve maintainability, and simplify future development.

---

## 5.8 Long-Term Platform Thinking

Stratus is intended to evolve through multiple revisions.

Design decisions should consider:

- Future compatibility
- Subsystem reuse
- Replaceability
- Interface stability
- Migration to custom electronics
- Long-term maintainability

---

## 5.9 Safe Incremental Integration

Hardware and software shall be integrated incrementally.

Initial tests shall use controlled and reduced-risk configurations, including:

- Current-limited power where practical
- Propellers removed during motor-output bring-up
- Explicit safe output states
- Independent subsystem testing
- Recorded verification results

---

# 6. High-Level Requirements

Detailed requirements for Stratus Rev A are defined in **REQ-001** and the supporting requirements documents.

This section provides a system-level summary.

## 6.1 Autonomous Flight

The system shall provide the foundational capabilities required to achieve stable autonomous hover through:

- Inertial sensing
- State estimation
- Closed-loop attitude stabilization
- Motor mixing
- Controlled motor output

---

## 6.2 Modular Architecture

The platform shall employ modular hardware, mechanical, electrical, and software architectures.

Subsystem replacement or improvement should not require unnecessary redesign of unrelated systems.

---

## 6.3 Embedded Flight Software

The aircraft shall use a custom-developed embedded flight software stack designed specifically for Stratus.

The software shall emphasize:

- Deterministic behavior
- Maintainability
- Modularity
- Portability
- Bounded resource use
- Testability
- Safe failure behavior

---

## 6.4 Sensor Integration

The system shall acquire and process inertial sensor measurements to support state estimation and closed-loop flight control.

The architecture shall permit future integration of additional sensors.

---

## 6.5 Propulsion and Power

The propulsion and power systems shall provide sufficient and repeatable operation to support Rev A integration and flight objectives.

Battery-connected equipment shall be compatible with the maximum voltage of the selected 4S battery.

---

## 6.6 Mechanical Design

The aircraft shall use a modular, repairable, and primarily additive-manufactured mechanical structure.

The structure shall support:

- Component retention
- Propeller clearance
- Wiring protection
- Sensor orientation
- Battery retention
- Serviceability
- Future expansion

---

## 6.7 Communications

The system shall provide development interfaces for:

- Firmware programming
- Debugging
- Diagnostics
- Telemetry
- Future command reception

Communication failures shall not directly produce uncontrolled propulsion behavior.

---

## 6.8 Interface Control

Electrical, software, mechanical, power, coordinate, debug, sensor, and motor-control interfaces shall be defined in **ICD-001**.

Unverified pin assignments or connector definitions shall not be treated as approved.

---

## 6.9 Engineering Documentation

Specifications, requirements, architecture documents, standards, decision records, interfaces, bills of materials, and verification evidence shall be maintained as project deliverables.

---

## 6.10 Traceability

Requirements shall be traceable to applicable architecture elements, decisions, implementation artifacts, verification methods, and evidence through **RTM-001**.

---

## 6.11 Future Expansion

The Rev A architecture shall support future capabilities where practical without requiring fundamental redesign.

---

# 7. System Architecture

The detailed Stratus Rev A system architecture is defined in:

- [ARC-001 — Stratus System Architecture](../design/ARC-001-System-Architecture.md)

Stratus Rev A is organized as a layered system composed of independent but interconnected subsystems.

Each subsystem performs a defined responsibility and exchanges information through controlled interfaces.

## 7.1 Flight Controller

Provides the primary embedded computing platform for:

- Peripheral management
- Sensor acquisition
- State estimation
- Flight control
- Motor output
- Communications
- System supervision
- Diagnostics

---

## 7.2 Inertial Sensing

Acquires angular-rate and acceleration measurements required for state estimation and stabilization.

---

## 7.3 State Estimation

Processes sensor measurements and produces a valid estimate of aircraft state for use by Flight Control.

---

## 7.4 Flight Control

Computes stabilization commands based on:

- Valid state estimates
- Desired flight setpoints
- Timing information
- Control limits

---

## 7.5 Motor Output

Converts control outputs into bounded, motor-specific commands while enforcing:

- Arming state
- Output limits
- Safe-state behavior
- Motor mapping
- Output validity

---

## 7.6 Propulsion

Converts electrical power and command signals into mechanical thrust through:

- Four motors
- Four ESC channels
- Four propellers

---

## 7.7 Power Distribution

Provides battery-level propulsion power and regulated power for electronics.

---

## 7.8 Mechanical Structure

Provides the structural framework for:

- Motors
- Propellers
- Battery
- ESC
- Flight Controller
- IMU
- Wiring
- Future payloads

---

## 7.9 Communications

Provides interfaces for:

- SWD
- USB
- Development UART
- Diagnostics
- Telemetry
- Commands
- Future radio integration

---

## 7.10 System Supervision

Coordinates:

- Startup state
- Arming
- Fault response
- Health monitoring
- Safe-state transitions

---

# 8. Hardware Configuration

The complete Rev A hardware configuration is maintained in:

- [BOM-001 — Stratus Rev A Bill of Materials](BOM.md)

Detailed hardware requirements are defined in:

- [REQ-HW-001 — Hardware Requirements](../requirements/hardware/HardwareRequirements.md)
- [REQ-EL-001 — Electrical Requirements](../requirements/electrical/ElectricalRequirements.md)
- [REQ-ME-001 — Mechanical Requirements](../requirements/mechanical/MechanicalRequirements.md)

Hardware-selection rationale is defined in the applicable ADRs and HDRs.

## 8.1 Flight Controller

Stratus Rev A shall use an STM32H743-class embedded processing platform.

The exact board, processor package, connector layout, and pin allocation shall be recorded in **ICD-001**.

**Reference:** ADR-001

---

## 8.2 Development Debugger

A NUCLEO-F401RE development board shall provide a genuine onboard ST-LINK/V2-1 debugger/programmer for external STM32H743 SWD development.

The NUCLEO-F401RE is development equipment and shall not be installed on the flight vehicle.

**Reference:** ADR-006

---

## 8.3 Inertial Sensing

An ICM-20602 six-axis inertial measurement unit shall provide:

- Three-axis angular-rate measurements
- Three-axis acceleration measurements

**Reference:** HDR-001

---

## 8.4 Propulsion

The Rev A propulsion system consists of:

- Four HappyModel EX1404 motors
- One Aero Selfie 45A four-in-one ESC
- Gemfan Hurricane 3520 propellers

**References:** HDR-002, HDR-003, HDR-004

---

## 8.5 Power System

The baseline power system uses:

- 4S lithium-polymer batteries
- Approximately 850 mAh baseline capacity
- XT30 battery connection
- Regulated electronics power

**Reference:** HDR-005

---

## 8.6 Mechanical Structure

The airframe consists primarily of modular additive-manufactured structural components assembled with standardized hardware.

**References:** ADR-002, ADR-003, HDR-006, SES-001

---

## 8.7 Electrical Infrastructure

Aircraft wiring shall use documented conductor sizes, connector practices, routing, strain relief, and workmanship standards.

**References:** HDR-007, SES-002

---

# 9. Software Configuration

Detailed software requirements and architecture are defined in:

- [REQ-SW-001 — Software Requirements](../requirements/software/SoftwareRequirements.md)
- [ARC-001 — Stratus System Architecture](../design/ARC-001-System-Architecture.md)

The Stratus flight software uses a layered embedded architecture that separates application behavior from device-specific and processor-specific implementation.

## 9.1 Platform Layer

Provides processor and board-specific support for:

- Startup
- Clocks
- GPIO
- Timers
- SPI
- UART
- USB
- DMA
- Timekeeping
- Reset behavior
- Watchdog support

---

## 9.2 Driver Layer

Provides interfaces for physical devices and transports, including:

- IMU
- ESC output
- UART
- USB
- Future radio or sensor hardware

---

## 9.3 Middleware and Services

Provides shared behavior such as:

- Scheduling
- Timing
- Communication framing
- Diagnostics
- Configuration
- Health monitoring

---

## 9.4 State Estimation

Produces aircraft-state estimates from validated sensor samples.

---

## 9.5 Flight Control

Produces control outputs from:

- State estimates
- Setpoints
- Timing data
- Configuration

---

## 9.6 Motor Output

Produces four bounded motor commands while enforcing safety constraints.

---

## 9.7 System Supervision

Controls:

- Startup
- Initialization
- Disarmed state
- Armed state
- Faulted state
- Safe-state behavior

---

## 9.8 Communications

Supports:

- Development diagnostics
- Telemetry
- Command validation
- Protocol handling
- Future transport independence

---

## 9.9 Future Navigation and Mission Management

Navigation and mission-management layers are architectural provisions and are not required Rev A operational capabilities.

---

# 10. Interfaces

The authoritative implementation-level interface definitions for Stratus Rev A are maintained in:

- [ICD-001 — Stratus Rev A Interface Control Document](../design/ICD-001-Interface-Control-Document.md)

The system architecture defines interface responsibilities.

The Interface Control Document defines exact interface details.

Engineering standards define implementation and workmanship practices.

## 10.1 Electrical Interfaces

Electrical interfaces include:

- Battery power
- Regulated electronics power
- Ground references
- IMU SPI
- IMU interrupt
- ESC command signals
- SWD
- UART
- USB
- Future expansion interfaces

Exact pins, peripherals, voltages, connectors, and safe states shall be recorded in **ICD-001**.

---

## 10.2 Mechanical Interfaces

Mechanical interfaces include:

- Flight Controller mounting
- ESC mounting
- IMU mounting
- Motor mounting
- Battery retention
- Wiring retention
- Future payload mounting

---

## 10.3 Software Interfaces

Software interfaces include:

- IMU samples
- State estimates
- Flight setpoints
- Control outputs
- Motor commands
- System health
- Telemetry data
- Received commands

Each software interface shall define:

- Producer
- Consumer
- Units
- Coordinate frame
- Validity
- Ownership
- Timing behavior

---

## 10.4 Development Interfaces

Development interfaces include:

- SWD programming and debugging
- USB programming or recovery
- Development UART
- Diagnostic output

---

## 10.5 External Operational Interfaces

Future operational interfaces may include:

- Command radio
- Telemetry radio
- Ground station
- GNSS
- Companion computer
- Payload interfaces

These interfaces are not considered operationally approved until defined and verified.

---

# 11. Performance Objectives

The primary objective of Stratus Rev A is to validate the platform architecture rather than maximize endurance, payload, speed, or maneuverability.

## 11.1 Stable Flight

The system shall demonstrate repeatable closed-loop autonomous hover through reliable:

- Sensor acquisition
- State estimation
- Flight stabilization
- Motor output

---

## 11.2 Reliable Operation

Primary subsystems shall operate predictably and repeatably under defined Rev A test conditions.

---

## 11.3 Modular Integration

Subsystems shall integrate through controlled interfaces that support independent development, maintenance, and replacement.

---

## 11.4 Maintainability

The platform shall support troubleshooting, repair, and component replacement through modular architecture and documentation.

---

## 11.5 Extensibility

The architecture shall support future hardware and software capabilities without fundamental redesign where practical.

---

## 11.6 Engineering Repeatability

The platform should be reproducible using the documented:

- Requirements
- Architecture
- Interfaces
- Standards
- Decision records
- BOM
- CAD
- Wiring
- Firmware
- Build procedures
- Verification records

---

## 11.7 Educational Objectives

The project shall provide practical experience in:

- Embedded systems
- Robotics
- Flight control
- Electronics
- Mechanical engineering
- Systems engineering
- Software architecture
- Verification and validation

---

# 12. Revision Goals

Revision A establishes the engineering foundation of Stratus.

## 12.1 Establish the Platform Architecture

Develop and validate a modular architecture that supports future platform evolution.

---

## 12.2 Validate Core Flight Capability

Demonstrate stable autonomous hover using custom:

- Sensor acquisition
- State estimation
- Flight control
- Motor-output software

---

## 12.3 Establish Engineering Standards

Define and apply standards for:

- Mechanical design
- Electrical wiring
- Documentation
- Future subsystem development

---

## 12.4 Develop the Initial Flight Software Stack

Implement the foundational embedded software required for Rev A operation and future expansion.

---

## 12.5 Validate the Hardware Platform

Demonstrate integrated operation of:

- Flight Controller
- IMU
- ESC
- Motors
- Propellers
- Battery
- Power regulation
- Mechanical structure
- Development interfaces

---

## 12.6 Establish Interface Control

Document and verify controlled interfaces through **ICD-001**.

---

## 12.7 Establish Requirements Traceability

Connect requirements to architecture, decisions, implementation, and verification through **RTM-001**.

---

## 12.8 Establish Engineering Documentation

Produce and maintain the required specifications, requirements, architecture documents, standards, decision records, and supporting documentation.

---

## 12.9 Enable Future Platform Evolution

Establish hardware, software, mechanical, electrical, and documentation practices that support future revisions.

---

# 13. Future Roadmap

The Stratus platform is intended to evolve through multiple revisions.

The roadmap is directional and may be modified through future engineering decisions.

## 13.1 Revision A — Foundation

Primary objectives:

- Modular airframe
- Custom embedded flight software
- Stable autonomous hover
- Engineering documentation
- Interface control
- Requirements traceability
- Architecture validation

---

## 13.2 Revision B — Platform Expansion

Potential objectives:

- Larger airframe
- Increased payload capacity
- Improved endurance
- Enhanced modularity
- Additional onboard sensing

---

## 13.3 Revision C — Custom Electronics

Potential objectives:

- Custom Flight Controller PCB
- Integrated power distribution
- Improved packaging
- Reduced mass
- Enhanced electrical reliability

---

## 13.4 Revision D — Autonomous Navigation

Potential objectives:

- Position estimation
- GNSS integration
- Waypoint navigation
- Return-to-home behavior
- Basic mission execution

---

## 13.5 Revision E — Advanced Perception

Potential objectives:

- Computer vision
- Obstacle detection
- Environmental perception
- Expanded sensor fusion

---

## 13.6 Revision F — Mission Autonomy

Potential objectives:

- Mission planning
- Autonomous decision-making
- Adaptive behavior
- Multi-objective mission execution

---

## 13.7 Long-Term Vision

The long-term objective is to establish a reusable autonomous aerial robotics platform supporting continued research and engineering development.

Future revisions should preserve validated interfaces and architectural principles where practical.

---

# 14. Verification and Acceptance

Rev A shall not be considered complete solely because the aircraft hardware has been assembled.

Acceptance shall require documented evidence demonstrating compliance with the applicable Rev A requirements.

## 14.1 Verification Sources

Verification planning and status shall be maintained in:

- [RTM-001 — Requirements Traceability Matrix](../requirements/RequirementsTraceabilityMatrix.md)

Evidence may include:

- Inspection records
- Engineering analyses
- Demonstrations
- Unit-test results
- Bench-test records
- Integration-test records
- Logic-analyzer captures
- Oscilloscope captures
- Build logs
- Flight-test records
- Flight logs

---

## 14.2 Minimum Rev A Acceptance Objectives

At minimum, Rev A acceptance should demonstrate:

- Flight Controller programming and debugging
- Safe startup behavior
- IMU communication
- Valid sensor measurements
- State-estimation operation
- Motor-output generation
- Correct motor mapping
- Correct motor directions
- Electrical power stability
- Communication diagnostics
- Fault detection
- Arming restrictions
- Stable controlled hover
- Recorded configuration and test evidence

---

## 14.3 Configuration Control

Verification results shall identify the tested:

- Hardware configuration
- Firmware revision
- Mechanical revision
- Wiring configuration
- Battery
- Propellers
- Test conditions

---

# 15. References

## 15.1 Authoritative Project Documents

- [SPEC-001 — Stratus Rev A System Specification](SPEC-001-Stratus-RevA.md)
- [REQ-001 — Stratus Rev A Requirements Specification](../requirements/REQ-001.md)
- [ARC-001 — Stratus System Architecture](../design/ARC-001-System-Architecture.md)
- [ICD-001 — Stratus Rev A Interface Control Document](../design/ICD-001-Interface-Control-Document.md)
- [BOM-001 — Stratus Rev A Bill of Materials](BOM.md)
- [RTM-001 — Requirements Traceability Matrix](../requirements/RequirementsTraceabilityMatrix.md)
- [INDEX-001 — Stratus Engineering Documentation Index](../INDEX-001-Engineering-Documentation-Index.md)

---

## 15.2 Functional Requirements

- [REQ-FR-001 — Flight Control](../requirements/flight-functions/FlightControl.md)
- [REQ-FR-002 — State Estimation](../requirements/flight-functions/StateEstimation.md)
- [REQ-FR-003 — Motor Output](../requirements/flight-functions/MotorOutput.md)
- [REQ-FR-004 — Communications](../requirements/flight-functions/Communications.md)

---

## 15.3 Engineering-Domain Requirements

- [REQ-HW-001 — Hardware Requirements](../requirements/hardware/HardwareRequirements.md)
- [REQ-SW-001 — Software Requirements](../requirements/software/SoftwareRequirements.md)
- [REQ-ME-001 — Mechanical Requirements](../requirements/mechanical/MechanicalRequirements.md)
- [REQ-EL-001 — Electrical Requirements](../requirements/electrical/ElectricalRequirements.md)

---

## 15.4 Engineering Standards

- [SES-001 — Mechanical Engineering Standard](../standards/SES-001-Hardware.md)
- [SES-002 — Electrical Engineering Standard](../standards/SES-002-Wiring.md)

---

## 15.5 Architecture Decision Records

- [ADR-001 — STM32H743 Architecture](../decisions/adr/ADR-001-STM32H743-Architecture.md)
- [ADR-002 — Rev A Platform Size](../decisions/adr/ADR-002-RevA-Platform-Size.md)
- [ADR-003 — Modular Airframe Architecture](../decisions/adr/ADR-003-Modular-Airframe-Architecture.md)
- [ADR-004 — Custom Flight Software](../decisions/adr/ADR-004-Custom-Flight-Software.md)
- [ADR-005 — Flight Stack Strategy](../decisions/adr/ADR-005-Flight-Stack-Strategy.md)
- [ADR-006 — NUCLEO-F401RE Development Debugger](../decisions/adr/ADR-006-NUCLEO-F401RE-Debugger.md)

---

## 15.6 Hardware Decision Records

- [HDR-001 — ICM-20602 IMU](../decisions/hdr/HDR-001-ICM20602-IMU.md)
- [HDR-002 — HappyModel EX1404 Motors](../decisions/hdr/HDR-002-HappyModel-EX1404-Motors.md)
- [HDR-003 — Aero Selfie 45A ESC](../decisions/hdr/HDR-003-AeroSelfie-45A-ESC.md)
- [HDR-004 — Gemfan Hurricane 3520 Propellers](../decisions/hdr/HDR-004-Gemfan-Hurricane-3520-Props.md)
- [HDR-005 — 4S 850 mAh Power System](../decisions/hdr/HDR-005-4S-850mAh-Power-System.md)
- [HDR-006 — Mechanical Hardware Standard](../decisions/hdr/HDR-006-Mechanical-Hardware-Standard.md)
- [HDR-007 — Wiring Materials Standard](../decisions/hdr/HDR-007-Wiring-Materials-Standard.md)

---

# 16. Related Documents

## Upstream

- Project README
- Project vision and philosophy

## Peer

- REQ-001
- ARC-001
- ICD-001
- BOM-001
- RTM-001
- INDEX-001

## Supporting

- REQ-FR Series
- REQ-HW-001
- REQ-SW-001
- REQ-ME-001
- REQ-EL-001
- SES Series
- ADR Series
- HDR Series

## Downstream

- Firmware source code
- CAD models
- Wiring diagrams
- Harness definitions
- Bring-up procedures
- Verification procedures
- Integration-test records
- Flight-test records
- Flight logs