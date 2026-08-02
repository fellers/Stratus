# Stratus Rev A Requirements Traceability Matrix

**Document ID:** RTM-001  
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
| 1.0 | 2026-08-02 | Initial Rev A requirements traceability baseline | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Traceability Model
4. Status Definitions
5. Verification Methods
6. Document-Level Traceability
7. Functional Requirements Traceability
8. Hardware Requirements Traceability
9. Software Requirements Traceability
10. Mechanical Requirements Traceability
11. Electrical Requirements Traceability
12. Documentation Requirements Traceability
13. Decision-Record Traceability
14. Verification Artifact Register
15. Open Traceability Actions
16. Baseline Completion Criteria
17. References
18. Related Documents

---

# 1. Purpose

This document provides bidirectional traceability for the Stratus Rev A engineering baseline.

The Requirements Traceability Matrix connects:

- System objectives
- System architecture
- Functional requirements
- Hardware requirements
- Software requirements
- Mechanical requirements
- Electrical requirements
- Engineering standards
- Architecture Decision Records
- Hardware Decision Records
- Implementation artifacts
- Verification procedures
- Verification evidence

The matrix is intended to demonstrate that each applicable requirement has an identifiable origin, implementation destination, and verification method.

---

# 2. Scope

This matrix applies to Stratus Rev A.

It covers the requirements defined by:

- **REQ-001** — Stratus Rev A Requirements Specification
- **REQ-FR-001** — Flight Control Functional Requirements
- **REQ-FR-002** — State Estimation Functional Requirements
- **REQ-FR-003** — Motor Output Functional Requirements
- **REQ-FR-004** — Communications Functional Requirements
- **REQ-HW-001** — Hardware Requirements
- **REQ-SW-001** — Software Requirements
- **REQ-ME-001** — Mechanical Requirements
- **REQ-EL-001** — Electrical Requirements
- Documentation requirements defined within **REQ-001**

This revision establishes traceability at the requirement-family and requirement-range level.

Individual requirement rows shall be added as implementation and verification artifacts are created.

---

# 3. Traceability Model

The intended traceability flow is:

```text
Project Vision and Objectives
            ↓
         SPEC-001
            ↓
         REQ-001
            ↓
Subsystem Requirements
            ↓
         ARC-001
            ↓
     ADR / HDR / SES
            ↓
Implementation Artifacts
            ↓
Verification Procedures
            ↓
Verification Evidence
```

## 3.1 Upstream Traceability

Upstream traceability identifies why a requirement exists.

Typical upstream sources include:

- SPEC-001
- REQ-001
- ARC-001
- Safety constraints
- Approved ADRs
- Approved HDRs
- Engineering standards

## 3.2 Downstream Traceability

Downstream traceability identifies where a requirement is implemented and verified.

Typical downstream artifacts include:

- Firmware source modules
- Board-interface definitions
- Wiring diagrams
- CAD models
- Manufacturing files
- Assembly procedures
- Bench-test procedures
- Integration-test procedures
- Flight-test procedures
- Test records

## 3.3 Traceability Rule

A requirement shall not be marked **Verified** unless objective evidence is identified in this matrix or an associated verification record.

---

# 4. Status Definitions

| Status | Meaning |
| --- | --- |
| Draft | Requirement or trace link is still being developed |
| Defined | Requirement exists and has an identified owner |
| Allocated | Requirement has been assigned to architecture or implementation |
| Implemented | An implementation artifact exists |
| Verification Planned | A verification method or procedure has been identified |
| Verified | Objective evidence demonstrates compliance |
| Failed | Verification demonstrated noncompliance |
| Deferred | Requirement is intentionally postponed |
| Not Applicable | Requirement does not apply to the tested configuration |
| Superseded | Requirement or trace link has been replaced |

---

# 5. Verification Methods

| Code | Method | Description |
| --- | --- | --- |
| I | Inspection | Examination of hardware, software, documentation, configuration, or workmanship |
| A | Analysis | Mathematical, logical, electrical, structural, timing, or engineering evaluation |
| D | Demonstration | Observation of required behavior without extensive instrumentation |
| T | Test | Controlled and repeatable execution with measured acceptance criteria |

