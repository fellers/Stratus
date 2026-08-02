# Stratus System Architecture

Document ID: ARC-001

Revision: 1.0

Status: Draft

Classification: Public

Project: Stratus

Author: Austin Fellows

Created: 2026-06-27

Last Updated: 2026-08-02

---

# Revision History

| Version | Date | Description | Author |
| --- | --- | --- | --- |
| 1.0 | 2026-06-27 | Initial revision | Austin Fellows |
| 1.1 | 2026-08-02 | Completed Rev A system architecture | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Architectural Principles
4. System Context
5. Subsystem Architecture
6. Hardware Architecture
7. Software Architecture
8. Execution Model
9. Data and Control Flow
10. Interface Definitions
11. Fault Handling and Safe States
12. Boot and Initialization Sequence
13. Timing Architecture
14. Memory Architecture
15. Future Architecture
16. References
17. Related Documents

---

# 1. Purpose

This document defines the system architecture of Stratus Rev A and describes the decomposition of the platform into hardware, software, mechanical, electrical, and functional subsystems.

The architecture establishes the responsibilities, boundaries, interfaces, dependencies, and data flows required to satisfy the objectives defined in SPEC-001 and the requirements indexed by REQ-001.

This document describes how the system is organized. Detailed component-selection rationale is maintained within Architecture Decision Records and Hardware Decision Records. Implementation-specific details are maintained in source code, interface documentation, engineering standards, and test artifacts.

---

# 2. Scope

This document applies to Stratus Rev A.

It defines the architecture required to support:

- Embedded flight software
- Inertial sensing
- State estimation
- Closed-loop attitude control
- Motor-command generation
- Four-motor propulsion
- Battery power distribution
- Development and debugging interfaces
- Modular mechanical integration
- Future telemetry and navigation expansion

The following capabilities remain outside the implemented scope of Rev A but are considered in the architecture:

- GPS navigation
- Position control
- Autonomous mission execution
- Computer vision
- Companion computing
- Custom flight controller PCB
- Swarm coordination

---

# 3. Architectural Principles

## 3.1 Modularity

Subsystems shall expose defined interfaces and minimize unnecessary knowledge of one another’s internal implementation.

## 3.2 Separation of Concerns

Hardware access, device drivers, state estimation, flight control, motor output, communications, and future mission functions shall remain logically separated.

## 3.3 Hardware Abstraction

Higher-level flight software shall not directly depend on processor registers, board pin assignments, or device-specific communication details.

## 3.4 Deterministic Behavior

Functions involved in sensing, estimation, control, and motor output shall execute with predictable timing and bounded behavior.

## 3.5 Safe Defaults

Outputs capable of producing motion shall default to a non-commanding state during reset, initialization, programming, communication loss, and detected critical faults.

## 3.6 Incremental Verification

Subsystems shall be independently testable before integration into the complete aircraft.

## 3.7 Replaceability

Hardware-specific implementations shall be replaceable without requiring fundamental redesign of unrelated software layers.

## 3.8 First-Principles Ownership

Core flight behavior shall be implemented and understood within the Stratus project rather than delegated to an external flight stack.

## 3.9 Progressive Complexity

Rev A shall establish a stable foundation before advanced navigation, perception, and autonomy are introduced.

---

# 4. System Context

Stratus Rev A is an autonomous aerial robotics platform that interacts with an operator, development equipment, its physical environment, and future external command systems.

## 4.1 External Actors

### Operator

The operator assembles, configures, tests, commands, and monitors the aircraft.

### Development Workstation

The development workstation builds firmware, programs the Flight Controller, supports debugging, and records test results.

### Programming and Debug Equipment

Programming and debugging equipment provides firmware download, processor control, memory inspection, breakpoints, and diagnostic access.

### Physical Environment

The physical environment provides gravitational, rotational, aerodynamic, vibrational, and atmospheric inputs measured or acted upon by the aircraft.

### Future Command System

A future radio, ground station, or autonomous mission source may provide commands and receive telemetry.

## 4.2 System Boundary

The Stratus system boundary includes:

- Airframe
- Flight Controller
- Inertial sensor
- ESC
- Motors
- Propellers
- Battery
- Aircraft wiring
- Embedded flight software
- Onboard communication interfaces

The following are external support equipment:

- Battery charger
- LiPo safety equipment
- Development workstation
- ST-Link debugger
- Logic analyzer
- Oscilloscope
- Bench power supply
- Manufacturing tools

