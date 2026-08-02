# Stratus Software Requirements

**Document ID:** REQ-SW-001  
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
| 1.0 | 2026-08-02 | Initial software requirements | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Software Architecture Requirements
4. Language and Build Requirements
5. Platform Requirements
6. Driver Requirements
7. Scheduling and Timing Requirements
8. Memory Requirements
9. Fault-Handling Requirements
10. Configuration Requirements
11. Logging and Diagnostics Requirements
12. Safety Requirements
13. Testability Requirements
14. Maintainability Requirements
15. Requirement Summary
16. References
17. Related Documents

---

# 1. Purpose

This document defines the software requirements for Stratus Rev A.

These requirements govern the architecture, implementation, timing, memory use, safety behavior, testability, and maintenance of the embedded flight software.

---

# 2. Scope

This document applies to:

- Startup software
- Platform abstraction
- Device drivers
- Scheduling
- Sensor acquisition
- State estimation
- Flight control
- Motor output
- System supervision
- Communications
- Diagnostics
- Configuration
- Fault handling
- Host-based tests

Detailed functional behavior is defined in:

- **REQ-FR-001** — Flight Control
- **REQ-FR-002** — State Estimation
- **REQ-FR-003** — Motor Output
- **REQ-FR-004** — Communications

---

# 3. Software Architecture Requirements

## REQ-SW-001 — Layered Architecture

The flight software shall use a layered architecture consisting of:

- Platform layer
- Driver layer
- Service layer
- Application layer

**Verification:**  
Architecture and code inspection.

---

## REQ-SW-002 — Dependency Direction

Dependencies shall flow from higher-level application software toward lower-level services, drivers, and platform interfaces.

Lower layers shall not depend on higher-level application modules.

**Verification:**  
Dependency review.

---

## REQ-SW-003 — Hardware Abstraction

Application software shall not directly access processor registers or board-specific peripheral handles.

**Verification:**  
Code inspection.

---

## REQ-SW-004 — Device Isolation

Device-specific behavior shall be isolated within device drivers.

**Verification:**  
Code inspection.

---

## REQ-SW-005 — Domain Types

Data passed among application subsystems shall use explicit domain types rather than unstructured arrays or hardware-specific representations.

Examples include:

- `ImuSample`
- `AttitudeEstimate`
- `FlightSetpoint`
- `ControlOutput`
- `MotorCommands`
- `SystemHealth`

**Verification:**  
Code inspection.

---

## REQ-SW-006 — Clear Ownership

Software objects, buffers, and shared data shall have defined ownership and lifetime.

**Verification:**  
Design and code review.

---

## REQ-SW-007 — Minimal Global State

Uncontrolled mutable global state shall be avoided.

**Verification:**  
Code inspection.

---

## REQ-SW-008 — Replaceable Implementations

Sensor drivers, output protocols, and communication transports shall be replaceable without redesigning unrelated application logic.

**Verification:**  
Architecture review and substitution test where practical.

---

# 4. Language and Build Requirements

## REQ-SW-009 — Production Language

The long-lived Stratus flight software shall be implemented primarily in modern embedded C++.

**Verification:**  
Source-code inspection.

---

## REQ-SW-010 — C Compatibility

C may be used where required for:

- Startup code
- Vendor libraries
- CMSIS
- Low-level platform interfaces
- Third-party components

**Verification:**  
Source-code inspection.

---

## REQ-SW-011 — Language Standard

The selected C++ language standard shall be explicitly defined in the build configuration.

**Verification:**  
Build-system inspection.

---

## REQ-SW-012 — Warning Policy

Production firmware shall compile with a documented warning level.

New warnings shall be reviewed rather than ignored by default.

**Verification:**  
Build-log inspection.

---

## REQ-SW-013 — Reproducible Build

The project shall document the compiler, build tools, target device, and required configuration.

**Verification:**  
Clean-build demonstration.

---

## REQ-SW-014 — Debug and Release Configurations

The build system shall support separate debug and release configurations.

**Verification:**  
Build demonstration.

---

## REQ-SW-015 — Version Identification

Firmware shall expose or record a version identifier.