Multiple methods may apply to one requirement.

---

# 6. Document-Level Traceability

| Requirement Document | Upstream Source | Architecture Allocation | Governing Standards or Decisions | Primary Verification | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-FR-001 — Flight Control | SPEC-001, REQ-001 | ARC-001 Flight Control subsystem | ADR-004, ADR-005 | Analysis, simulation, bench test, flight test | Defined |
| REQ-FR-002 — State Estimation | SPEC-001, REQ-001 | ARC-001 State Estimation subsystem | ADR-001, HDR-001 | Unit test, sensor replay, bench test, flight test | Defined |
| REQ-FR-003 — Motor Output | SPEC-001, REQ-001 | ARC-001 Motor Output subsystem | HDR-002, HDR-003, HDR-004 | Logic-analyzer test, motor bench test | Defined |
| REQ-FR-004 — Communications | SPEC-001, REQ-001 | ARC-001 Communications subsystem | ADR-004, ADR-005, SES-002 | Unit test, parser test, UART/SWD demonstration | Defined |
| REQ-HW-001 — Hardware | SPEC-001, REQ-001 | ARC-001 Hardware Architecture | HDR-001 through HDR-007 | Inspection, analysis, bring-up test | Defined |
| REQ-SW-001 — Software | SPEC-001, REQ-001 | ARC-001 Software Architecture | ADR-004, ADR-005 | Code inspection, unit test, timing test | Defined |
| REQ-ME-001 — Mechanical | SPEC-001, REQ-001 | ARC-001 Mechanical Structure | ADR-002, ADR-003, SES-001 | CAD inspection, dimensional test, assembly test | Defined |
| REQ-EL-001 — Electrical | SPEC-001, REQ-001 | ARC-001 Power and Electrical Architecture | HDR-003, HDR-005, HDR-007, SES-002 | Inspection, continuity test, voltage test | Defined |
| REQ-DOC-001 through REQ-DOC-008 | REQ-001 | Documentation architecture | INDEX-001 and repository conventions | Documentation and link inspection | Defined |

---

# 7. Functional Requirements Traceability

## 7.1 Flight Control

| Requirement Source | Architectural Allocation | Inputs | Outputs | Expected Implementation | Verification | Status |
| --- | --- | --- | --- | --- | --- | --- |
| REQ-FR-001 | ARC-001 Flight Control | AttitudeEstimate, FlightSetpoint, timing data | ControlOutput | Flight-control application module | Host simulation, unit test, bench test, flight test | Defined |
| Flight-control initialization requirements | ARC-001 Boot Sequence | Configuration and estimator state | Initialized controller state | Controller initialization module | Unit test and startup demonstration | Verification Planned |
| Closed-loop stabilization requirements | ARC-001 Flight Control | Estimated attitude and desired state | Axis corrections | Attitude or rate controller | Simulation and controlled test | Verification Planned |
| Control-limit requirements | ARC-001 Fault Handling | Controller state and limits | Bounded control output | Saturation and anti-windup logic | Boundary-value test | Verification Planned |
| Invalid-state handling requirements | ARC-001 Safe State | Invalid estimate or numeric input | Rejected or safe output | Controller validation logic | Fault injection | Verification Planned |

**Expansion required:** Add one row for every individual `REQ-FC-*` statement after `FlightControl.md` is audited.

---

## 7.2 State Estimation

| Requirement Source | Architectural Allocation | Inputs | Outputs | Expected Implementation | Verification | Status |
| --- | --- | --- | --- | --- | --- | --- |
| REQ-FR-002 | ARC-001 State Estimation | Validated ImuSample and timestamp | AttitudeEstimate and validity | State-estimation application module | Host test, replay test, bench test | Defined |
| Sensor-conversion requirements | ARC-001 Sensor Acquisition | Raw accelerometer and gyroscope data | Scaled physical measurements | IMU driver and acquisition service | Known-value unit test | Verification Planned |
| Calibration requirements | ARC-001 State Estimation | Raw or scaled sensor values | Corrected measurements | Calibration module | Static sensor test | Verification Planned |
| Orientation requirements | ARC-001 Coordinate conventions | Sensor-frame measurements | Aircraft-frame measurements | Coordinate-transform module | Axis-orientation test | Verification Planned |
| Estimator-validity requirements | ARC-001 System Supervision | Estimate health and timing | Validity and fault state | Estimator health logic | Stale-data and invalid-data injection | Verification Planned |

