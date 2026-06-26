# Stratus Rev A System Specification

Document ID: SPEC-001

Revision: 1.0

Status: Draft

Classification: Public

Project: Stratus

Author: Austin Fellows

Created: 2026-06-26

Last Updated: 2026-06-26

---

# Revision History

| Version | Date | Description | Author |
|----------|------------|--------------------------|----------------|
| 1.0 | 2026-06-26 | Initial revision | Austin Fellows |

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Systems Engineer | Austin Fellows | Approved |

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
14. References

## 1. Purpose

This document defines the system-level specification for **Stratus Rev A**, the initial hardware revision of the Stratus autonomous aerial robotics platform.

The purpose of this specification is to establish a single authoritative source describing the intended capabilities, architecture, operational objectives, and engineering boundaries of the system. It serves as the governing reference for all subsequent engineering activities, including hardware design, software development, system integration, testing, and future platform revisions.

This specification intentionally avoids detailed implementation information. Implementation-specific decisions are maintained within supporting engineering documentation, including Architecture Decision Records (ADRs), Hardware Decision Records (HDRs), Engineering Standards (SES), Requirements Specifications (REQ), Architecture Documents (ARC), and the Bill of Materials (BOM).

Unless superseded by a later revision, this document shall serve as the primary engineering reference for Stratus Rev A.

## 2. Mission

The mission of the Stratus project is to design, develop, and validate a modular autonomous aerial robotics platform through first-principles engineering.

Stratus is intended to serve as a long-term engineering platform that enables the exploration and application of embedded systems, flight control, robotics, mechanical design, electronics, and systems engineering. The project prioritizes understanding and ownership of each subsystem over rapid integration of existing commercial solutions.

Revision A establishes the foundational architecture upon which future revisions will be built. Its primary objective is to validate the core hardware and software architecture while establishing the engineering standards, documentation, and development practices necessary to support increasingly capable autonomous aircraft.

The long-term vision of Stratus is to evolve into a fully autonomous, modular aerial robotics platform capable of supporting advanced sensing, navigation, mission planning, and future research initiatives without requiring fundamental architectural redesign.

## 3. Scope

This specification defines the capabilities, architecture, and engineering objectives of **Stratus Rev A**, the initial hardware revision of the Stratus autonomous aerial robotics platform.

Revision A is intended to establish the foundational hardware, software, and systems engineering practices that will support future platform evolution. The primary focus of this revision is to validate the core architecture and engineering processes rather than maximize flight performance or operational capability.

The scope of Revision A includes:

- Development of a modular quadcopter platform utilizing a custom-designed, 3D-printable airframe.
- Implementation of a custom embedded flight software stack developed from first principles.
- Validation of the selected electronics architecture, propulsion system, and power system.
- Establishment of engineering documentation, standards, and decision records to support future revisions.
- Demonstration of stable autonomous hover through closed-loop attitude stabilization.

The following capabilities are considered outside the scope of Revision A and are planned for future revisions:

- GPS-assisted navigation
- Computer vision and onboard perception
- Autonomous mission planning
- Swarm coordination
- Custom flight controller PCB
- Advanced payload integration

Where practical, Revision A shall establish architectural interfaces that allow these capabilities to be incorporated into future revisions without requiring significant redesign of the core platform.

## 4. System Overview

Stratus Rev A is a modular autonomous quadcopter designed to serve as the foundational platform for the long-term Stratus engineering program. The system integrates mechanical, electrical, and software subsystems into a cohesive architecture intended to support autonomous flight while remaining highly maintainable, extensible, and reusable.

The platform is designed around a modular systems architecture in which individual subsystems may be independently developed, tested, and replaced with minimal impact to the overall system. This design philosophy enables rapid iteration, simplifies maintenance, and supports the progressive expansion of platform capabilities throughout future revisions.

At a high level, Stratus Rev A consists of the following major subsystems:

- Flight Control
- Inertial Sensing
- Propulsion
- Power Distribution
- Mechanical Structure
- Communications
- Software