**Verification:**  
Build and runtime inspection.

---

# 5. Platform Requirements

## REQ-SW-016 — Startup Initialization

The software shall initialize processor state, memory, clocks, and required runtime support before executing application logic.

**Verification:**  
Code inspection and startup test.

---

## REQ-SW-017 — Safe GPIO Initialization

Motor-control and safety-relevant GPIO shall enter defined safe states before dependent application modules initialize.

**Verification:**  
Code review and signal measurement.

---

## REQ-SW-018 — Monotonic Timebase

The software shall provide a monotonic hardware-backed timebase.

**Verification:**  
Timing test.

---

## REQ-SW-019 — Peripheral Timeout Support

Platform interfaces that may fail to complete shall support bounded timeouts.

**Verification:**  
Code inspection and fault-injection test.

---

## REQ-SW-020 — Reset-Cause Access

The software should provide access to the processor reset cause.

**Verification:**  
Functional test.

---

## REQ-SW-021 — Watchdog Provision

The platform shall support use of a hardware watchdog.

**Verification:**  
Platform inspection and future watchdog test.

---

# 6. Driver Requirements

## REQ-SW-022 — Driver Initialization Result

Each device driver shall report whether initialization succeeded or failed.

**Verification:**  
Code inspection and fault test.

---

## REQ-SW-023 — Driver Error Reporting

Drivers shall report communication or device failures using defined result or status types.

**Verification:**  
Code inspection.

---

## REQ-SW-024 — No Hidden Infinite Blocking

Drivers shall not block indefinitely while waiting for hardware.

**Verification:**  
Code inspection and timeout testing.

---

## REQ-SW-025 — IMU Identity Check

The IMU driver shall verify the device identity before reporting the sensor as operational.

**Verification:**  
Functional test.

---

## REQ-SW-026 — IMU Configuration Verification

The IMU driver should verify critical configuration registers after initialization.

**Verification:**  
Driver test.

---

## REQ-SW-027 — Sample Timestamp

Sensor samples shall be associated with a monotonic timestamp.

**Verification:**  
Code and telemetry inspection.

---

## REQ-SW-028 — Output Safe State

The ESC or motor-output driver shall support an explicit non-commanding output state.

**Verification:**  
Functional test.

---

# 7. Scheduling and Timing Requirements

## REQ-SW-029 — Deterministic Execution Model

Rev A shall use a deterministic cooperative or time-triggered execution model unless superseded by an approved architecture decision.

**Verification:**  
Architecture and code inspection.

---

## REQ-SW-030 — Bounded Task Execution

Periodic tasks shall have bounded execution behavior.

**Verification:**  
Execution-time measurement.

---

## REQ-SW-031 — Deadline Monitoring

The software should detect missed or excessively delayed executions of critical periodic functions.

**Verification:**  
Timing-fault test.

---

## REQ-SW-032 — ISR Restrictions

Interrupt service routines shall perform only time-critical operations and shall defer complex processing.

**Verification:**  
Code inspection.

---

## REQ-SW-033 — Control Timing

The software shall provide consistent time intervals or measured time deltas for state estimation and control.

**Verification:**  
Timing measurement.

---

## REQ-SW-034 — Stale Data Detection

The software shall detect sensor measurements and state estimates that exceed their permitted age.

**Verification:**  
Fault-injection test.

---

## REQ-SW-035 — Nonblocking Communications

Communication output shall not prevent execution of flight-critical tasks.

**Verification:**  
Communication-load stress test.

---

# 8. Memory Requirements

## REQ-SW-036 — Bounded Memory Use

Flight software memory use shall be bounded.

**Verification:**  
Memory-map and code inspection.

---

## REQ-SW-037 — Static Allocation

Flight-critical runtime data shall use static, automatic, or otherwise bounded allocation.

**Verification:**  
Code inspection.

---

## REQ-SW-038 — Dynamic Allocation Restriction

Uncontrolled dynamic allocation after startup shall not be used in flight-critical software.

**Verification:**  
Code and linker inspection.

---

## REQ-SW-039 — Stack Review

Stack use shall be reviewed and sized with margin.

**Verification:**  
Static analysis or runtime watermark measurement.