**Expansion required:** Add one row for every individual `REQ-SE-*` statement after `StateEstimation.md` is audited.

---

## 7.3 Motor Output

| Requirement Source | Architectural Allocation | Inputs | Outputs | Expected Implementation | Verification | Status |
| --- | --- | --- | --- | --- | --- | --- |
| REQ-FR-003 | ARC-001 Motor Output | ControlOutput, throttle command, system state | Four MotorCommands | Motor mixer and ESC driver | Unit test, logic-analyzer test, motor test | Defined |
| Motor-mixing requirements | ARC-001 Motor Output | Roll, pitch, yaw, throttle | Four mixed outputs | Mixer module | Known-vector unit tests | Verification Planned |
| Output-limiting requirements | ARC-001 Safe State | Requested motor values | Bounded motor values | Output limiter | Boundary-value tests | Verification Planned |
| Disarmed-output requirements | ARC-001 System Supervision | Disarmed state | Non-commanding outputs | Arming gate | Startup and state-transition test | Verification Planned |
| Motor-mapping requirements | ARC-001 Hardware Architecture | Logical motor command | Correct physical ESC channel | Board and output configuration | Propeller-free motor mapping test | Verification Planned |

**Expansion required:** Add one row for every individual `REQ-MO-*` statement after `MotorOutput.md` is audited.

---

## 7.4 Communications

| Requirement Range | Architectural Allocation | Expected Implementation | Verification Method | Planned Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-COM-001 through REQ-COM-004 | Development and Debug Interfaces | SWD and USB DFU configuration | I, D, T | Debugger and DFU bring-up record | Verification Planned |
| REQ-COM-005 through REQ-COM-008 | Development Communications | UART transport and diagnostic service | I, D, T | UART diagnostic test | Verification Planned |
| REQ-COM-009 through REQ-COM-017 | Telemetry | Telemetry generator and encoder | D, T | Telemetry output test | Defined |
| REQ-COM-018 through REQ-COM-025 | Command Reception | Command decoder, validator, and dispatcher | I, T | Command validation tests | Defined |
| REQ-COM-026 through REQ-COM-035 | Message Handling | Protocol parser and framing module | I, T | Parser unit-test suite | Defined |
| REQ-COM-036 through REQ-COM-040 | Data Integrity | CRC/checksum and sequence validation | A, T | Corruption and replay tests | Defined |
| REQ-COM-041 through REQ-COM-045 | Timing and Performance | Scheduler and communication service | A, T | Communication-load timing test | Defined |
| REQ-COM-046 through REQ-COM-051 | Fault Handling | Communication health and recovery logic | T | Fault-injection test record | Defined |
| REQ-COM-052 through REQ-COM-056 | Security and Safety | Command authorization boundaries | I, A, T | Safety-path inspection | Defined |
| REQ-COM-057 through REQ-COM-060 | Configuration | Central communication configuration | I, T | Configuration test | Defined |
| REQ-COM-061 through REQ-COM-065 | Testability | Host-side protocol test framework | I, T | Automated test results | Defined |
| REQ-COM-066 through REQ-COM-070 | Future Expansion | Transport-independent interfaces | I, A | Architecture review | Deferred |

---

# 8. Hardware Requirements Traceability