These subsystems operate together to provide the fundamental capabilities required for autonomous flight, including sensor acquisition, state estimation, flight stabilization, motor control, and future autonomous navigation.

Detailed subsystem architectures, interfaces, and implementation details are documented separately within the project architecture documentation (ARC series) and supporting engineering standards (SES series).

## 5. Design Philosophy

The Stratus project is guided by a set of engineering principles intended to promote long-term maintainability, extensibility, and technical understanding. These principles serve as the foundation for architectural, hardware, and software decisions throughout the lifecycle of the project.

### First-Principles Engineering

Whenever practical, systems shall be designed and implemented from first principles rather than assembled from existing integrated solutions. Existing technologies may be studied and referenced; however, implementation ownership remains a primary project objective.

### Modularity

Subsystems shall be designed as independent, well-defined modules with standardized interfaces. This approach minimizes coupling between systems, simplifies maintenance, and supports incremental hardware and software evolution.

### Documentation-Driven Development

Engineering decisions shall be documented before implementation whenever practical. Decision Records, Engineering Standards, Specifications, and Requirements establish a permanent record of design intent and provide traceability throughout the project lifecycle.

### Architecture Before Optimization

Architectural correctness, maintainability, and extensibility shall take precedence over premature optimization. Performance improvements should occur only after a robust and well-understood system architecture has been established.

### Progressive Complexity

Each hardware revision should introduce new capabilities while minimizing unnecessary changes to validated subsystems. New functionality should build upon existing architecture rather than replace it.

### Educational Value

Engineering decisions should maximize learning opportunities across embedded systems, robotics, control theory, electronics, mechanical design, and systems engineering. When multiple technically acceptable solutions exist, preference may be given to the option that provides greater educational benefit.

### Standardization

Mechanical hardware, electrical interfaces, software architecture, and engineering documentation shall follow established project standards whenever practical. Consistent standards improve maintainability, reduce complexity, and simplify future development.

### Long-Term Platform Thinking

Stratus is intended to evolve through multiple hardware revisions over an extended period. Design decisions should therefore consider future compatibility, subsystem reuse, and long-term maintainability rather than focusing solely on the requirements of the current revision.

## 6. High-Level Requirements

The detailed functional and non-functional requirements for Stratus Rev A are documented in **REQ-001**. This section provides a high-level summary of the system capabilities established by those requirements.

### Autonomous Flight

The system shall provide the foundational capabilities necessary to achieve stable autonomous flight through closed-loop attitude stabilization and real-time control.

### Modular Architecture

The platform shall employ a modular hardware and software architecture that supports independent subsystem development, replacement, and future expansion with minimal impact to existing systems.

### Embedded Flight Software

The aircraft shall utilize a custom-developed embedded flight software stack designed specifically for the Stratus platform. The software architecture shall emphasize maintainability, portability, and long-term extensibility.

### Sensor Integration

The system shall acquire and process inertial sensor data to support state estimation and closed-loop flight control. The architecture shall permit integration of additional sensors in future revisions.

### Propulsion and Power

The propulsion and power subsystems shall provide reliable and repeatable operation sufficient to support autonomous flight while maintaining compatibility with future platform growth.

### Mechanical Design

The aircraft shall utilize a modular, repairable, and primarily 3D-printable mechanical structure designed for rapid iteration, ease of maintenance, and standardized assembly practices.

### Engineering Documentation

Engineering artifacts, including specifications, requirements, standards, decision records, and bills of materials, shall be maintained as first-class project deliverables throughout the lifecycle of the platform.

### Future Expansion

The architecture established by Revision A shall support future capabilities including autonomous navigation, advanced sensing, custom electronics, and expanded mission functionality without requiring fundamental redesign of the platform.

## 7. System Architecture

The detailed system architecture for Stratus Rev A is documented in **ARC-001**. This section provides a high-level overview of the primary subsystems and their interactions.

Stratus Rev A is organized as a layered system composed of independent yet interconnected subsystems. Each subsystem performs a well-defined responsibility while communicating through standardized interfaces to minimize coupling and simplify future development.

The primary system subsystems are:

### Flight Control

Responsible for coordinating aircraft operation by processing sensor information, executing flight control algorithms, and issuing propulsion commands.

### Inertial Sensing

Responsible for acquiring inertial measurement data required for state estimation and flight stabilization.

### Propulsion

Responsible for converting flight control commands into mechanical thrust through coordinated motor control.

### Power Distribution

Responsible for supplying electrical power to all onboard subsystems while maintaining reliable operation throughout the flight envelope.

### Mechanical Structure

Provides the structural framework supporting all onboard systems while enabling modular assembly, maintenance, and future hardware expansion.

### Communications

Provides interfaces for firmware development, debugging, telemetry, future command and control, and system monitoring.

### Software

Implements the layered embedded software architecture responsible for hardware abstraction, device drivers, state estimation, flight control, navigation, and future mission management.

These subsystems communicate through standardized electrical, mechanical, and software interfaces to provide a modular architecture that supports incremental capability growth while minimizing redesign between platform revisions.

Implementation details, subsystem interactions, interface definitions, and architectural diagrams are documented separately within **ARC-001**.

## 8. Hardware Configuration

The complete hardware configuration for Stratus Rev A is maintained within **BOM-001**. Individual hardware selection rationale is documented within the corresponding Hardware Decision Records (HDRs).

The Rev A hardware configuration consists of the following primary subsystems:

### Flight Controller

An ARM Cortex-M based embedded processing platform provides centralized control of all onboard flight systems, including sensor acquisition, state estimation, control algorithms, communications, and propulsion management.

*Reference: ADR-001*

### Inertial Sensing

A six-axis inertial measurement unit provides real-time gyroscope and accelerometer measurements required for attitude estimation and closed-loop flight stabilization.

*Reference: HDR-001*

### Propulsion

A four-motor brushless propulsion system provides thrust generation and attitude control for the aircraft. Electronic speed controllers convert flight control commands into motor actuation while maintaining reliable operation throughout the expected flight envelope.

*References: HDR-002, HDR-003, HDR-004*

### Power System

A rechargeable lithium-polymer battery supplies electrical power to all onboard subsystems through a standardized power distribution architecture designed to support future platform expansion.

*Reference: HDR-005*

### Mechanical Structure

The airframe consists primarily of modular, additive-manufactured structural components assembled using standardized mechanical hardware. The structure is designed to support rapid iteration, simplified maintenance, and future subsystem replacement.

*Reference: HDR-006*

### Electrical Infrastructure

The aircraft utilizes standardized wiring materials, conductor sizes, connector conventions, and routing practices to improve reliability, maintainability, and manufacturing consistency.

*Reference: HDR-007*

The hardware architecture has been selected to maximize modularity, simplify future revisions, and support migration toward increasingly capable autonomous aircraft without requiring significant redesign of the core platform.

## 9. Software Configuration

The detailed software architecture for Stratus Rev A is documented in **ARC-001**. This section provides a high-level overview of the software subsystems and their responsibilities.

The Stratus software stack is designed as a layered embedded architecture that separates hardware-specific functionality from flight algorithms and future autonomous capabilities. Each layer performs a well-defined responsibility while exposing standardized interfaces to adjacent layers.

The primary software layers consist of:

### Hardware Abstraction

Provides a hardware-independent interface to the underlying microcontroller peripherals, enabling future hardware revisions with minimal impact to higher software layers.

### Device Drivers

Implements communication with onboard sensors, propulsion hardware, communication interfaces, and future peripheral devices.

### State Estimation

Processes sensor data to estimate the aircraft's orientation and future vehicle state required for closed-loop flight control.

### Flight Control

Executes the control algorithms responsible for aircraft stabilization, attitude regulation, and motor command generation.

### Navigation

Provides the framework for future position estimation, waypoint navigation, and autonomous guidance capabilities.

### Mission Management

Coordinates high-level autonomous behaviors and future mission execution while interfacing with lower-level navigation and flight control systems.

### Communications

Provides interfaces for firmware updates, debugging, telemetry, and future command-and-control functionality.

