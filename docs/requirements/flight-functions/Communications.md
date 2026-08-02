# Stratus Communications Functional Requirements

**Document ID:** REQ-FR-004  
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
| 1.0 | 2026-08-02 | Initial communications functional requirements | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Communications Architecture
4. Operating Assumptions
5. Development Communications Requirements
6. Telemetry Requirements
7. Command Reception Requirements
8. Message Handling Requirements
9. Data Integrity Requirements
10. Timing and Performance Requirements
11. Fault Handling Requirements
12. Security and Safety Requirements
13. Configuration Requirements
14. Testability Requirements
15. Future Communications Requirements
16. Requirement Summary
17. References
18. Related Documents

---

# 1. Purpose

This document defines the functional requirements for communications within Stratus Rev A.

The Communications subsystem provides the interfaces required to:

- Program and debug the Flight Controller
- Produce development diagnostics
- Transmit system telemetry
- Receive validated commands
- Report system health and faults
- Support future ground-station and radio integration

These requirements define required behavior rather than selecting a specific operational radio, telemetry protocol, or ground-station implementation.

---

# 2. Scope

This document applies to communications between the Stratus Flight Controller and external systems.

The scope includes:

- SWD programming and debugging
- USB firmware programming and recovery
- Development UART
- Diagnostic messages
- Telemetry output
- Command reception
- Message validation
- Communication timeouts
- Communication fault reporting
- Future operational command and telemetry links

The following are outside the implemented Rev A scope unless added through an approved change:

- Long-range radio control
- Encrypted operational command links
- Cellular communication
- Satellite communication
- Swarm networking
- Autonomous mission upload
- Video transmission
- High-bandwidth payload data

---

# 3. Communications Architecture

The Communications subsystem shall be separated into the following logical functions:

- Physical or peripheral transport
- Transport driver
- Message framing
- Message validation
- Command handling
- Telemetry generation
- Diagnostic output
- Communication health monitoring

The architecture shall prevent application-level flight behavior from depending directly on UART, USB, or radio peripheral registers.

Conceptual flow:

```text
External System
      │
      ▼
Physical Transport
      │
      ▼
Transport Driver
      │
      ▼
Framing and Validation
      │
      ├──▶ Command Handler
      │
      ├──▶ Configuration Handler
      │
      └──▶ Diagnostic Handler

Aircraft State
      │
      ▼
Telemetry Generator
      │
      ▼
Message Encoder
      │
      ▼
Transport Driver
      │
      ▼
External System

# 4. Operating Assumptions

The following assumptions apply to Rev A:

- SWD is the primary development-debugging interface.
- USB DFU is available as a firmware-programming or recovery path.
- A UART interface is available for development diagnostics.
- Operational radio hardware has not yet been selected.
- Early command inputs may originate from development tools rather than a flight-ready controller.
- Communication loss shall not produce uncontrolled motor behavior.
- Flight-critical stabilization shall continue independently of noncritical telemetry output where safe and technically possible.

---

# 5. Development Communications Requirements

## REQ-COM-001 — SWD Programming Support

The Flight Controller shall support firmware programming through SWD.

**Rationale:**  
SWD provides reliable programming and debugging access during firmware development.

**Verification:**  
Demonstration by programming valid firmware through an ST-Link-compatible debugger.

---

## REQ-COM-002 — SWD Debug Support

The Flight Controller shall support processor halt, resume, single-step execution, breakpoints, and memory inspection through SWD.

**Rationale:**  
Low-level debugging is required for bring-up and fault diagnosis.

**Verification:**  
Demonstration using the development environment.

---

## REQ-COM-003 — Reset Access

The development interface should provide access to the target reset signal.

**Rationale:**  
External reset improves recovery from startup and firmware faults.

**Verification:**  
Inspection and functional demonstration.

---

## REQ-COM-004 — USB Firmware Recovery

The Flight Controller shall support firmware loading or recovery through the STM32 USB DFU bootloader when the hardware configuration permits.

**Rationale:**  
DFU provides an alternate recovery path when SWD is unavailable or inconvenient.

**Verification:**  
Demonstration using STM32CubeProgrammer or an equivalent tool.

---

## REQ-COM-005 — Development UART

The Flight Controller shall provide at least one UART interface for development diagnostics.

**Rationale:**  
A UART provides a simple and observable diagnostic path independent of the debugger.

**Verification:**  
Inspection and transmission demonstration.

---

## REQ-COM-006 — Default UART Configuration

The initial development UART shall use the following default configuration unless superseded by the board-interface documentation:

- 115200 baud
- 8 data bits
- No parity
- 1 stop bit

**Rationale:**  
A documented default reduces setup ambiguity during bring-up.

**Verification:**  
Configuration inspection and terminal demonstration.

---

## REQ-COM-007 — Nonblocking Diagnostic Output

Diagnostic output shall not indefinitely block time-critical flight execution.

**Rationale:**  
A slow or disconnected terminal shall not suspend estimation or control.

**Verification:**  
Code inspection and timing test with the receiver disconnected or congested.

---

## REQ-COM-008 — Configurable Diagnostic Verbosity

The software shall support enabling, reducing, or disabling diagnostic output by build configuration or runtime configuration.

**Rationale:**  
Verbose diagnostics are useful during bring-up but may interfere with timing during integrated operation.

**Verification:**  
Inspection and demonstration using at least two verbosity configurations.

---

# 6. Telemetry Requirements

## REQ-COM-009 — Telemetry Output

The Communications subsystem shall support transmission of system telemetry to an external receiver.

**Rationale:**  
Telemetry is required for observing system behavior without halting execution.

**Verification:**  
Demonstration using a development UART or future telemetry transport.

---

## REQ-COM-010 — System-State Telemetry

The telemetry interface shall be capable of reporting the current system operating state.

Examples include:

- Booting
- Initializing
- Disarmed
- Armed
- Faulted
- Safe state

**Verification:**  
Functional test across supported operating-state transitions.

---

## REQ-COM-011 — Sensor Telemetry

The telemetry interface shall be capable of reporting selected inertial-sensor measurements.

At minimum, the interface should support:

- Angular rate
- Acceleration
- Sample timestamp
- Sensor validity

**Verification:**  
Functional demonstration using live or recorded sensor data.

---

## REQ-COM-012 — State-Estimate Telemetry

The telemetry interface shall be capable of reporting selected state-estimation outputs.

At minimum, the interface should support:

- Estimated orientation
- Estimate timestamp
- Estimate-valid flag

**Verification:**  
Functional demonstration.

---

## REQ-COM-013 — Motor-Command Telemetry

The telemetry interface shall be capable of reporting individual motor commands.

**Rationale:**  
Motor-command visibility supports mixer, output, and control-loop verification.

**Verification:**  
Demonstration while motor outputs remain physically safe.

---

## REQ-COM-014 — Power Telemetry

When battery or rail monitoring is implemented, the telemetry interface shall support reporting available power-system measurements.

Potential values include:

- Battery voltage
- Regulated rail voltage
- Current
- Low-voltage state

**Verification:**  
Functional demonstration when the applicable sensing hardware exists.

---

## REQ-COM-015 — Fault Telemetry

The telemetry interface shall support reporting active faults and fault identifiers.

**Rationale:**  
Fault visibility is necessary for troubleshooting and safe operation.

**Verification:**  
Fault-injection test.

---

## REQ-COM-016 — Telemetry Selection

The software shall permit selection or configuration of which telemetry messages are transmitted.

**Rationale:**  
Not all data can or should be transmitted at maximum rate.

**Verification:**  
Configuration inspection and demonstration.

---

## REQ-COM-017 — Telemetry Rate Control

Telemetry transmission rates shall be independently configurable by message category where practical.

**Rationale:**  
High-rate sensor data and low-rate status data have different bandwidth needs.

**Verification:**  
Measurement of message rates under at least two configurations.

---

# 7. Command Reception Requirements

## REQ-COM-018 — Command Reception

The Communications subsystem shall support receipt of externally generated commands.

**Rationale:**  
Future operation requires an external source for setpoints, configuration, or system commands.

**Verification:**  
Demonstration using a development transport.

---

## REQ-COM-019 — Command Validation

Each received command shall be validated before it affects system behavior.

Validation shall include, as applicable:

- Message format
- Message type
- Message length
- Checksum or integrity field
- Parameter range
- System-state permission
- Command freshness

**Verification:**  
Functional and malformed-message testing.

---

## REQ-COM-020 — Invalid Command Rejection

Malformed, unsupported, unauthorized, stale, or out-of-range commands shall be rejected.

**Rationale:**  
Invalid input shall not directly affect flight behavior.

**Verification:**  
Fault-injection testing using invalid messages.

---

## REQ-COM-021 — Command Acknowledgment

Commands that change system state or configuration should produce an acknowledgment indicating success or failure.

**Verification:**  
Demonstration with valid and invalid commands.

---

## REQ-COM-022 — Arming Command Restrictions

An external command shall not arm the aircraft unless all system arming preconditions are satisfied.

**Rationale:**  
Communication access shall not bypass System Supervision.

**Verification:**  
Functional test with valid and invalid arming conditions.

---

## REQ-COM-023 — Disarm Command Priority

A valid disarm or emergency-stop command shall receive priority over noncritical communication processing.

**Rationale:**  
Commands intended to stop propulsion must not be delayed by telemetry or configuration traffic.

**Verification:**  
Timing and functional test under communication load.

---

## REQ-COM-024 — Flight Setpoint Range Checking

Received flight setpoints shall be constrained to documented valid ranges before being forwarded to Flight Control.

**Verification:**  
Boundary-value testing.

---

## REQ-COM-025 — Configuration Command Restrictions

Configuration values affecting flight behavior shall only be changed while the system is in an allowed operating state.

The default allowed state should be disarmed.

**Verification:**  
Functional test while disarmed and armed.

---

# 8. Message Handling Requirements

## REQ-COM-026 — Framed Messages

Operational communication messages shall use an explicit framing method.

The framing method shall permit the receiver to identify:

- Message start
- Message type
- Payload length
- Payload
- Integrity field
- Message end or next-message boundary

**Verification:**  
Protocol inspection and parser test.

---

## REQ-COM-027 — Unique Message Identification

Each supported operational message type shall have a unique identifier.

**Verification:**  
Protocol documentation inspection.

---

## REQ-COM-028 — Version Identification

The communication protocol shall include a method for identifying the protocol or message-format version.

**Rationale:**  
Version identification supports compatibility across firmware revisions.

**Verification:**  
Protocol inspection and compatibility test.

---

## REQ-COM-029 — Bounded Message Size

All received messages shall have a defined maximum size.

**Rationale:**  
Bounded sizes support deterministic memory use and parser safety.

**Verification:**  
Code inspection and oversized-message testing.

---

## REQ-COM-030 — Fixed-Capacity Buffers

Flight software communication buffers shall use fixed or otherwise bounded capacity.

**Rationale:**  
Communication traffic shall not cause uncontrolled dynamic-memory consumption.

**Verification:**  
Code inspection.

---

## REQ-COM-031 — Parser Recovery

The message parser shall recover from malformed or incomplete input and resume processing later valid messages.

**Verification:**  
Test using corrupted, truncated, and noise-injected data streams.

---

## REQ-COM-032 — Unknown Message Handling

Unknown message identifiers shall be rejected or ignored without causing undefined behavior.

**Verification:**  
Functional test.

---

## REQ-COM-033 — Partial Message Timeout

The receiver shall abandon an incomplete message after a defined timeout or parser-reset condition.

**Verification:**  
Functional test with truncated input.

---

## REQ-COM-034 — Endianness Definition

Multibyte protocol fields shall use a documented byte order.

**Verification:**  
Protocol inspection and encode/decode test.

---

## REQ-COM-035 — Data-Type Definition

Protocol fields shall use explicitly defined widths and interpretations.

Examples include:

- Unsigned 8-bit integer
- Signed 16-bit integer
- IEEE 754 32-bit floating point
- Fixed-point value with documented scale

**Verification:**  
Protocol inspection.

---

# 9. Data Integrity Requirements

## REQ-COM-036 — Message Integrity Check

Operational messages shall include an integrity-check mechanism.

A checksum or cyclic redundancy check may be used.

**Verification:**  
Corruption-detection test.

---

## REQ-COM-037 — Corrupted Message Rejection

A message that fails its integrity check shall not be forwarded to the applicable application subsystem.

**Verification:**  
Fault-injection testing.

---

## REQ-COM-038 — Sequence Information

Time-sensitive operational command messages should include a sequence number, timestamp, or equivalent freshness indicator.

**Rationale:**  
The receiver must be able to detect repeated, delayed, or out-of-order commands where those conditions matter.

**Verification:**  
Protocol inspection and sequence test.

---

## REQ-COM-039 — Duplicate Command Handling

Duplicate commands shall be handled deterministically.

Commands that must execute only once shall not be unintentionally repeated due to retransmission.

**Verification:**  
Duplicate-message testing.

---

## REQ-COM-040 — Stale Command Rejection

Commands older than the defined validity interval shall be rejected when command age can be determined.

**Verification:**  
Timestamp or timeout test.

---

# 10. Timing and Performance Requirements

## REQ-COM-041 — Communication Processing Budget

Communication processing shall execute within a bounded time budget appropriate to its assigned task rate.

**Verification:**  
Execution-time measurement.

---

## REQ-COM-042 — Telemetry Load Limiting

Telemetry generation shall not consume sufficient CPU time or bandwidth to cause flight-control deadline failures.

**Verification:**  
Stress test at maximum configured telemetry load.

---

## REQ-COM-043 — Command Processing Latency

Valid high-priority commands shall be processed within a documented maximum latency.

The final latency requirement shall be established after transport selection and scheduler measurement.

**Verification:**  
Timing measurement.

---

## REQ-COM-044 — Communication Timeout Detection

The system shall detect loss of an expected operational command link after a defined timeout.

**Verification:**  
Disconnect or silence test.

---

## REQ-COM-045 — Independent Stabilization Timing

Loss or congestion of noncritical communications shall not directly stop required sensor acquisition, state estimation, flight control, or motor-output scheduling.

**Verification:**  
Communication-stress test while monitoring control-loop timing.

---

# 11. Fault Handling Requirements

## REQ-COM-046 — Communication Fault Reporting

The subsystem shall report communication faults to System Supervision.

Faults may include:

- Buffer overflow
- Repeated integrity failure
- Transport failure
- Command timeout
- Parser failure
- Unsupported protocol version

**Verification:**  
Fault-injection testing.

---

## REQ-COM-047 — Command-Link Loss Response

Loss of an operational command link shall result in a predefined system response.

The response shall be selected according to the available flight capability and may include:

- Rejecting further arming
- Holding a safe setpoint
- Entering a failsafe mode
- Disarming when safe and appropriate
- Entering the system safe state

The Rev A response shall be documented before untethered flight.

**Verification:**  
Controlled link-loss test.

---

## REQ-COM-048 — Telemetry Failure Isolation

Failure of telemetry transmission alone shall not automatically produce a critical flight fault unless telemetry is explicitly required for the active operating mode.

**Verification:**  
Transport-disconnect test.

---

## REQ-COM-049 — Buffer Overflow Handling

A communication-buffer overflow shall be detected and handled without memory corruption.

**Verification:**  
Stress and overflow testing.

---

## REQ-COM-050 — Transport Reinitialization

A failed noncritical communication transport should be capable of controlled reinitialization without resetting the complete Flight Controller.

**Verification:**  
Fault-injection and recovery test.

---

## REQ-COM-051 — Critical Communication Failure

When a communication failure prevents safe command interpretation, affected commands shall be rejected and the failure shall be reported to System Supervision.

**Verification:**  
Fault-injection testing.

---

# 12. Security and Safety Requirements

## REQ-COM-052 — No Direct Motor Command Bypass

External communication messages shall not bypass Motor Output safety limits, arming logic, or System Supervision.

**Verification:**  
Architecture and code inspection.

---

## REQ-COM-053 — Restricted Dangerous Commands

Commands capable of arming, starting motors, erasing configuration, or changing critical parameters shall require explicit message types and state validation.

**Verification:**  
Functional test.

---

## REQ-COM-054 — Debug Interface Awareness

The system documentation shall identify SWD, USB, UART, and other development interfaces as trusted physical-access interfaces.

**Rationale:**  
Rev A development interfaces are not intended to provide operational security against a physically connected attacker.

**Verification:**  
Documentation inspection.

---

## REQ-COM-055 — Sensitive Data

The system shall not intentionally transmit secret credentials or private keys through unprotected diagnostic output.

**Verification:**  
Code and configuration inspection.

---

## REQ-COM-056 — Operational Security Provision

The architecture shall permit future addition of authenticated and encrypted command transport without redesigning Flight Control.

**Verification:**  
Architecture review.

---

# 13. Configuration Requirements

## REQ-COM-057 — Transport Configuration

Communication transport settings shall be centrally defined rather than duplicated across unrelated modules.

Settings may include:

- Baud rate
- Peripheral instance
- Pin assignment
- Buffer size
- Timeout
- Message rates

**Verification:**  
Code inspection.

---

## REQ-COM-058 — Protocol Configuration

Protocol constants shall be explicitly documented or defined in a common interface module.

**Verification:**  
Code and documentation inspection.

---

## REQ-COM-059 — Safe Default Configuration

The default communication configuration shall not cause motor arming or active propulsion during startup.

**Verification:**  
Startup test.

---

## REQ-COM-060 — Configuration Validation

Communication configuration values shall be validated before use.

**Verification:**  
Invalid-configuration testing.

---

# 14. Testability Requirements

## REQ-COM-061 — Host-Side Message Testing

Message encoding and decoding logic shall be testable without physical aircraft hardware.

**Rationale:**  
Protocol behavior should be independently verifiable.

**Verification:**  
Host-based unit test.

---

## REQ-COM-062 — Parser Unit Tests

The message parser shall have tests covering:

- Valid messages
- Invalid length
- Invalid integrity field
- Unknown message type
- Truncated message
- Oversized message
- Back-to-back messages
- Noise before a valid frame

**Verification:**  
Unit-test review and execution.

---

## REQ-COM-063 — Loopback Testing

At least one supported communication transport should permit loopback or equivalent end-to-end testing.

**Verification:**  
Functional demonstration.

---

## REQ-COM-064 — Communication Statistics

The software should maintain diagnostic counters for selected communication events.

Potential counters include:

- Messages received
- Messages transmitted
- Invalid messages
- Integrity failures
- Buffer overflows
- Timeouts
- Unknown message identifiers

**Verification:**  
Inspection and functional test.

---

## REQ-COM-065 — Fault Injection

The communication implementation shall support testing with intentionally malformed, delayed, repeated, dropped, and corrupted messages.

**Verification:**  
Test procedure review and execution.

---

# 15. Future Communications Requirements

## REQ-COM-066 — Transport Independence

Application-level command and telemetry handling shall not depend on a single physical transport.

**Rationale:**  
The same protocol or application behavior may later operate over UART, USB, or radio.

**Verification:**  
Architecture and code inspection.

---

## REQ-COM-067 — Ground-Station Compatibility

The architecture shall support future communication with a Stratus ground-station application.

Potential functions include:

- Live telemetry
- Parameter configuration
- Fault reporting
- Firmware information
- Data logging
- Calibration support
- Mission configuration

**Verification:**  
Architecture review.

---

## REQ-COM-068 — Radio Integration

The architecture shall permit future integration of an operational radio without requiring modification of core Flight Control algorithms.

**Verification:**  
Architecture review.

---

## REQ-COM-069 — Bidirectional Telemetry Link

The future operational link should support bidirectional communication.

**Rationale:**  
Bidirectional communication supports acknowledgment, configuration, health reporting, and command delivery.

**Verification:**  
Future design review.

---

## REQ-COM-070 — Log Download

The future communications architecture should support retrieval of stored flight or diagnostic logs.

**Verification:**  
Future design review.

---

# 16. Requirement Summary

| Requirement Range | Area |
| --- | --- |
| REQ-COM-001 through REQ-COM-008 | Development communications |
| REQ-COM-009 through REQ-COM-017 | Telemetry |
| REQ-COM-018 through REQ-COM-025 | Command reception |
| REQ-COM-026 through REQ-COM-035 | Message handling |
| REQ-COM-036 through REQ-COM-040 | Data integrity |
| REQ-COM-041 through REQ-COM-045 | Timing and performance |
| REQ-COM-046 through REQ-COM-051 | Fault handling |
| REQ-COM-052 through REQ-COM-056 | Security and safety |
| REQ-COM-057 through REQ-COM-060 | Configuration |
| REQ-COM-061 through REQ-COM-065 | Testability |
| REQ-COM-066 through REQ-COM-070 | Future expansion |

---

# 17. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Requirements Index
- **ARC-001** — Stratus System Architecture
- **SES-002** — Stratus Electrical Engineering Standard
- **REQ-FR-001** — Flight Control Functional Requirements
- **REQ-FR-002** — State Estimation Functional Requirements
- **REQ-FR-003** — Motor Output Functional Requirements
- **ADR-004** — Custom Flight Software
- **ADR-005** — Flight Stack Strategy

---

# 18. Related Documents

## Upstream

- SPEC-001
- REQ-001
- ARC-001

## Peer

- REQ-FR-001 — Flight Control
- REQ-FR-002 — State Estimation
- REQ-FR-003 — Motor Output
- FunctionalRequirements.md
- NonFunctionalRequirements.md
- Interfaces.md

## Downstream

- Communications software design
- Transport-driver implementation
- Protocol definition
- Ground-station interface definition
- Communications verification procedures