| Requirement Range | Architecture or Decision Allocation | Implementation Artifact | Verification Method | Planned Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-HW-001 through REQ-HW-004 | ARC-001 Hardware Architecture | System block diagram and BOM | I, A | Hardware architecture review | Defined |
| REQ-HW-005 through REQ-HW-015 | ADR-001 and Flight Controller architecture | STM32H743 development board configuration | I, D, T | MCU and peripheral bring-up record | Verification Planned |
| REQ-HW-016 through REQ-HW-022 | HDR-001 | ICM-20602 module and mount | I, D, T | WHO_AM_I and sensor data test | Verification Planned |
| REQ-HW-023 through REQ-HW-032 | HDR-002, HDR-003, HDR-004 | Motors, ESC, propellers, and mounts | I, A, T | Propulsion bench-test record | Verification Planned |
| REQ-HW-033 through REQ-HW-041 | HDR-005 and SES-002 | Battery and regulated power system | I, A, T | Rail-voltage and load test | Verification Planned |
| REQ-HW-042 through REQ-HW-045 | ARC-001 debug and communications interfaces | SWD, USB, and UART interfaces | I, D, T | Debug-interface test record | Verification Planned |
| REQ-HW-046 through REQ-HW-049 | ARC-001 Future Architecture | Reserved interfaces and test points | I, A | Expansion-interface review | Defined |
| REQ-HW-050 through REQ-HW-053 | ARC-001 and SES standards | Integrated hardware assembly | I, T | Vibration and thermal observations | Deferred |
| REQ-HW-054 through REQ-HW-058 | ARC-001 Safe State and SES-002 | Safe startup and protected wiring | I, D, T | Propeller-free safety test | Verification Planned |
| REQ-HW-059 through REQ-HW-060 | Hardware bring-up plan | Bring-up and configuration records | I | Completed bring-up checklist | Verification Planned |

---

# 9. Software Requirements Traceability

| Requirement Range | Architecture Allocation | Expected Implementation | Verification Method | Planned Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-SW-001 through REQ-SW-008 | ARC-001 Software Architecture | Platform, driver, service, and application directories | I, A | Software architecture review | Defined |
| REQ-SW-009 through REQ-SW-015 | ADR-004 and ADR-005 | Compiler and build configuration | I, D | Reproducible build record | Defined |
| REQ-SW-016 through REQ-SW-021 | ARC-001 Platform Layer | Startup, clocks, GPIO, timebase, watchdog | I, T | Platform bring-up tests | Verification Planned |
| REQ-SW-022 through REQ-SW-028 | ARC-001 Driver Layer | IMU, ESC, UART, and platform drivers | I, T | Driver unit and integration tests | Defined |
| REQ-SW-029 through REQ-SW-035 | ARC-001 Execution and Timing Model | Cooperative scheduler and periodic tasks | A, T | Timing and deadline measurements | Defined |
| REQ-SW-036 through REQ-SW-042 | ARC-001 Memory Architecture | Linker configuration and fixed-capacity buffers | I, A, T | Map-file and memory tests | Defined |
| REQ-SW-043 through REQ-SW-049 | ARC-001 Fault Handling | Fault manager and safe-state logic | I, T | Fault-injection tests | Defined |
| REQ-SW-050 through REQ-SW-054 | ARC-001 configuration responsibilities | Central configuration module | I, T | Invalid-configuration tests | Defined |
| REQ-SW-055 through REQ-SW-059 | ARC-001 Communications and Supervision | Logging and health interfaces | I, D, T | Diagnostic output test | Defined |
| REQ-SW-060 through REQ-SW-066 | ARC-001 Safe State | Arming state machine and motor gate | I, T | Arming and reset safety tests | Defined |
| REQ-SW-067 through REQ-SW-072 | ARC-001 testability principles | Host-test and bench-test framework | I, T | Automated test report | Defined |
| REQ-SW-073 through REQ-SW-077 | Project coding and documentation conventions | Source repository and interface documentation | I | Code-review checklist | Defined |

---

# 10. Mechanical Requirements Traceability