## 4.3 System Context Diagram

text                      Development Workstation                               │                     Program / Debug / Monitor                               │                               ▼                     ┌───────────────────┐         Commands ──▶│                   │──▶ Telemetry                     │   Stratus Rev A   │  Environment ──────▶│                   │──▶ Thrust / Motion                     └───────────────────┘                               ▲                               │                          Operator 

---

# 5. Subsystem Architecture

Stratus Rev A is decomposed into the following major subsystems.

## 5.1 Flight Control

The Flight Control subsystem is responsible for:

- Receiving estimated aircraft state
- Receiving desired flight-state commands
- Calculating control corrections
- Producing axis-level control outputs
- Detecting control-related faults
- Requesting safe-state transitions when required

Flight Control shall not directly access sensor registers or generate hardware-specific ESC waveforms.

## 5.2 State Estimation

The State Estimation subsystem is responsible for:

- Receiving validated inertial measurements
- Applying calibration and coordinate transformations
- Estimating aircraft attitude
- Tracking estimator validity
- Providing timestamped state estimates
- Detecting unusable or stale measurement data

The estimator implementation may evolve without changing the external responsibility of the subsystem.

## 5.3 Sensor Acquisition

The Sensor Acquisition function is responsible for:

- Initializing sensor devices
- Scheduling or responding to sensor measurements
- Reading raw sensor data
- Validating communication success
- Applying device-level scaling
- Timestamping samples
- Reporting sensor health

Sensor Acquisition provides measurements to State Estimation through a device-independent data structure.

## 5.4 Motor Output

The Motor Output subsystem is responsible for:

- Receiving axis-level or motor-level control commands
- Applying the motor-mixing strategy
- Enforcing output limits
- Applying arming and safe-state constraints
- Generating individual motor commands
- Sending commands through the selected ESC protocol

## 5.5 Propulsion

The Propulsion subsystem consists of:

- Four-in-one ESC
- Four brushless motors
- Four propellers
- Associated power and signal wiring

It converts electrical power and motor commands into thrust and rotational moments.

## 5.6 Power Distribution

The Power Distribution subsystem is responsible for:

- Accepting battery power
- Supplying propulsion power
- Supplying regulated electronics power
- Maintaining common electrical references
- Supporting voltage monitoring
- Minimizing power-induced resets and noise

## 5.7 Communications

The Communications subsystem is responsible for:

- Firmware-programming access
- Debug access
- Development diagnostics
- Telemetry transport
- Future command-and-control transport

The architecture shall allow development communications to exist independently of future operational communications.

## 5.8 Mechanical Structure

The Mechanical Structure subsystem is responsible for:

- Supporting all components
- Maintaining component orientation
- Providing motor geometry
- Protecting wiring and electronics
- Enabling modular replacement
- Providing battery retention
- Supporting future payloads

Mechanical implementation shall conform to SES-001.

## 5.9 System Supervision

The System Supervision function is responsible for:

- Tracking initialization status
- Managing system operating states
- Enforcing arming conditions
- Detecting critical faults
- Coordinating safe-state transitions
- Providing health information to other subsystems

---

# 6. Hardware Architecture

## 6.1 Flight Controller

The Flight Controller is based on an STM32H743-class microcontroller platform.

Its responsibilities include:

- Executing embedded flight software
- Acquiring sensor data
- Running estimation and control algorithms
- Generating motor-control outputs
- Managing communications
- Monitoring system health
- Supporting programming and debugging

The selected development board is a Rev A implementation detail documented in the applicable BOM and decision record.

## 6.2 Inertial Measurement Unit

The primary inertial sensor is an ICM-20602 six-axis IMU.

It provides:

- Three-axis angular-rate measurements
- Three-axis acceleration measurements

The IMU communicates with the Flight Controller over SPI.

The architecture reserves support for an interrupt signal so that future software may use data-ready-driven acquisition.

## 6.3 Electronic Speed Controller

The Aero Selfie 45A four-in-one ESC provides four independent motor-control channels.

The ESC receives:

- Battery-level power
- Individual motor-command signals
- Common ground reference

The ESC supplies three-phase power to each motor.

## 6.4 Motors and Propellers

Four HappyModel EX1404 motors and Gemfan Hurricane 3520 propellers form the Rev A thrust-generation hardware.

