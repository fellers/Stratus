# Stratus Rev A Interface Control Document

**Document ID:** ICD-001  
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
| 1.0 | 2026-08-02 | Initial Rev A interface-control baseline | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Interface-Control Principles
4. System Interface Overview
5. Coordinate Systems and Conventions
6. Flight Controller Interface
7. Debug and Programming Interfaces
8. IMU Interface
9. ESC and Motor-Control Interface
10. Power Interfaces
11. Development UART Interface
12. USB Interface
13. Future Communications Interface
14. Software Interfaces
15. Mechanical Interfaces
16. Harness and Connector Identification
17. Startup and Safe-State Requirements
18. Interface Verification
19. Interface Allocation Tables
20. Open Interface Decisions
21. Change Control
22. References
23. Related Documents

---

# 1. Purpose

This document defines the controlled interfaces for Stratus Rev A.

It provides the authoritative implementation-level description of how Stratus subsystems connect and exchange:

- Electrical power
- Digital signals
- Sensor measurements
- Motor commands
- Diagnostic data
- Configuration data
- Mechanical loads
- Coordinate-frame information

Requirements documents define what the system must provide.

The system architecture defines how responsibilities are divided among subsystems.

This Interface Control Document defines the exact boundaries, signal assignments, data formats, ownership, and safe states used to connect those subsystems.

---

# 2. Scope

This document applies to the following Stratus Rev A interfaces:

- Flight Controller power
- Flight Controller pin assignments
- SWD programming and debugging
- USB firmware programming and recovery
- IMU SPI communication
- IMU interrupt signaling
- ESC motor-command outputs
- ESC power and grounding
- Motor channel assignments
- Development UART
- Battery connection
- Regulated electronics power
- Ground references
- Software data interfaces
- Mechanical mounting interfaces
- Aircraft and sensor coordinate systems
- Future telemetry or command-radio expansion

This document does not replace:

- Requirements specifications
- System architecture
- Wiring workmanship standards
- Mechanical manufacturing standards
- Hardware-selection decision records
- Communication protocol specifications

---

# 3. Interface-Control Principles

## 3.1 Single Authoritative Definition

Each controlled interface shall have one authoritative definition.

Signal names, pin assignments, connector pinouts, data types, coordinate conventions, and safe states shall not be independently redefined in multiple documents.

---

## 3.2 Placeholder Policy

Unverified interface values shall be marked:

```text
TBD — To Be Determined
TBC — To Be Confirmed
```

A placeholder shall not be treated as an approved wiring or firmware assignment.

---

## 3.3 No Pin Assignment by Assumption

Microcontroller pins and peripheral instances shall not be assigned solely from generic STM32H743 capability.

Assignments shall be verified against:

- The exact Flight Controller or development-board schematic
- The exact STM32H743 package
- Board routing
- Existing onboard functions
- Voltage compatibility
- Timer and DMA availability
- Debug-interface requirements

---

## 3.4 Interface Ownership

Each interface shall identify:

- Producing subsystem
- Consuming subsystem
- Signal or data direction
- Initialization owner
- Error-detection owner
- Safe-state owner

---

## 3.5 Controlled Changes

Changes to a released interface shall include review of:

- Hardware wiring
- Firmware configuration
- Software drivers
- Mechanical routing
- Requirements
- Architecture
- Verification procedures
- Traceability

---

# 4. System Interface Overview

```text
                    External Development Computer
                         │        │        │
                         │ SWD    │ USB    │ UART
                         ▼        ▼        ▼
                 ┌─────────────────────────────┐
                 │      Flight Controller      │
                 │         STM32H743           │
                 └─────────────────────────────┘
                      │          │          │
                  SPI │     ESC  │     ADC/ │ Future
                      │   Signals│     UART │ Interfaces
                      ▼          ▼          ▼
                 ┌────────┐  ┌─────────┐  ┌─────────────┐
                 │  IMU   │  │ 4-in-1  │  │ Navigation, │
                 │ICM-20602│ │   ESC   │  │ Radio, etc. │
                 └────────┘  └─────────┘  └─────────────┘
                                  │
                           ┌──────┼──────┐
                           ▼      ▼      ▼
                         Motor  Motor  Motors
                           1      2      3–4

        4S LiPo Battery
               │
               ├──────────────▶ 4-in-1 ESC
               │
               └──────────────▶ Regulated Electronics Supply
                                      │
                                      ▼
                              Flight Controller and IMU
```

---

# 5. Coordinate Systems and Conventions

## 5.1 Aircraft Coordinate System

Stratus shall use the following aircraft body-axis convention:

| Axis | Positive Direction |
| --- | --- |
| X | Forward |
| Y | Right |
| Z | Down |

This convention shall be used by:

- State estimation
- Flight control
- Sensor transformations
- Motor mixing
- Mechanical drawings
- Telemetry
- Test documentation

---

## 5.2 Positive Rotations

Positive angular rotations shall follow the right-hand rule.

| Rotation | Axis |
| --- | --- |
| Roll | X axis |
| Pitch | Y axis |
| Yaw | Z axis |

The exact signs used by sensor-driver outputs and control commands shall be verified during axis-orientation testing.

---

## 5.3 IMU Sensor Frame

The native ICM-20602 sensor axes shall be documented relative to the breakout board and aircraft frame.

| Sensor Axis | Breakout-Board Direction | Aircraft-Axis Mapping | Sign |
| --- | --- | --- | --- |
| IMU X | TBC | TBC | TBC |
| IMU Y | TBC | TBC | TBC |
| IMU Z | TBC | TBC | TBC |

The firmware shall apply a documented transformation from the IMU sensor frame to the aircraft body frame.

---

## 5.4 Motor Numbering Convention

Motor numbering shall be based on the aircraft viewed from above with the aircraft nose pointing forward.

The final motor numbering and rotation directions are not yet approved.

| Motor | Physical Location | Required Rotation | ESC Channel | Status |
| --- | --- | --- | --- | --- |
| Motor 1 | TBD | TBD | TBD | Open |
| Motor 2 | TBD | TBD | TBD | Open |
| Motor 3 | TBD | TBD | TBD | Open |
| Motor 4 | TBD | TBD | TBD | Open |

Motor numbering shall be identical in:

- CAD
- Wiring documentation
- Firmware configuration
- Motor mixer
- Test procedures
- Telemetry
- Flight logs

---

# 6. Flight Controller Interface

## 6.1 Flight Controller Identification

| Item | Value |
| --- | --- |
| Processor family | STM32H743-class |
| Exact processor part number | TBC |
| Exact development board or module | TBC |
| Processor package | TBC |
| Logic voltage | TBC |
| Primary firmware environment | TBC |
| Board schematic revision | TBC |

The exact Flight Controller hardware shall be recorded before final pin allocation.

---

## 6.2 Flight Controller Interface Categories

The Flight Controller shall provide interfaces for:

- Target power
- Ground
- SWD
- Reset
- USB
- IMU SPI
- IMU interrupt
- Four motor-command outputs
- Development UART
- Battery monitoring, when implemented
- Future radio or telemetry hardware

---

## 6.3 Master Pin-Allocation Table

No entry in this table shall be used for wiring until its status is **Approved**.

| Function | Peripheral | MCU Pin | Board Connector or Header | Direction | Reset State | Status |
| --- | --- | --- | --- | --- | --- | --- |
| SWDIO | SWD | TBC | TBC | Bidirectional | Debug-defined | Open |
| SWCLK | SWD | TBC | TBC | Input | Debug-defined | Open |
| NRST | Reset | TBC | TBC | Input | Assertable | Open |
| USB D+ | USB | TBC | TBC | Bidirectional | Inactive | Open |
| USB D− | USB | TBC | TBC | Bidirectional | Inactive | Open |
| IMU SCK | SPI | TBC | TBC | Output | Defined inactive | Open |
| IMU MOSI | SPI | TBC | TBC | Output | Defined inactive | Open |
| IMU MISO | SPI | TBC | TBC | Input | High impedance | Open |
| IMU CS | GPIO | TBC | TBC | Output | High/inactive | Open |
| IMU interrupt | EXTI/GPIO | TBC | TBC | Input | Input | Open |
| Motor 1 command | Timer | TBC | TBC | Output | Non-commanding | Open |
| Motor 2 command | Timer | TBC | TBC | Output | Non-commanding | Open |
| Motor 3 command | Timer | TBC | TBC | Output | Non-commanding | Open |
| Motor 4 command | Timer | TBC | TBC | Output | Non-commanding | Open |
| UART TX | UART | TBC | TBC | Output | Idle high | Open |
| UART RX | UART | TBC | TBC | Input | Input | Open |
| Battery voltage sense | ADC | TBC | TBC | Input | Analog input | Deferred |
| Future communications TX | TBC | TBC | TBC | Output | TBC | Reserved |
| Future communications RX | TBC | TBC | TBC | Input | TBC | Reserved |

---

# 7. Debug and Programming Interfaces

## 7.1 SWD Interface

The primary development and debugging interface shall be Serial Wire Debug.

The minimum required SWD signals are:

| Signal | Description | Direction Relative to Target |
| --- | --- | --- |
| SWDIO | Serial-wire data | Bidirectional |
| SWCLK | Serial-wire clock | Input |
| GND | Electrical reference | Reference |
| VTREF | Target-voltage reference | Output from target reference |
| NRST | Target reset | Input, recommended |

---

## 7.2 SWD Connector Definition

| Connector Position | Signal | Voltage or Function | Status |
| --- | --- | --- | --- |
| 1 | VTREF | Target logic-voltage reference | TBC |
| 2 | SWDIO | Serial-wire data | TBC |
| 3 | GND | Ground | TBC |
| 4 | SWCLK | Serial-wire clock | TBC |
| 5 | NRST | Target reset | TBC |

The final connector family, keying, orientation, and numbering shall be documented before harness construction.

---

## 7.3 ST-Link Connection

Rev A development shall support connection to a genuine ST-Link debugger, including the ST-Link interface available on the NUCLEO-F401RE development board when configured for external-target debugging.

The target and debugger shall share:

- Ground
- Target-voltage reference
- SWDIO
- SWCLK
- Reset where used

The debugger shall not unintentionally power the target through an undocumented path.

---

## 7.4 SWD Safe Behavior

Connecting, disconnecting, halting, resetting, or programming through SWD shall not intentionally command motor rotation.

Motor-control outputs shall remain non-commanding during:

- Processor reset
- Firmware erase
- Firmware programming
- Debugger attachment
- Processor halt
- Early startup

---

## 7.5 Bootloader Interface

| Item | Value |
| --- | --- |
| Bootloader type | STM32 system bootloader |
| Intended use | Firmware recovery or alternate programming |
| Entry method | TBC |
| BOOT pin or option-byte behavior | TBC |
| Required USB or UART interface | TBC |
| Verification status | Open |

---

# 8. IMU Interface

## 8.1 IMU Identification

| Item | Value |
| --- | --- |
| Device | ICM-20602 |
| Interface | SPI |
| Supply voltage | TBC from exact module documentation |
| Logic voltage | TBC |
| Device identity register | WHO_AM_I |
| Expected identity value | TBC from authoritative datasheet |
| Interrupt output used | TBC |

---

## 8.2 IMU SPI Signals

| Signal | Producer | Consumer | Direction | Required Default |
| --- | --- | --- | --- | --- |
| SCK | Flight Controller | IMU | FC to IMU | Inactive clock state |
| MOSI | Flight Controller | IMU | FC to IMU | Defined inactive state |
| MISO | IMU | Flight Controller | IMU to FC | High impedance when deselected |
| CS | Flight Controller | IMU | FC to IMU | High/inactive |
| INT | IMU | Flight Controller | IMU to FC | TBC |
| VCC | Power subsystem | IMU | Power | Within approved range |
| GND | Ground system | IMU | Reference | Common logic reference |

---

## 8.3 SPI Configuration

| Parameter | Startup Value | Operational Value | Status |
| --- | --- | --- | --- |
| SPI peripheral | TBC | TBC | Open |
| SPI mode | TBC | TBC | Open |
| Clock polarity | TBC | TBC | Open |
| Clock phase | TBC | TBC | Open |
| Bit order | Most significant bit first, TBC | Same | Open |
| Word length | 8 bits, TBC | Same | Open |
| Initialization clock rate | TBC | Not applicable | Open |
| Maximum operational clock rate | TBC | TBC | Open |
| Chip-select polarity | Active low, TBC | Same | Open |
| Transfer timeout | TBC | TBC | Open |

Values shall be verified against the authoritative ICM-20602 documentation and the exact breakout module.

---

## 8.4 IMU Initialization Ownership

The IMU driver shall own:

- Device reset
- Device identity verification
- Register configuration
- Configuration readback
- Data acquisition
- Communication timeout handling
- Sample validity
- Sensor error reporting

The State Estimation subsystem shall not directly access SPI registers.

---

## 8.5 IMU Sample Software Interface

A validated IMU sample should use an interface equivalent to:

```cpp
struct ImuSample {
    float angular_rate_rad_s[3];
    float acceleration_m_s2[3];
    std::uint64_t timestamp_us;
    bool valid;
};
```

The exact production type may differ, but shall define:

- Units
- Coordinate frame
- Sign convention
- Timestamp source
- Validity
- Ownership

---

## 8.6 IMU Failure Behavior

The IMU interface shall report failure when:

- Device identity is incorrect
- Initialization fails
- Communication times out
- Data is stale
- Received data is invalid
- Required configuration cannot be confirmed

Invalid IMU data shall not be silently presented as valid state-estimation input.

---

# 9. ESC and Motor-Control Interface

## 9.1 ESC Identification