The software architecture emphasizes modularity, maintainability, portability, and long-term extensibility. Higher software layers are intentionally isolated from hardware-specific implementation details to simplify future hardware revisions and subsystem expansion.

Implementation details, software interfaces, task organization, and subsystem interactions are documented within **ARC-001**.

## 10. Interfaces

The detailed interface definitions for Stratus Rev A are documented within **ARC-001** and the applicable Engineering Standards (SES). This section provides a high-level overview of the interfaces that enable communication between system subsystems and external development tools.

### Internal Interfaces

The internal architecture utilizes standardized electrical, mechanical, and software interfaces to promote subsystem independence and simplify future hardware revisions.

Primary internal interface categories include:

#### Electrical Interfaces

Provide communication and power distribution between onboard electronics through standardized communication protocols and power connections.

#### Mechanical Interfaces

Provide standardized mounting locations, fastening methods, and module attachment points that support the modular airframe architecture.

#### Software Interfaces

Provide well-defined interfaces between software layers and subsystems while minimizing coupling and promoting long-term maintainability.

---

### External Interfaces

External interfaces provide mechanisms for development, debugging, configuration, and future operational communication.

Primary external interface categories include:

#### Development Interface

Supports firmware programming, debugging, and system configuration during development and validation activities.

#### Telemetry Interface

Provides the framework for future transmission of system status, health information, and operational telemetry.

#### Command and Control Interface

Provides the architectural foundation for future command input, mission updates, and autonomous operation.

---

Detailed interface specifications, communication protocols, connector definitions, and subsystem interactions are maintained within **ARC-001** and the applicable Engineering Standards (SES series).

## 11. Performance Objectives

The primary objective of Stratus Rev A is to validate the foundational architecture of the platform rather than maximize operational performance. Success is measured by the reliability, maintainability, and extensibility of the overall system rather than by flight endurance or maneuverability.

The following performance objectives define the intended outcomes of Revision A:

### Stable Flight

The platform shall demonstrate repeatable, closed-loop autonomous hover through reliable attitude estimation and flight stabilization.

### Reliable Operation

All primary subsystems shall operate together in a predictable and repeatable manner under normal operating conditions.

### Modular Integration

Subsystems shall integrate through standardized interfaces that support independent development, maintenance, and replacement with minimal impact to the overall system.

### Maintainability

The platform shall support efficient troubleshooting, repair, and subsystem replacement through modular mechanical, electrical, and software architectures.

### Extensibility

The established architecture shall support future hardware and software capabilities without requiring fundamental redesign of validated subsystems.

### Engineering Repeatability

The platform shall be fully reproducible using the documented engineering processes, specifications, standards, decision records, and bill of materials maintained within the project repository.

### Educational Objectives

The platform shall maximize opportunities for developing expertise in embedded systems, robotics, flight control, electronics, mechanical engineering, and systems engineering through implementation ownership and first-principles engineering.

## 12. Revision Goals

Revision A establishes the engineering foundation of the Stratus platform. While future revisions will introduce additional capabilities and increasingly sophisticated hardware, the primary objective of Revision A is to validate the project's architecture, engineering methodology, and development processes.

The goals of Revision A are as follows:

### Establish the Platform Architecture

Develop and validate a modular system architecture that supports long-term platform evolution while minimizing redesign between future revisions.

### Validate Core Flight Capability

Demonstrate stable autonomous hover through implementation of custom embedded flight software, state estimation, and closed-loop flight control.

### Establish Engineering Standards

Define and document engineering standards governing mechanical hardware, electrical wiring, documentation, and future subsystem development.

### Develop the Initial Flight Software Stack

Implement the foundational embedded software architecture required to support future navigation, mission management, and autonomous capabilities.

### Validate the Hardware Platform

Demonstrate reliable operation of the selected Flight Control, Inertial Sensing, Propulsion, Power Distribution, Mechanical Structure, and Communications subsystems as an integrated system.

### Establish Engineering Documentation

Produce a complete set of engineering specifications, requirements, architecture documents, standards, decision records, and supporting documentation that accurately describe the platform and support future development.