Each motor occupies a defined aircraft position and shall have a documented:

- Motor number
- Rotation direction
- ESC channel
- Output signal
- Physical connector or solder location

## 6.5 Battery and Primary Power

Rev A uses a 4S 850 mAh LiPo battery with an XT30 connector.

The battery supplies primary propulsion power and indirectly supplies regulated electronics power.

Battery voltage may be monitored by the Flight Controller through an appropriately scaled sensing interface in a future implementation.

## 6.6 Debug and Programming

The architecture supports:

- USB DFU for firmware programming and recovery
- SWD for debugging and direct programming
- UART for development diagnostics
- USB for future development or communication functions

SWD shall remain accessible during Rev A development.

## 6.7 Hardware Block Diagram

text                    4S LiPo Battery                          │                          ▼                 ┌─────────────────┐                 │ 4-in-1 ESC /    │                 │ Power Interface │                 └───────┬─────────┘                         │           ┌─────────────┼─────────────┐           ▼             ▼             ▼        Motor 1       Motor 2       Motors 3–4                           ▲                          │ Motor Commands                          │                 ┌────────┴─────────┐                 │ Flight Controller│                 │   STM32H743      │                 └───┬─────┬─────┬─┘                     │     │     │                   SPI    SWD   UART/USB                     │     │     │                     ▼     ▼     ▼                   IMU   Debug  Development 

---

# 7. Software Architecture

The Stratus flight software shall use a layered architecture.

## 7.1 Platform Layer

The Platform layer contains processor- and board-specific functionality.

Responsibilities include:

- Startup
- Clock configuration
- Interrupt configuration
- GPIO
- Timer access
- SPI peripheral access
- UART peripheral access
- USB access
- Reset and watchdog functions
- Board pin definitions

Higher layers shall not directly depend on STM32 register addresses.

## 7.2 Driver Layer

The Driver layer contains device-specific implementations.

Examples include:

- ICM-20602 driver
- ESC protocol driver
- Battery-monitor driver
- Debug-transport driver

Drivers depend on Platform interfaces but do not depend on Flight Control or State Estimation.

## 7.3 Service Layer

The Service layer provides reusable system capabilities such as:

- Timekeeping
- Scheduling
- Logging
- Health monitoring
- Parameter management
- Calibration
- Fault reporting

## 7.4 Application Layer

The Application layer contains system behavior.

Primary application components include:

- Sensor Acquisition
- State Estimation
- Flight Control
- Motor Output
- System Supervision
- Communications management

## 7.5 Domain Types

Shared domain types shall represent information passed among subsystems.

Examples include:

- ImuSample
- AttitudeEstimate
- FlightSetpoint
- ControlOutput
- MotorCommands
- SystemHealth
- FaultRecord
- Timestamp

Domain types shall not embed hardware register details or driver handles.

## 7.6 Dependency Direction

Dependencies shall flow downward:

text Application     ↓ Services     ↓ Drivers     ↓ Platform     ↓ Hardware 

Lower layers shall not depend on higher layers.

## 7.7 C++ Production Architecture

The long-lived Stratus firmware is intended to use modern embedded C++.

The production implementation should favor:

- Strong types
- Explicit ownership
- Compile-time configuration
- Interfaces at hardware boundaries
- Deterministic object lifetimes
- Static allocation
- Minimal global mutable state
- Unit-testable algorithm components

The initial C bring-up project is a hardware-learning and verification environment rather than the final firmware architecture.

## 7.8 Restricted Runtime Features

Unless later justified, production embedded C++ shall avoid:

- Exceptions
- Run-time type information
- Unbounded dynamic allocation
- Hidden heap use
- Uncontrolled recursion
- Blocking operations in time-critical paths
- Standard-library facilities with uncertain memory or timing behavior

---

# 8. Execution Model

## 8.1 Rev A Execution Strategy

Rev A shall begin with a cooperative, time-triggered execution model.

A simple scheduler shall invoke periodic functions according to defined rates.

An RTOS is not required for initial Rev A operation.

## 8.2 Interrupt Responsibilities

Interrupt service routines shall perform only time-critical work.

Typical ISR responsibilities include:

- Capturing timestamps
- Moving peripheral data
- Recording event flags
- Advancing DMA state
- Acknowledging hardware interrupts

Complex estimation, control, parsing, and logging shall occur outside ISR context.