---

## REQ-SW-040 — Fixed-Capacity Buffers

Communication and logging buffers shall have fixed or bounded capacity.

**Verification:**  
Code inspection.

---

## REQ-SW-041 — DMA Memory Compatibility

DMA buffers shall be placed in compatible memory and handled correctly with respect to the STM32H7 cache architecture.

**Verification:**  
Memory-placement review and DMA test.

---

## REQ-SW-042 — Buffer Overflow Protection

Buffer boundaries shall be checked or guaranteed by construction.

**Verification:**  
Code inspection and boundary tests.

---

# 9. Fault-Handling Requirements

## REQ-SW-043 — Fault Classification

Software faults shall be classified by severity.

**Verification:**  
Design inspection.

---

## REQ-SW-044 — Critical Fault Response

A detected critical fault shall prevent or terminate active motor commands through the defined safe-state mechanism.

**Verification:**  
Fault-injection test without propellers.

---

## REQ-SW-045 — Fault Recording

The software should record sufficient information to identify the source of detected faults.

**Verification:**  
Fault telemetry or log inspection.

---

## REQ-SW-046 — Invalid State Handling

Unexpected state-machine transitions shall be rejected or handled deterministically.

**Verification:**  
State-transition testing.

---

## REQ-SW-047 — Watchdog Service Policy

The watchdog shall only be serviced when required critical software functions have made acceptable progress.

**Verification:**  
Code inspection and watchdog test.

---

## REQ-SW-048 — Assertion Policy

Assertions may be used during development but shall not be the sole mechanism for production fault handling.

**Verification:**  
Code inspection.

---

## REQ-SW-049 — Recoverable Fault Isolation

A recoverable noncritical subsystem fault should not force a complete processor reset when controlled reinitialization is possible.

**Verification:**  
Fault-recovery testing.

---

# 10. Configuration Requirements

## REQ-SW-050 — Central Configuration

Board assignments, peripheral selections, communication settings, and major constants shall be centrally defined.

**Verification:**  
Code inspection.

---

## REQ-SW-051 — Configuration Validation

Configuration values shall be validated before use.

**Verification:**  
Invalid-configuration test.

---

## REQ-SW-052 — Safe Defaults

Default configuration shall produce a disarmed and non-commanding system state.

**Verification:**  
Startup test.

---

## REQ-SW-053 — Parameter Range Definition

Parameters affecting flight behavior shall have documented valid ranges.

**Verification:**  
Documentation and code inspection.

---

## REQ-SW-054 — Persistent Configuration Integrity

When persistent runtime configuration is introduced, it shall include:

- Format version
- Validation
- Default recovery
- Corruption detection

**Verification:**  
Future configuration test.

---

# 11. Logging and Diagnostics Requirements

## REQ-SW-055 — Diagnostic Output

The software shall provide development diagnostic output.

**Verification:**  
Functional demonstration.

---

## REQ-SW-056 — Diagnostic Rate Control

Diagnostic output shall support configurable verbosity or message selection.

**Verification:**  
Configuration test.

---

## REQ-SW-057 — No Sensitive Diagnostic Leakage

Diagnostics shall not intentionally expose secrets or private credentials.

**Verification:**  
Code inspection.

---

## REQ-SW-058 — Health Reporting

Each major subsystem shall provide a health or validity indication.

**Verification:**  
Interface and telemetry inspection.

---

## REQ-SW-059 — Communication Statistics

The software should maintain selected communication and fault counters.

**Verification:**  
Functional test.

---

# 12. Safety Requirements

## REQ-SW-060 — Disarmed Startup

The system shall start in a disarmed state.

**Verification:**  
Startup test.

---

## REQ-SW-061 — Explicit Arming

The system shall require an explicit valid transition before entering the armed state.

**Verification:**  
State-machine test.

---

## REQ-SW-062 — Arming Preconditions

Arming shall be rejected unless required health and initialization checks pass.

**Verification:**  
Fault-injection test.

---

## REQ-SW-063 — Motor Command Limiting

Motor commands shall be constrained to defined valid limits.

**Verification:**  
Boundary testing.

---