| Requirement Range | Architecture or Standard Allocation | Implementation Artifact | Verification Method | Planned Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-ME-001 through REQ-ME-006 | ADR-002 and ARC-001 | Rev A airframe CAD assembly | I, A | CAD architecture review | Defined |
| REQ-ME-007 through REQ-ME-012 | ADR-003 and SES-001 | Modular arms, mounts, and fastener interfaces | I, D | Module-replacement demonstration | Defined |
| REQ-ME-013 through REQ-ME-019 | SES-001 | Flight Controller and ESC mounts | I, D | Fit and access inspection | Verification Planned |
| REQ-ME-020 through REQ-ME-025 | HDR-002, HDR-004, SES-001 | Motor geometry and propeller envelope | I, A, D | Propeller-clearance record | Verification Planned |
| REQ-ME-026 through REQ-ME-031 | ARC-001 Mechanical Structure | Battery tray and retention system | I, D, T | Battery-retention test | Defined |
| REQ-ME-032 through REQ-ME-036 | HDR-001 and SES-001 | IMU mount | I, D, T | Orientation and vibration test | Defined |
| REQ-ME-037 through REQ-ME-041 | SES-001 and SES-002 | Cable-routing features | I | Wiring-clearance inspection | Defined |
| REQ-ME-042 through REQ-ME-048 | SES-001 | CAD source and manufacturing exports | I, D | Print and dimensional records | Defined |
| REQ-ME-049 through REQ-ME-054 | ARC-001 Mechanical Structure | Arms, center structure, and inserts | I, A, T | Structural and landing tests | Deferred |
| REQ-ME-055 through REQ-ME-059 | SES-001 | Serviceable assembly design | I, D | Maintenance demonstration | Defined |
| REQ-ME-060 through REQ-ME-063 | ARC-001 Future Architecture | Reserved payload and module interfaces | I, A | Expansion review | Deferred |
| REQ-ME-064 through REQ-ME-066 | SES-001 | Inspection checklist and dimensional records | I | Completed inspection records | Verification Planned |

---

# 11. Electrical Requirements Traceability

| Requirement Range | Architecture or Standard Allocation | Implementation Artifact | Verification Method | Planned Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-EL-001 through REQ-EL-005 | ARC-001 Power Distribution and SES-002 | System wiring diagram | I, A | Electrical architecture review | Defined |
| REQ-EL-006 through REQ-EL-012 | HDR-005 and SES-002 | 4S battery and XT30 harness | I, A, T | Polarity and load inspection | Verification Planned |
| REQ-EL-013 through REQ-EL-018 | ARC-001 Power Distribution | Regulated power source | I, A, T | Rail-voltage and transient test | Verification Planned |
| REQ-EL-019 through REQ-EL-023 | SES-002 | Grounding and return-path implementation | I, A, T | Continuity and noise measurements | Defined |
| REQ-EL-024 through REQ-EL-032 | HDR-007 and SES-002 | Aircraft wiring harnesses | I, A | Harness inspection | Defined |
| REQ-EL-033 through REQ-EL-038 | SES-002 | Battery and signal connectors | I, D | Connector retention inspection | Defined |
| REQ-EL-039 through REQ-EL-044 | HDR-001 and ARC-001 IMU Interface | SPI sensor harness | I, D, T | SPI and logic-level test | Verification Planned |
| REQ-EL-045 through REQ-EL-050 | HDR-003 and ARC-001 ESC Interface | ESC signal and motor-phase wiring | I, D, T | Motor mapping and direction test | Verification Planned |
| REQ-EL-051 through REQ-EL-057 | ARC-001 Development Interfaces | SWD and UART harnesses | I, D, T | Debug and UART test | Verification Planned |
| REQ-EL-058 through REQ-EL-064 | SES-002 | Protected bring-up configuration | I, D, T | Pre-power and safety checklist | Verification Planned |
| REQ-EL-065 through REQ-EL-070 | SES-002 | Solder joints and harness records | I, T | Workmanship and continuity records | Defined |
| REQ-EL-071 through REQ-EL-076 | SES-002 | Electrical test procedures | I, T | Bring-up and power-noise records | Verification Planned |
| REQ-EL-077 through REQ-EL-080 | ARC-001 Future Architecture | Reserved power and communication interfaces | I, A | Expansion-interface review | Deferred |

---

# 12. Documentation Requirements Traceability