## 8.3 Main Execution Loop

The main loop shall:

- Service scheduled tasks
- Process pending events
- Execute background diagnostics
- Monitor health
- Avoid uncontrolled blocking

Conceptual structure:

text Initialize platform Initialize drivers Run self-tests Enter disarmed state  while running:     update scheduler time     execute due tasks     process faults     service communications     enforce system state 

## 8.4 Task Categories

Expected task categories include:

| Task | Relative Frequency | Responsibility |
| --- | --- | --- |
| Sensor acquisition | High | Acquire and validate IMU data |
| State estimation | High | Update attitude estimate |
| Flight control | High | Compute control outputs |
| Motor output | High | Update ESC commands |
| System supervision | Medium | Track health and operating state |
| Communications | Medium or low | Process diagnostics and telemetry |
| Status indication | Low | Heartbeat and status signaling |
| Logging | Low or event-driven | Record selected diagnostic data |

Exact rates shall be established through measurement and verification.

## 8.5 Blocking Behavior

Time-critical execution paths shall not wait indefinitely for:

- Peripheral communication
- User input
- Logging output
- Dynamic resources
- External responses

Timeouts shall be used where hardware or communications can fail to respond.

---

# 9. Data and Control Flow

## 9.1 Primary Flight Data Flow

text IMU Hardware     ↓ SPI Platform Interface     ↓ ICM-20602 Driver     ↓ Sensor Acquisition     ↓ Validated ImuSample     ↓ State Estimation     ↓ AttitudeEstimate     ↓ Flight Control     ↓ ControlOutput     ↓ Motor Mixer     ↓ MotorCommands     ↓ ESC Driver     ↓ ESC     ↓ Motors and Propellers 

## 9.2 Command Flow

Rev A command input may initially consist of development-defined setpoints.

Future command flow is expected to be:

text Operator / Ground System     ↓ Communication Transport     ↓ Command Validation     ↓ Flight Mode / Setpoint Generation     ↓ Flight Control 

Commands shall be validated before they affect flight outputs.

## 9.3 Health Flow

Each subsystem shall expose sufficient health information for System Supervision.

text Drivers / Services / Applications               ↓          Health Status               ↓       System Supervision               ↓  Safe State / Diagnostic Reporting 

## 9.4 Timestamping

Sensor data and state estimates shall use a monotonic system time source.

Timing data shall allow the software to determine:

- Sample age
- Control-loop interval
- Missed deadlines
- Stale estimates
- Communication timeouts

## 9.5 Ownership

Data passed between subsystems shall have clear ownership and lifetime.

Time-critical paths should prefer:

- Value types
- Fixed-size buffers
- Explicit references
- Single-producer/single-consumer structures where appropriate

Uncontrolled sharing of mutable global data shall be avoided.

---

# 10. Interface Definitions

## 10.1 Flight Controller to IMU

| Attribute | Definition |
| --- | --- |
| Interface | SPI |
| Controller | Flight Controller |
| Peripheral | ICM-20602 |
| Logic level | 3.3 V-compatible |
| Required signals | SCK, MISO, MOSI, CS, GND, power |
| Optional signal | Data-ready interrupt |
| Ownership | Sensor driver |
| Failure behavior | Report invalid or unavailable sensor data |

The SPI mode, maximum operating rate, startup rate, and timing constraints shall be confirmed from the actual sensor documentation and validated during bring-up.

## 10.2 Flight Controller to ESC

| Attribute | Definition |
| --- | --- |
| Interface | Individual digital motor-control outputs |
| Channels | Four |
| Ground reference | Shared |
| Ownership | Motor Output subsystem |
| Default state | Non-commanding |
| Failure behavior | Transition outputs to predefined safe state |

The initial protocol may be a simple supported ESC command format. Migration to a higher-performance digital protocol shall not require redesign of Flight Control.

## 10.3 Battery to ESC

| Attribute | Definition |
| --- | --- |
| Interface | XT30 primary power |
| Source | 4S LiPo |
| Maximum expected voltage | 16.8 V |
| Ownership | Power Distribution |
| Safety requirement | Correct polarity and insulated conductors |

## 10.4 SWD Interface

| Signal | Purpose |
| --- | --- |
| SWDIO | Bidirectional debug data |
| SWCLK | Debug clock |
| GND | Common reference |
| VTref / 3.3 V | Target-voltage reference or power, depending on debugger |
| NRST | Optional external reset |