## REQ-SW-064 — Communication Bypass Prevention

External communications shall not bypass arming logic, safety limits, or System Supervision.

**Verification:**  
Architecture and functional testing.

---

## REQ-SW-065 — Invalid Numeric Handling

NaN, infinity, and otherwise invalid numeric values shall not be allowed to propagate into active motor commands.

**Verification:**  
Fault-injection test.

---

## REQ-SW-066 — Software Reset Safety

Processor reset or software restart shall return motor outputs to the defined non-commanding state.

**Verification:**  
Reset test without propellers.

---

# 13. Testability Requirements

## REQ-SW-067 — Host-Based Algorithm Testing

State-estimation, control, mixing, parsing, and other hardware-independent logic shall be testable on a host computer.

**Verification:**  
Host-test execution.

---

## REQ-SW-068 — Dependency Substitution

Hardware interfaces should permit substitution with mocks, fakes, or test implementations.

**Verification:**  
Unit-test architecture review.

---

## REQ-SW-069 — Boundary Testing

Software shall be tested at documented input and output boundaries.

**Verification:**  
Test review.

---

## REQ-SW-070 — Fault Injection

The test architecture shall support injection of:

- Sensor failure
- Communication failure
- Stale data
- Invalid configuration
- Timing faults
- Invalid numeric data

**Verification:**  
Test execution.

---

## REQ-SW-071 — Hardware-in-the-Loop Testing

The project should support hardware-in-the-loop or bench integration testing before flight.

**Verification:**  
Integration-test demonstration.

---

## REQ-SW-072 — Regression Testing

Corrected software defects should receive regression tests where practical.

**Verification:**  
Test-repository inspection.

---

# 14. Maintainability Requirements

## REQ-SW-073 — Descriptive Naming

Software identifiers shall use descriptive names consistent with subsystem terminology.

**Verification:**  
Code review.

---

## REQ-SW-074 — Documented Interfaces

Public software interfaces shall document responsibilities, inputs, outputs, ownership, and failure behavior.

**Verification:**  
Code and documentation inspection.

---

## REQ-SW-075 — Single Responsibility

Modules and classes should have focused responsibilities.

**Verification:**  
Design review.

---

## REQ-SW-076 — Source Traceability

Implemented flight behavior shall be traceable to applicable requirements.

**Verification:**  
Traceability-matrix inspection.

---

## REQ-SW-077 — Version-Controlled Source

Authoritative source code and build configuration shall be maintained in version control.

**Verification:**  
Repository inspection.

---

# 15. Requirement Summary

| Requirement Range | Area |
| --- | --- |
| REQ-SW-001 through REQ-SW-008 | Architecture |
| REQ-SW-009 through REQ-SW-015 | Language and build |
| REQ-SW-016 through REQ-SW-021 | Platform |
| REQ-SW-022 through REQ-SW-028 | Drivers |
| REQ-SW-029 through REQ-SW-035 | Scheduling and timing |
| REQ-SW-036 through REQ-SW-042 | Memory |
| REQ-SW-043 through REQ-SW-049 | Fault handling |
| REQ-SW-050 through REQ-SW-054 | Configuration |
| REQ-SW-055 through REQ-SW-059 | Diagnostics |
| REQ-SW-060 through REQ-SW-066 | Safety |
| REQ-SW-067 through REQ-SW-072 | Testability |
| REQ-SW-073 through REQ-SW-077 | Maintainability |

---

# 16. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Requirements Index
- **ARC-001** — Stratus System Architecture
- **REQ-FR-001** — Flight Control
- **REQ-FR-002** — State Estimation
- **REQ-FR-003** — Motor Output
- **REQ-FR-004** — Communications
- **ADR-004** — Custom Flight Software
- **ADR-005** — Flight Stack Strategy

---

# 17. Related Documents

## Upstream

- SPEC-001
- ARC-001
- REQ-001

## Peer

- REQ-HW-001 — Hardware Requirements
- REQ-ME-001 — Mechanical Requirements
- REQ-EL-001 — Electrical Requirements

## Downstream

- Software design documents
- Source code
- Unit tests
- Integration tests
- Software verification records