| Requirement | Implementation Artifact | Verification Method | Evidence | Status |
| --- | --- | --- | --- | --- |
| REQ-DOC-001 — Authoritative Documentation | INDEX-001 and controlled document set | I | Documentation index review | Defined |
| REQ-DOC-002 — Unique Document Identification | Document metadata headers | I | Duplicate-ID scan | Verification Planned |
| REQ-DOC-003 — Revision History | Revision-history sections | I | Document audit | Defined |
| REQ-DOC-004 — Requirements Traceability | RTM-001 | I | This document | Implemented |
| REQ-DOC-005 — Decision Records | ADR and HDR directories | I | Decision-record audit | Defined |
| REQ-DOC-006 — Test Documentation | Future test procedures and records | I | Test-record audit | Deferred |
| REQ-DOC-007 — Link Integrity | Relative Markdown links | I, T | Repository link-check report | Verification Planned |
| REQ-DOC-008 — Documentation Index | INDEX-001 | I | Final documentation audit | Verification Planned |

---

# 13. Decision-Record Traceability

| Decision Record | Decision Area | Requirements Supported | Architecture Area | Status |
| --- | --- | --- | --- | --- |
| ADR-001 | STM32H743 architecture | REQ-HW-005 through REQ-HW-015; applicable REQ-SW requirements | Flight Controller and Platform | Active |
| ADR-002 | Rev A platform size | REQ-ME-001 through applicable airframe requirements | Mechanical Structure | Active |
| ADR-003 | Modular airframe architecture | REQ-ME-007 through REQ-ME-012 | Mechanical Structure | Active |
| ADR-004 | Custom flight software | REQ-SW-001 through REQ-SW-077 | Software Architecture | Active |
| ADR-005 | Flight-stack strategy | Functional and software requirement families | Software and Execution Model | Active |
| HDR-001 | ICM-20602 IMU | REQ-HW-016 through REQ-HW-022; REQ-EL-039 through REQ-EL-044 | Sensor Acquisition | Active |
| HDR-002 | HappyModel EX1404 motors | REQ-HW-023 through applicable propulsion requirements | Propulsion | Active |
| HDR-003 | Aero Selfie 45A ESC | REQ-HW-025 through REQ-HW-029; REQ-EL-045 through REQ-EL-050 | Propulsion and Motor Output | Active |
| HDR-004 | Gemfan Hurricane 3520 propellers | REQ-HW-030 through REQ-HW-032; REQ-ME-023 through REQ-ME-024 | Propulsion Geometry | Active |
| HDR-005 | 4S 850 mAh power system | REQ-HW-033 through REQ-HW-041; REQ-EL-006 through REQ-EL-018 | Power Distribution | Active |
| HDR-006 | Mechanical hardware standard | Applicable REQ-ME requirements | Mechanical Structure | Active |
| HDR-007 | Wiring-material standard | REQ-EL-024 through REQ-EL-038 | Electrical Integration | Active |

---

# 14. Verification Artifact Register

| Artifact ID | Artifact | Requirements Covered | Current Status |
| --- | --- | --- | --- |
| VER-HW-001 | Flight Controller programming and debug test | REQ-HW-005 through REQ-HW-015; REQ-COM-001 through REQ-COM-004 | Planned |
| VER-HW-002 | IMU SPI identity and data test | REQ-HW-016 through REQ-HW-022; REQ-EL-039 through REQ-EL-044 | Planned |
| VER-HW-003 | ESC and motor mapping test | REQ-HW-023 through REQ-HW-032; REQ-EL-045 through REQ-EL-050 | Planned |
| VER-EL-001 | Pre-power electrical inspection | REQ-EL-058 through REQ-EL-075 | Planned |
| VER-EL-002 | Regulated-rail and transient test | REQ-HW-037 through REQ-HW-041; REQ-EL-013 through REQ-EL-018 | Planned |
| VER-ME-001 | Mechanical fit and clearance inspection | REQ-ME-001 through REQ-ME-041 | Planned |
| VER-ME-002 | Battery-retention test | REQ-ME-026 through REQ-ME-031 | Planned |
| VER-SW-001 | Firmware clean-build verification | REQ-SW-009 through REQ-SW-015 | Planned |
| VER-SW-002 | Scheduler timing test | REQ-SW-029 through REQ-SW-035 | Planned |
| VER-SW-003 | Safe-state and arming test | REQ-SW-043 through REQ-SW-049; REQ-SW-060 through REQ-SW-066 | Planned |
| VER-COM-001 | UART diagnostic test | REQ-COM-005 through REQ-COM-017 | Planned |
| VER-COM-002 | Protocol parser unit tests | REQ-COM-018 through REQ-COM-040; REQ-COM-061 through REQ-COM-065 | Planned |
| VER-DOC-001 | Markdown link-integrity scan | REQ-DOC-007 | Planned |
| VER-DOC-002 | Documentation baseline audit | REQ-DOC-001 through REQ-DOC-008 | Planned |