Debugger power behavior shall be verified before simultaneous connection with other power sources.

## 10.5 Development UART

The development UART shall provide diagnostic and bring-up communication.

Initial configuration should use:

- 115200 baud
- 8 data bits
- No parity
- 1 stop bit

The final pin assignment shall be recorded in the board-interface documentation.

## 10.6 Mechanical Interfaces

Mechanical interfaces shall comply with SES-001.

Each mounted electronics module shall define:

- Mounting pattern
- Fastener type
- Orientation
- Component envelope
- Connector-access envelope
- Cable exit
- Required clearance

## 10.7 Electrical Interfaces

Wiring, connector, grounding, and routing practices shall comply with SES-002.

## 10.8 Software Interfaces

Software interfaces shall:

- Use explicit input and output types
- Avoid exposing peripheral handles above the Driver layer
- Report success, failure, or health state
- Define behavior for unavailable data
- Avoid hidden blocking
- Document ownership and lifetime
- Remain testable without physical hardware where practical

---

# 11. Fault Handling and Safe States

## 11.1 Fault Categories

Faults shall be categorized by severity.

| Severity | Description | Expected Response |
| --- | --- | --- |
| Informational | Noncritical diagnostic condition | Record or report |
| Degraded | Capability reduced but controlled operation may continue | Limit functionality and report |
| Critical | Safe flight cannot be assured | Enter safe state |
| Fatal | Software or hardware integrity is lost | Disable motor commands and reset or halt safely |

## 11.2 Critical Fault Examples

Critical faults may include:

- Loss of required IMU communication
- Invalid or stale attitude estimate
- Control-loop deadline failure
- Corrupted configuration required for flight
- Invalid motor-command state
- Undervoltage below safe operation threshold
- Watchdog timeout
- Unrecoverable processor fault

## 11.3 Safe State

The minimum Rev A safe state shall:

- Prevent active motor commands
- Maintain motor outputs at the defined non-commanding level
- Reject arming
- Record the detected fault where practical
- Indicate fault status through available diagnostics
- Require an explicit reset or recovery procedure where appropriate

A safe state does not guarantee safe airborne recovery. Rev A fault handling prioritizes preventing uncontrolled propulsion.

## 11.4 Arming Preconditions

The system shall not enter an armed state unless required checks pass.

Expected preconditions include:

- Initialization complete
- IMU communication valid
- State estimate valid
- No critical faults active
- Motor outputs initialized
- Command source valid
- Battery condition acceptable where monitoring exists

## 11.5 Watchdog

A hardware watchdog should be introduced once the main execution model is stable.

The watchdog shall only be serviced when critical software functions have demonstrated expected progress.

## 11.6 Assertions

Development builds may use assertions to detect invalid software assumptions.

Production behavior shall not depend solely on assertions for safety-critical fault handling.

---

# 12. Boot and Initialization Sequence

The expected startup sequence is:

1. Processor reset
2. Startup assembly executes
3. Stack and memory sections are initialized
4. FPU is enabled
5. System clock is configured
6. Low-level Platform interfaces are initialized
7. GPIO enters defined safe states
8. Timebase is initialized
9. Communications used for diagnostics are initialized
10. SPI is initialized at a sensor-compatible startup rate
11. IMU identity is verified
12. IMU configuration is applied
13. Sensor measurements are validated
14. State Estimation initializes
15. Flight Control initializes
16. Motor Output initializes in a non-commanding state
17. System self-tests are evaluated
18. System enters the disarmed-ready state

If a required initialization step fails, startup shall not proceed to an armed-capable state.

---

# 13. Timing Architecture

## 13.1 Monotonic Timebase

The system shall provide a monotonic high-resolution timebase suitable for:

- Sensor timestamps
- Control-loop timing
- Scheduler operation
- Timeout detection
- Performance measurement

## 13.2 Initial Timing Targets

The following are initial architectural targets rather than released performance requirements:

| Function | Initial Target |
| --- | --- |
| IMU acquisition | 1 kHz |
| State estimation | 1 kHz |
| Flight control | 500 Hz to 1 kHz |
| Motor output | Match control loop or protocol requirement |
| System supervision | 50–100 Hz |
| Telemetry and diagnostics | 10–100 Hz |
| Status indication | 1–10 Hz |

Final rates shall be selected based on:

- Sensor capability
- Control-system analysis
- CPU utilization
- Measured execution time
- ESC protocol
- Noise behavior
- Verification results

## 13.3 Deadline Monitoring

The system should detect:

- Missed periodic executions
- Excessive execution duration
- Stale sensor data
- Stale state estimates
- Motor-output update failures

## 13.4 Delay Loops

Busy-wait delay loops may be used during initial bring-up only.

Released flight software shall use hardware-backed timing rather than uncalibrated instruction-count delay loops.

---

# 14. Memory Architecture

## 14.1 General Policy

Memory placement shall be deliberate on the STM32H743 because not all memory regions provide identical behavior or peripheral accessibility.

## 14.2 Static Allocation

Flight-critical objects and buffers shall use static or automatic allocation with bounded lifetime.

Dynamic allocation after startup should be prohibited unless a later decision record establishes a controlled allocator and justification.

## 14.3 Stack

Stack usage shall be bounded and reviewed.

Large buffers shall not be placed on the stack without explicit analysis.

## 14.4 DMA Buffers

Buffers used by DMA shall be placed in DMA-accessible memory and managed consistently with the STM32H7 data-cache architecture.

Cache cleaning, invalidation, or noncached placement shall be used where required.

## 14.5 Fast Memory

Time-critical algorithm state may be placed in tightly coupled memory where justified and compatible with access requirements.

## 14.6 Persistent Configuration

Rev A may initially compile configuration values into firmware.

Future persistent configuration shall include:

- Versioning
- Validation
- Default values
- Corruption detection
- Controlled update behavior

---

# 15. Future Architecture

## 15.1 Rev B

Potential architectural expansion includes:

- Larger 5-inch airframe
- Increased payload capability
- Additional sensing
- Improved communication hardware
- Longer endurance

The validated software subsystem boundaries should remain intact.

## 15.2 Rev C

Rev C is expected to introduce a custom Flight Controller PCB.

The custom PCB should preserve the established software abstractions while integrating:

- MCU
- IMU
- Power regulation
- Debug interface
- Sensor connectors
- ESC interfaces
- Voltage monitoring
- Additional expansion interfaces

## 15.3 Navigation Expansion

Future navigation architecture may add:

- GNSS
- Magnetometer
- Barometer
- Position estimation
- Guidance
- Waypoint management
- Return-to-home behavior

These capabilities shall build above the existing attitude-control architecture.

## 15.4 Perception Expansion

Future perception architecture may add:

- Camera
- Optical flow
- Range sensing
- Obstacle detection
- Companion processor

The Flight Controller should remain responsible for deterministic low-level flight stabilization even when a companion processor is introduced.

## 15.5 Communication Expansion

Future operational communications may include:

- Radio command link
- Telemetry link
- Ground station
- Configuration protocol
- Mission upload
- Log download

Transport-specific logic shall remain isolated from flight behavior.

---

# 16. References

- SPEC-001 — Stratus Rev A System Specification
- REQ-001 — Stratus Rev A Requirements Specification
- BOM-001 — Bill of Materials
- SES-001 — Stratus Mechanical Engineering Standard
- SES-002 — Stratus Electrical Engineering Standard
- ADR-001 — STM32H743 Architecture
- ADR-002 — Rev A Platform Size
- ADR-003 — Modular Airframe Architecture
- ADR-004 — Custom Flight Software
- ADR-005 — Flight Stack Strategy
- HDR-001 — ICM-20602 IMU
- HDR-002 — HappyModel EX1404 Motors
- HDR-003 — Aero Selfie 45A 4-in-1 ESC
- HDR-004 — Gemfan Hurricane 3520 Propellers
- HDR-005 — 4S 850mAh Power System
- HDR-006 — Mechanical Hardware Standard
- HDR-007 — Wiring Materials Standard

---

# 17. Related Documents

## Upstream

- SPEC-001 — Stratus Rev A System Specification
- REQ-001 — Stratus Rev A Requirements Specification

## Peer

- BOM-001 — Bill of Materials
- SES-001 — Mechanical Engineering Standard
- SES-002 — Electrical Engineering Standard
- Requirements Traceability Matrix

## Supporting

- ADR Series
- HDR Series
- Functional Requirement Specifications
- Hardware Requirement Specifications
- Software Requirement Specifications
- Mechanical Requirement Specifications
- Electrical Requirement Specifications