### Enable Future Platform Evolution

Establish hardware, software, and documentation practices that enable future revisions to expand platform capability without requiring fundamental architectural redesign.

## 13. Future Roadmap

The Stratus platform is intended to evolve through multiple hardware revisions, with each revision introducing new capabilities while preserving the architectural foundation established by previous work.

The roadmap presented below reflects the current engineering vision for the platform and is intended to guide long-term development. Future revisions may be adjusted as project objectives evolve.

### Revision A Foundation

Establish the core hardware and software architecture required for autonomous flight.

Primary objectives include:

- Modular airframe
- Custom embedded flight software
- Stable autonomous hover
- Engineering documentation
- Engineering standards
- System architecture validation

---

### Revision B Platform Expansion

Expand the physical capabilities of the platform while preserving the validated architecture developed during Revision A.

Potential objectives include:

- Larger airframe
- Increased payload capacity
- Improved flight endurance
- Enhanced modularity
- Additional onboard sensing

---

### Revision C Custom Electronics

Transition from development hardware to custom-designed electronics while maintaining software compatibility.

Potential objectives include:

- Custom flight controller PCB
- Integrated power distribution
- Improved packaging
- Reduced system weight
- Enhanced electrical reliability

---

### Revision D Autonomous Navigation

Introduce autonomous navigation capabilities beyond attitude stabilization.

Potential objectives include:

- Position estimation
- GPS integration
- Waypoint navigation
- Return-to-home functionality
- Basic mission execution

---

### Revision E Advanced Perception

Expand environmental awareness through additional sensing technologies.

Potential objectives include:

- Computer vision
- Obstacle detection
- Sensor fusion enhancements
- Environmental perception

---

### Revision F Mission Autonomy

Develop higher-level autonomous behaviors capable of executing increasingly complex missions.

Potential objectives include:

- Mission planning
- Autonomous decision making
- Adaptive behaviors
- Multi-objective mission execution

---

### Long-Term Vision

The long-term objective of the Stratus project is to establish a flexible autonomous aerial robotics platform capable of supporting ongoing research, experimentation, and engineering development across embedded systems, robotics, control theory, electronics, and autonomous systems.

Future revisions should continue to prioritize modularity, maintainability, engineering rigor, and first-principles development while preserving compatibility with established project standards wherever practical.

## 14. References

The following documents comprise the engineering documentation package for the Stratus project. Unless otherwise noted, the latest approved revision of each document shall be considered applicable.

### Authoritative Documents

These documents define the system requirements, architecture, and engineering intent of the Stratus platform.

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — System Requirements
- **ARC-001** — System Architecture
- **BOM-001** — Bill of Materials

---

### Engineering Standards

These documents establish engineering standards governing hardware, electrical systems, documentation, and future development practices.

- **SES-001** — Mechanical Hardware Standard
- **SES-002** — Wiring Standard

---

### Architecture Decision Records (ADR)

These documents capture significant architectural decisions made throughout the development of the Stratus platform.

- **ADR-001** — STM32H743 Architecture
- **ADR-002** — Rev A Platform Size
- **ADR-003** — Modular Airframe Architecture
- **ADR-004** — Custom Flight Software
- **ADR-005** — Flight Stack Strategy

---

### Hardware Decision Records (HDR)

These documents capture significant hardware selection decisions and their associated engineering rationale.

- **HDR-001** — ICM-20602 IMU
- **HDR-002** — HappyModel EX1404 Motors
- **HDR-003** — Aero Selfie 45A 4-in-1 ESC
- **HDR-004** — Gemfan Hurricane 3520 Propellers
- **HDR-005** — 4S 850mAh Power System
- **HDR-006** — Mechanical Hardware Standard
- **HDR-007** — Wiring Materials Standard

---

### Project Documentation

Additional documentation supporting future engineering activities may include:

- Flight Test Logs
- Build Logs
- CAD Models
- PCB Design Files
- Firmware Documentation
- Simulation Results
- Verification and Validation Documentation