---

# 15. Open Traceability Actions

| Action ID | Action | Priority | Status |
| --- | --- | --- | --- |
| TRACE-001 | Expand FlightControl.md into individual `REQ-FC-*` rows | High | Open |
| TRACE-002 | Expand StateEstimation.md into individual `REQ-SE-*` rows | High | Open |
| TRACE-003 | Expand MotorOutput.md into individual `REQ-MO-*` rows | High | Open |
| TRACE-004 | Add exact SPEC-001 objective or requirement identifiers after SPEC-001 audit | High | Open |
| TRACE-005 | Add firmware source paths as modules are implemented | Medium | Open |
| TRACE-006 | Add CAD filenames and part revisions | Medium | Open |
| TRACE-007 | Add wiring-diagram and harness artifact identifiers | Medium | Open |
| TRACE-008 | Add verification-procedure filenames | Medium | Open |
| TRACE-009 | Add verification results after testing | Medium | Open |
| TRACE-010 | Run repository-wide Markdown link validation | High | Open |
| TRACE-011 | Verify document identifiers are unique and consistent | High | Open |
| TRACE-012 | Update INDEX-001 with the completed requirements baseline | High | Open |

---

# 16. Baseline Completion Criteria

The Rev A requirements baseline may be considered complete when:

- All authoritative requirements documents are indexed.
- Every requirement has a stable identifier.
- Every requirement has an upstream source or documented rationale.
- Every requirement is allocated to an architecture element.
- Every requirement has a verification method.
- Applicable requirements identify an implementation destination.
- Broken cross-references have been corrected.
- Empty or obsolete scaffold documents have been populated, removed, or marked appropriately.
- INDEX-001 reflects the authoritative repository structure.
- Open traceability actions are either completed or explicitly deferred.

Completion of the requirements baseline does not mean that every requirement has been implemented or verified.

---

# 17. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Rev A Requirements Specification
- **ARC-001** — Stratus System Architecture
- **BOM-001** — Bill of Materials
- **SES-001** — Mechanical Engineering Standard
- **SES-002** — Electrical Engineering Standard
- **REQ-FR-001** — Flight Control Functional Requirements
- **REQ-FR-002** — State Estimation Functional Requirements
- **REQ-FR-003** — Motor Output Functional Requirements
- **REQ-FR-004** — Communications Functional Requirements
- **REQ-HW-001** — Hardware Requirements
- **REQ-SW-001** — Software Requirements
- **REQ-ME-001** — Mechanical Requirements
- **REQ-EL-001** — Electrical Requirements
- **ADR Series** — Architecture Decision Records
- **HDR Series** — Hardware Decision Records

---

# 18. Related Documents

## Upstream

- SPEC-001
- REQ-001
- ARC-001

## Peer

- INDEX-001
- BOM-001
- SES-001
- SES-002
- ADR Series
- HDR Series

## Supporting Requirements

- REQ-FR-001
- REQ-FR-002
- REQ-FR-003
- REQ-FR-004
- REQ-HW-001
- REQ-SW-001
- REQ-ME-001
- REQ-EL-001

## Downstream

- Firmware source code
- CAD source models
- Manufacturing exports
- Wiring diagrams
- Interface-control documents
- Verification procedures
- Bench-test records
- Integration-test records
- Flight-test records