| Item | Value |
| --- | --- |
| Device | Aero Selfie 45A four-in-one ESC |
| Channel count | Four |
| Battery compatibility | 4S, subject to exact rating verification |
| Command protocol | TBC |
| Logic voltage compatibility | TBC |
| Telemetry capability | TBC |
| Firmware family | TBC |

---

## 9.2 Motor-Control Signals

| Signal | Producer | Consumer | Direction | Safe State |
| --- | --- | --- | --- | --- |
| Motor 1 command | Flight Controller | ESC channel TBC | Output | Non-commanding |
| Motor 2 command | Flight Controller | ESC channel TBC | Output | Non-commanding |
| Motor 3 command | Flight Controller | ESC channel TBC | Output | Non-commanding |
| Motor 4 command | Flight Controller | ESC channel TBC | Output | Non-commanding |
| Signal ground | Ground system | ESC | Reference | Connected |

---

## 9.3 ESC Protocol Configuration

| Parameter | Value | Status |
| --- | --- | --- |
| Protocol | TBD |
| Timer peripheral or peripherals | TBD |
| Timer channels | TBD |
| Update rate | TBD |
| Minimum command | TBD |
| Maximum command | TBD |
| Disarmed command | TBD |
| Startup command | Non-commanding |
| Signal polarity | TBD |
| Telemetry return | Deferred or TBD |

The selected protocol shall be documented before firmware implementation is treated as flight-ready.

---

## 9.4 Motor Mapping

| Logical Motor | Physical Position | ESC Channel | Timer Channel | Rotation | Propeller Type | Status |
| --- | --- | --- | --- | --- | --- | --- |
| Motor 1 | TBD | TBD | TBD | TBD | TBD | Open |
| Motor 2 | TBD | TBD | TBD | TBD | TBD | Open |
| Motor 3 | TBD | TBD | TBD | TBD | TBD | Open |
| Motor 4 | TBD | TBD | TBD | TBD | TBD | Open |

Motor mapping shall be verified without propellers installed.

---

## 9.5 Motor Command Software Interface

A motor-command interface should be equivalent to:

```cpp
struct MotorCommands {
    float motor_1;
    float motor_2;
    float motor_3;
    float motor_4;
    std::uint64_t timestamp_us;
    bool enabled;
};
```

The final interface shall define:

- Command range
- Units or normalization
- Saturation behavior
- Timestamp semantics
- Armed-state behavior
- Invalid-value handling

---

## 9.6 ESC Failure Behavior

When motor-output validity is lost, the interface shall transition to the defined non-commanding state.

Conditions include:

- Disarmed system state
- Critical system fault
- Invalid numeric command
- Stale control output
- Processor reset
- Failed output-driver initialization

---

# 10. Power Interfaces

## 10.1 Battery Interface

| Item | Value |
| --- | --- |
| Battery chemistry | Lithium polymer |
| Battery configuration | 4S |
| Nominal voltage | 14.8 V |
| Maximum charged voltage | 16.8 V |
| Baseline capacity | Approximately 850 mAh |
| Primary connector | XT30 |
| Polarity convention | Positive and ground, physically polarized |
| Battery monitoring | Planned or deferred |

---

## 10.2 Power Distribution

```text
4S Battery
    │
    ├──▶ Four-in-One ESC
    │       └──▶ Motors 1–4
    │
    └──▶ Regulated Electronics Supply
            ├──▶ Flight Controller
            ├──▶ IMU
            └──▶ Future low-power electronics
```

---

## 10.3 Power-Rail Table

| Rail | Nominal Voltage | Source | Loads | Current Capacity | Status |
| --- | --- | --- | --- | --- | --- |
| VBAT | 14.8 V nominal, 16.8 V maximum | 4S LiPo | ESC and regulator input | TBC | Defined |
| Flight Controller input | TBC | Regulated source | Flight Controller | TBC | Open |
| 3.3 V logic | TBC | Flight Controller or regulator | MCU and logic | TBC | Open |
| IMU supply | TBC | Flight Controller or regulator | ICM-20602 module | TBC | Open |
| Future accessory rail | TBC | TBC | Radio or sensors | TBC | Reserved |

---

## 10.4 Grounding

The following shall share a valid common reference unless explicitly isolated:

- Flight Controller
- IMU
- ESC command interface
- Development UART
- SWD debugger
- Future non-isolated communications devices

High-current motor and battery returns shall be arranged to reduce interference with sensor and logic references.

---

## 10.5 Multiple Power Sources

Before simultaneously connecting USB, debugger power, bench power, and aircraft power, the permitted power paths shall be verified.

The following shall be documented for each connector:

- Whether it supplies power
- Whether it receives power
- Whether it only senses voltage
- Whether back-powering is possible
- Whether simultaneous connection is permitted

---

# 11. Development UART Interface

## 11.1 UART Purpose

The development UART shall support:

- Startup diagnostics
- Fault messages
- System-state messages
- Sensor observations
- Development telemetry
- Command and parser testing

It is not automatically considered a secure operational control interface.

---

## 11.2 UART Configuration

| Parameter | Default |
| --- | --- |
| Peripheral | TBC |
| Flight Controller TX pin | TBC |
| Flight Controller RX pin | TBC |
| Baud rate | 115200 baud |
| Data bits | 8 |
| Parity | None |
| Stop bits | 1 |
| Flow control | None |
| Logic voltage | TBC |
| Connector | TBC |

---

## 11.3 UART Signal Direction

| Signal | Producer | Consumer |
| --- | --- | --- |
| FC_TX | Flight Controller | External adapter RX |
| FC_RX | External adapter TX | Flight Controller |
| GND | Common reference | Both |

The external adapter shall use logic levels compatible with the Flight Controller.

A true RS-232 voltage interface shall not be connected directly to MCU UART pins.

---

## 11.4 UART Failure Behavior

A disconnected, stalled, or congested UART shall not indefinitely block:

- Sensor acquisition
- State estimation
- Flight control
- Motor-output updates
- System supervision

---

# 12. USB Interface

## 12.1 USB Purpose

USB may support:

- Firmware programming
- Device Firmware Upgrade
- Recovery
- Development communication
- Future configuration tools

The exact Rev A USB functions shall be documented after Flight Controller hardware confirmation.

---

## 12.2 USB Definition

| Item | Value |
| --- | --- |
| USB peripheral | TBC |
| Connector type | TBC |
| USB D+ pin | TBC |
| USB D− pin | TBC |
| VBUS behavior | TBC |
| Target-powered or bus-powered behavior | TBC |
| DFU support | Planned |
| Virtual COM support | TBC |

---

# 13. Future Communications Interface

## 13.1 Reserved Interface

The hardware and software architecture shall reserve a transport interface suitable for a future operational command and telemetry link.

Potential transports include:

- UART
- SPI
- USB
- CAN
- Another approved digital interface

---

## 13.2 Future Radio Interface Table

| Item | Value |
| --- | --- |
| Radio device | TBD |
| Transport | TBD |
| Peripheral | TBD |
| Pins | TBD |
| Supply voltage | TBD |
| Maximum current | TBD |
| Connector | TBD |
| Protocol | TBD |
| Authentication | Future requirement |
| Encryption | Future requirement |

No operational radio shall be treated as integrated until these fields and the applicable verification procedures are completed.

---

# 14. Software Interfaces

## 14.1 Software Layer Boundaries

```text
Application
    │
    ▼
Services and Domain Interfaces
    │
    ▼
Device Drivers
    │
    ▼
Platform Abstraction
    │
    ▼
STM32 Hardware
```

Application software shall not directly access STM32 peripheral registers.

---

## 14.2 Primary Software Data Interfaces

| Interface | Producer | Consumer | Primary Data |
| --- | --- | --- | --- |
| IMU sample | IMU driver or acquisition service | State Estimation | Angular rate, acceleration, timestamp, validity |
| State estimate | State Estimation | Flight Control and telemetry | Orientation, timestamp, validity |
| Flight setpoint | Command or test source | Flight Control | Desired rates or attitude and throttle |
| Control output | Flight Control | Motor Output | Roll, pitch, yaw, and collective command |
| Motor commands | Motor Output | ESC driver | Four bounded commands |
| System health | Subsystem health producers | System Supervision | Validity, faults, timing |
| Telemetry data | Application subsystems | Communications | Selected system data |
| Received command | Communications | Command handler | Validated command and metadata |

---

## 14.3 Interface Ownership Table

| Interface | Initialization Owner | Runtime Producer | Validation Owner | Fault Consumer |
| --- | --- | --- | --- | --- |
| IMU SPI | IMU driver | IMU driver | IMU driver | System Supervision |
| State estimate | State Estimation | State Estimation | State Estimation | Flight Control and System Supervision |
| Control output | Flight Control | Flight Control | Flight Control | Motor Output and System Supervision |
| Motor commands | Motor Output | Motor Output | Motor Output | ESC driver and System Supervision |
| UART transport | Communications driver | Communications subsystem | Parser and transport | System Supervision |
| SWD | Development tooling | External debugger | Development process | Development process |

---

## 14.4 Data Validity

Time-sensitive software interfaces shall identify data validity using one or more of:

- Timestamp
- Sequence number
- Valid flag
- Health status
- Age limit
- Initialization state

Consumers shall not silently treat invalid or stale data as current valid data.

---

## 14.5 Unit Conventions

Unless explicitly documented otherwise, software interfaces should use SI units.

| Quantity | Preferred Unit |
| --- | --- |
| Angular rate | radians per second |
| Angle | radians |
| Acceleration | meters per second squared |
| Time | seconds or integer microseconds |
| Voltage | volts |
| Current | amperes |
| Distance | meters |
| Temperature | degrees Celsius |
| Motor command | Documented normalized or protocol-specific unit |

---

# 15. Mechanical Interfaces

## 15.1 Flight Controller Mounting Interface

| Item | Value |
| --- | --- |
| Board envelope | TBC |
| Mounting-hole pattern | TBC |
| Fastener size | TBC |
| Standoff height | TBC |
| Connector-clearance envelope | TBC |
| Required access | USB, SWD, power, signal connectors |
| Orientation | TBC |

---

## 15.2 IMU Mounting Interface

| Item | Value |
| --- | --- |
| Module envelope | TBC |
| Mounting method | TBC |
| Fastener or adhesive method | TBC |
| Aircraft-frame orientation | TBC |
| Position relative to center | Near aircraft center where practical |
| Vibration-isolation method | TBC |
| Removal method | Serviceable |

---

## 15.3 ESC Mounting Interface

| Item | Value |
| --- | --- |
| ESC envelope | TBC |
| Mounting-hole pattern | TBC |
| Fastener size | TBC |
| Cooling clearance | TBC |
| Battery-wire exit direction | TBC |
| Motor-wire exit directions | TBC |
| Signal-connector access | Required |

---

## 15.4 Battery Interface

| Item | Value |
| --- | --- |
| Baseline battery | 4S, approximately 850 mAh |
| Battery envelope | TBC |
| Mounting location | TBC |
| Strap width | TBC |
| Adjustment range | TBC |
| Connector access | Required |
| Propeller clearance | Required |

---

# 16. Harness and Connector Identification

## 16.1 Harness Naming Convention

Harnesses should use identifiers in the following form:

```text
HAR-<NUMBER>
```

Examples:

```text
HAR-001 — Battery-to-ESC harness
HAR-002 — Regulated-power harness
HAR-003 — IMU SPI harness
HAR-004 — ESC control-signal harness
HAR-005 — SWD debug harness
HAR-006 — Development UART harness
```

---

## 16.2 Connector Naming Convention

Connectors should use identifiers in the following form:

```text
J<NUMBER>
```

Example:

```text
J1 — Battery input
J2 — Flight Controller power
J3 — IMU interface
J4 — ESC control interface
J5 — SWD
J6 — Development UART
```

Final numbering shall be assigned in the wiring diagram.

---

## 16.3 Harness Definition Table

| Harness | Source | Destination | Signals | Wire Gauge | Connector | Status |
| --- | --- | --- | --- | --- | --- | --- |
| HAR-001 | 4S battery | Four-in-one ESC | VBAT and GND | TBC | XT30 and ESC termination | Open |
| HAR-002 | Regulated supply | Flight Controller | Power and ground | TBC | TBC | Open |
| HAR-003 | Flight Controller | IMU | SPI, interrupt, power, ground | TBC | TBC | Open |
| HAR-004 | Flight Controller | ESC | Four commands and ground | TBC | TBC | Open |
| HAR-005 | ST-Link | Flight Controller | SWDIO, SWCLK, GND, VTREF, NRST | TBC | TBC | Open |
| HAR-006 | USB-UART adapter | Flight Controller | TX, RX, GND | TBC | TBC | Open |

---

## 16.4 Connector Orientation

Every connector pinout shall include:

- Connector identifier
- Connector family
- Mating-part identifier
- Pin numbering
- Viewing direction
- Key or latch orientation
- Signal name
- Wire color
- Voltage
- Source and destination

A pinout without a defined viewing direction shall not be considered complete.

---

# 17. Startup and Safe-State Requirements

## 17.1 Safe Interface State

Before application initialization is complete:

- Motor-command signals shall be non-commanding.
- IMU chip select shall be inactive.
- Unused outputs shall use defined states.
- Communications shall not arm the aircraft.
- Invalid sensor data shall not be accepted as valid.
- Fault status shall default conservatively.

---

## 17.2 Initialization Order

The intended interface initialization sequence is:

1. Processor and runtime initialization
2. Safe GPIO configuration
3. Clock and timebase initialization
4. Debug and diagnostic initialization
5. Power and reset-cause checks
6. Communication-peripheral initialization
7. IMU SPI initialization
8. IMU identity and configuration verification
9. State Estimation initialization
10. Flight Control initialization
11. Motor Output initialization in non-commanding state
12. System Supervision health evaluation
13. Entry into disarmed operational state

---

## 17.3 Interface Failure Response

| Interface Failure | Required Response |
| --- | --- |
| SWD unavailable | Normal standalone firmware operation may continue |
| USB unavailable | Report when possible; retain alternate programming path |
| UART unavailable | Continue flight-critical scheduling |
| IMU unavailable | Reject arming and report critical sensor fault |
| IMU data stale | Invalidate state estimate and enter defined fault response |
| ESC driver unavailable | Prevent arming and maintain non-commanding outputs |
| Command link lost | Execute defined command-link-loss behavior |
| Telemetry link lost | Continue flight-critical behavior when telemetry is noncritical |
| Power rail invalid | Prevent arming or enter safe state |
| Invalid pin configuration | Prevent affected subsystem activation |

---

# 18. Interface Verification

## 18.1 Verification Methods

Interfaces shall be verified using one or more of:

- Inspection
- Analysis
- Demonstration
- Test

---

## 18.2 Required Interface Tests

| Test ID | Test | Interfaces Covered | Status |
| --- | --- | --- | --- |
| VER-ICD-001 | SWD programming and debugging | Flight Controller and debugger | Planned |
| VER-ICD-002 | USB DFU or recovery test | Flight Controller and host computer | Planned |
| VER-ICD-003 | Development UART test | Flight Controller and UART adapter | Planned |
| VER-ICD-004 | IMU SPI identity test | Flight Controller and ICM-20602 | Planned |
| VER-ICD-005 | IMU axis-orientation test | IMU and aircraft coordinates | Planned |
| VER-ICD-006 | Motor-output signal test | Flight Controller and ESC | Planned |
| VER-ICD-007 | Motor mapping and direction test | ESC and motors | Planned |
| VER-ICD-008 | Power-rail validation | Battery, regulator, FC, and IMU | Planned |
| VER-ICD-009 | Ground-continuity test | All non-isolated interfaces | Planned |
| VER-ICD-010 | Connector and harness inspection | Electrical and mechanical interfaces | Planned |
| VER-ICD-011 | Safe startup and reset test | Motor outputs and system supervision | Planned |
| VER-ICD-012 | Communication congestion test | UART and flight-critical scheduling | Planned |

---

## 18.3 Pin-Assignment Verification

Before a pin assignment is approved, verify:

- Exact MCU part and package
- Exact board schematic
- Board-header exposure
- Alternate-function availability
- Timer channel availability
- DMA compatibility where required
- Voltage compatibility
- Reset-state behavior
- Conflicts with onboard peripherals
- Debug-pin conflicts
- Bootloader requirements
- Physical connector access

---

# 19. Interface Allocation Tables

## 19.1 Electrical Interface Summary

| Interface | Source | Destination | Type | Status |
| --- | --- | --- | --- | --- |
| Battery power | 4S LiPo | ESC | High-current DC | Defined |
| Electronics power | Regulator | Flight Controller | Regulated DC | Open |
| IMU power | Regulator or Flight Controller | ICM-20602 | Regulated DC | Open |
| IMU data | Flight Controller | ICM-20602 | SPI | Open |
| IMU interrupt | ICM-20602 | Flight Controller | Digital input | Open |
| Motor commands | Flight Controller | ESC | Digital timing protocol | Open |
| SWD | ST-Link | Flight Controller | Debug | Open |
| USB | Host computer | Flight Controller | USB | Open |
| Development UART | Flight Controller and adapter | Bidirectional | UART | Open |
| Future radio | Flight Controller | Radio | TBD | Reserved |

---

## 19.2 Software Interface Summary

| Interface | Producer | Consumer | Status |
| --- | --- | --- | --- |
| ImuSample | IMU driver | State Estimation | Defined conceptually |
| AttitudeEstimate | State Estimation | Flight Control | Defined conceptually |
| FlightSetpoint | Command handler or test source | Flight Control | Defined conceptually |
| ControlOutput | Flight Control | Motor Output | Defined conceptually |
| MotorCommands | Motor Output | ESC driver | Defined conceptually |
| SystemHealth | Major subsystems | System Supervision | Defined conceptually |
| Telemetry messages | Communications encoder | External receiver | Protocol TBD |
| Received commands | Communications parser | Command handler | Protocol TBD |

---

## 19.3 Mechanical Interface Summary

| Interface | Connected Items | Status |
| --- | --- | --- |
| Flight Controller mount | Airframe and Flight Controller | Open |
| IMU mount | Airframe and IMU module | Open |
| ESC mount | Airframe and four-in-one ESC | Open |
| Motor mounts | Arms and four motors | Defined conceptually |
| Battery mount | Airframe and 4S battery | Open |
| Harness retention | Airframe and wiring | Open |
| Future payload mount | Airframe and payload | Reserved |

---

# 20. Open Interface Decisions

| Action ID | Decision or Missing Data | Priority | Status |
| --- | --- | --- | --- |
| ICD-ACT-001 | Confirm exact STM32H743 Flight Controller board and processor package | Critical | Open |
| ICD-ACT-002 | Obtain and archive the exact Flight Controller schematic | Critical | Open |
| ICD-ACT-003 | Assign and verify the IMU SPI peripheral and pins | Critical | Open |
| ICD-ACT-004 | Confirm ICM-20602 breakout-board voltage requirements | Critical | Open |
| ICD-ACT-005 | Confirm ICM-20602 SPI mode and maximum clock | High | Open |
| ICD-ACT-006 | Assign the IMU interrupt pin | High | Open |
| ICD-ACT-007 | Select and document the ESC command protocol | Critical | Open |
| ICD-ACT-008 | Assign four compatible timer outputs | Critical | Open |
| ICD-ACT-009 | Define motor numbering and rotation directions | Critical | Open |
| ICD-ACT-010 | Confirm ESC signal-level compatibility | Critical | Open |
| ICD-ACT-011 | Define the regulated electronics power source | Critical | Open |
| ICD-ACT-012 | Verify all permitted USB, debugger, and external-power combinations | High | Open |
| ICD-ACT-013 | Assign the development UART peripheral and pins | High | Open |
| ICD-ACT-014 | Define connector families and pin numbering | High | Open |
| ICD-ACT-015 | Create the complete aircraft wiring diagram | High | Open |
| ICD-ACT-016 | Record mechanical mounting patterns and envelopes | Medium | Open |
| ICD-ACT-017 | Define communication protocol fields and message identifiers | Medium | Open |
| ICD-ACT-018 | Update RTM-001 with ICD-001 allocations | Medium | Open |

---

# 21. Change Control

Changes to controlled interfaces shall be recorded in this document.

An interface change should include:

1. Updated interface definition
2. Updated revision number
3. Updated revision history
4. Review of connected hardware
5. Review of firmware pin and peripheral configuration
6. Review of software data types
7. Review of mechanical routing or mounting
8. Review of wiring documentation
9. Review of verification procedures
10. Updated requirements traceability

Pin assignments shall not be changed silently after harness fabrication or firmware integration.

---

# 22. References

- **SPEC-001** — Stratus Rev A System Specification
- **REQ-001** — Stratus Rev A Requirements Specification
- **ARC-001** — Stratus System Architecture
- **RTM-001** — Requirements Traceability Matrix
- **REQ-FR-001** — Flight Control Functional Requirements
- **REQ-FR-002** — State Estimation Functional Requirements
- **REQ-FR-003** — Motor Output Functional Requirements
- **REQ-FR-004** — Communications Functional Requirements
- **REQ-HW-001** — Hardware Requirements
- **REQ-SW-001** — Software Requirements
- **REQ-ME-001** — Mechanical Requirements
- **REQ-EL-001** — Electrical Requirements
- **SES-001** — Mechanical Engineering Standard
- **SES-002** — Electrical Engineering Standard
- **HDR-001** — ICM-20602 IMU
- **HDR-003** — Aero Selfie 45A ESC
- **HDR-005** — 4S Power System
- **HDR-007** — Wiring Materials

---

# 23. Related Documents

## Upstream

- SPEC-001 — Stratus Rev A System Specification
- REQ-001 — Stratus Rev A Requirements Specification
- ARC-001 — Stratus System Architecture

## Peer

- RTM-001 — Requirements Traceability Matrix
- BOM-001 — Bill of Materials
- SES-001 — Mechanical Engineering Standard
- SES-002 — Electrical Engineering Standard
- ADR Series
- HDR Series

## Supporting Requirements

- REQ-FR-001 — Flight Control
- REQ-FR-002 — State Estimation
- REQ-FR-003 — Motor Output
- REQ-FR-004 — Communications
- REQ-HW-001 — Hardware
- REQ-SW-001 — Software
- REQ-ME-001 — Mechanical
- REQ-EL-001 — Electrical

## Downstream

- Flight Controller pin-allocation file
- Board configuration source
- Wiring diagram
- Harness definitions
- Connector pinouts
- Communication protocol specification
- CAD interface drawings
- Interface verification procedures
- Interface verification records