# Stratus Electrical Engineering Standard

Document ID: SES-002

Revision: 1.0

Status: Draft

Classification: Public

Project: Stratus

Author: Austin Fellows

Created: 2026-08-02

Last Updated: 2026-08-02

---

# Revision History

| Version | Date | Description | Author |
| --- | --- | --- | --- |
| 1.0 | 2026-08-02 | Initial revision | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Draft |

---

# Table of Contents

1. Purpose
2. Scope
3. Governing Principles
4. Electrical System Classification
5. Voltage and Power Conventions
6. Grounding
7. Wire and Conductor Standards
8. Wire Color Conventions
9. Connectors
10. Power Distribution
11. Signal Interfaces
12. Inertial Sensor Interface
13. ESC and Motor-Control Interfaces
14. Development and Debug Interfaces
15. Soldering and Termination
16. Harness Construction
17. Routing and Mechanical Protection
18. Electrical Protection
19. Electrical Inspection and Test
20. Documentation and Identification
21. Deviations and Exceptions
22. References
23. Related Documents

---

# 1. Purpose

This document establishes the electrical engineering standards governing the design, assembly, integration, inspection, and maintenance of the Stratus platform.

The purpose of this standard is to ensure that Stratus electrical systems remain safe, reliable, maintainable, understandable, and reusable across future revisions.

This document defines electrical implementation practices rather than component-selection rationale. Specific hardware selections and architectural decisions are documented in the applicable Hardware Decision Records and Architecture Decision Records.

---

# 2. Scope

This standard applies to Stratus Rev A electrical systems, including:

- Battery connections
- Power distribution
- Flight Controller power
- ESC power and control
- Motor wiring
- Sensor wiring
- Communication interfaces
- Programming and debugging interfaces
- Connectors
- Wire harnesses
- Soldered joints
- Strain relief
- Grounding
- Electrical inspection
- Bench-test practices

Commercial off-the-shelf components are not required to comply internally with this standard. Their integration into Stratus shall comply with the applicable voltage, grounding, wiring, connector, routing, and inspection requirements defined here.

---

# 3. Governing Principles

Electrical development for Stratus shall follow these principles:

### Safety

Electrical assemblies shall minimize the risk of short circuits, reverse polarity, overheating, unintended motor operation, and battery damage.

### Reliability

Connections shall remain mechanically and electrically secure under expected vibration, movement, and handling.

### Maintainability

Wiring shall be organized, identifiable, inspectable, and replaceable without unnecessary disassembly.

### Standardization

Common wire gauges, colors, connector types, signal names, and routing practices shall be reused wherever practical.

### Separation of Concerns

High-current power wiring and sensitive signal wiring shall be treated as distinct electrical classes.

### Traceability

Electrical interfaces shall be documented sufficiently to support troubleshooting, reproduction, and future redesign.

### Progressive Refinement

Rev A shall prioritize safe and understandable electrical integration over minimum harness mass or maximum packaging density.

---

# 4. Electrical System Classification

Stratus electrical connections shall be classified into the following categories:

| Class | Description | Examples |
| --- | --- | --- |
| Primary Power | Unregulated battery-level power | Battery to ESC, battery input |
| Regulated Power | Power supplied at a controlled voltage | 5 V and 3.3 V rails |
| High-Current Output | Conductors carrying propulsion current | ESC-to-motor wiring |
| Digital Signal | Logic-level control or communication | SPI, UART, SWD, motor commands |
| Analog Signal | Voltage representing a measured quantity | Battery-voltage sensing |
| Ground | Shared electrical reference and return path | Power ground, signal ground |
| Development Interface | Temporary or permanent programming/debug access | SWD, USB, UART |

The classification of each interface shall be considered when selecting wire gauge, routing, connector type, and protection.

---

# 5. Voltage and Power Conventions

## 5.1 Battery Platform

Stratus Rev A shall use a nominal 4S lithium-polymer battery platform unless superseded by an approved decision record.

A 4S LiPo battery has:

- Nominal voltage: approximately 14.8 V
- Maximum fully charged voltage: 16.8 V
- Minimum safe voltage dependent on cell condition, load, and operating policy

All battery-connected equipment shall be rated for the maximum expected battery voltage, not only the nominal voltage.

## 5.2 Logic Voltage

The primary digital logic level shall be 3.3 V unless an interface explicitly requires another level.

Five-volt signals shall not be connected directly to non-five-volt-tolerant MCU or sensor pins.

## 5.3 Regulated Rails

Each regulated rail shall document:

- Nominal voltage
- Expected tolerance
- Maximum continuous current
- Source
- Loads
- Ground reference
- Protection
- Connector or test-point location

## 5.4 Power-Off Assumption

Electrical assembly, continuity testing, connector changes, and soldering shall be performed with the propulsion battery disconnected.

---

# 6. Grounding

## 6.1 Common Reference

All digital communication interfaces shall share a valid ground reference unless electrical isolation is explicitly designed into the interface.

## 6.2 Power and Signal Grounds

Power and signal grounds may share a common electrical reference, but routing shall minimize high-current motor and ESC return currents through sensitive sensor-ground paths.

## 6.3 Ground Loops

Unnecessary parallel ground paths shall be avoided where they may create circulating currents, noise coupling, or ambiguous current return paths.

## 6.4 Sensor Grounding

The IMU and other sensitive sensors shall use a short, low-impedance ground connection referenced to the Flight Controller.

## 6.5 Debug Ground

SWD, UART, USB, logic-analyzer, and oscilloscope connections shall include a common ground unless the instrument or interface is specifically isolated.

## 6.6 Bench Equipment

Before attaching grounded bench equipment, the engineer shall understand whether the instrument ground is earth-referenced and whether the connection can create an unintended short.

---

# 7. Wire and Conductor Standards

## 7.1 Conductor Construction

Flexible aircraft wiring shall use stranded copper conductors.

Tinned stranded copper is preferred because it improves solderability and corrosion resistance.

Solid-core wire shall not be used for flight wiring subject to vibration or repeated flexing.

## 7.2 Insulation

Flexible silicone insulation is preferred for internal aircraft wiring because of its:

- Flexibility
- Heat resistance
- Soldering tolerance
- Resistance to cracking under repeated movement

Other insulation materials may be used when their temperature, flexibility, abrasion, and voltage ratings are appropriate.

## 7.3 Standard Gauges

The following gauges are preferred for Rev A:

| Gauge | Preferred Use |
| --- | --- |
| 18 AWG | Primary battery and higher-current power connections where appropriate |
| 22 AWG | Moderate-current regulated power and accessory power |
| 24 AWG | Low-current power, SPI, UART, control, and general signal wiring |

Actual conductor size shall be selected based on:

- Maximum current
- Wire length
- Voltage drop
- Temperature rise
- Flexibility
- Connector capacity
- Fault current
- Available space

## 7.4 Current Rating

Wire gauge shall not be selected solely from a generic ampacity table. The design shall also consider:

- Bundle heating
- Enclosure temperature
- Duty cycle
- Propulsion current transients
- Connector limits
- Solder-joint capacity
- Voltage-drop tolerance

## 7.5 Wire Length

Wiring shall be no longer than reasonably required for assembly, serviceability, and strain relief.

Excessive service loops shall be avoided where they add mass, obstruct airflow, or increase electromagnetic coupling.

---

# 8. Wire Color Conventions

The following color convention shall be used wherever practical:

| Color | Function |
| --- | --- |
| Black | Ground or negative return |
| Red | Positive power |
| Orange | Battery-level positive power where distinction from regulated power is useful |
| Yellow | Clock or timing signal |
| Green | Data signal |
| Blue | Data signal or secondary communication line |
| White | Chip select, enable, interrupt, or miscellaneous control |
| Purple | Reserved auxiliary signal |
| Gray | Reserved or nonstandard signal requiring explicit labeling |

Color alone shall not be treated as sufficient identification for complex harnesses.

Where only one wire color is available, both ends shall be labeled or otherwise documented.

Black wire may be used exclusively for ground in mixed-color harnesses.

---

# 9. Connectors

## 9.1 General Requirements

Connectors shall be selected based on:

- Current rating
- Voltage rating
- Pin count
- Polarization
- Retention
- Vibration resistance
- Size
- Weight
- Availability
- Serviceability
- Mating-cycle requirements

## 9.2 Battery Connector

XT30 shall be the standard Rev A propulsion-battery connector unless superseded by an approved decision.

Battery connectors shall be polarized and installed so that exposed conductive surfaces do not present an avoidable short-circuit hazard.

## 9.3 Signal Connectors

Signal connectors shall be keyed or polarized where practical.

Unkeyed headers shall use clear pin-1 identification and documented orientation.

## 9.4 Connector Current

The current rating of a circuit shall not exceed the rating of its connector, terminals, PCB traces, or conductors.

The lowest-rated element determines the allowable circuit current.

## 9.5 Connector Retention

Connectors subject to vibration or movement shall have adequate friction retention, latch retention, strain relief, or secondary retention.

Permanent adhesive shall not be used as a substitute for an unsuitable connector.

## 9.6 Mating Compatibility

Physically compatible connectors carrying different voltages or functions shall be avoided where accidental interchange could cause damage.

---

# 10. Power Distribution

## 10.1 Primary Power Path

The primary propulsion power path shall be:

text Battery   ↓ XT30 connector   ↓ ESC / power-distribution input   ↓ Individual motor phases 

Accessory and Flight Controller power shall branch through an explicitly identified regulated source.

## 10.2 Current Paths

High-current paths shall be short and mechanically secure.

Primary power conductors shall not rely on breadboards, low-current jumper wires, or temporary test clips during powered propulsion operation.

## 10.3 Polarity

Positive and negative battery connections shall be verified before first power application and after any connector replacement.

## 10.4 Power Sequencing

Subsystems shall not depend on an undocumented power-up sequence.

Where sequencing is required, it shall be defined in ARC-001 or the applicable interface specification.

## 10.5 Regulator Capacity

Regulated power sources shall include adequate current margin for:

- Flight Controller
- IMU
- Communication modules
- Future peripherals
- Startup transients
- Expected expansion

## 10.6 Brownout Prevention

Power architecture shall minimize voltage droop capable of resetting the Flight Controller or corrupting sensor operation during propulsion transients.

## 10.7 Test Points

Critical rails should provide accessible test points for:

- Battery voltage
- Regulated voltage
- Ground
- Current measurement where practical

---

# 11. Signal Interfaces

## 11.1 Logic Compatibility

Both sides of a digital interface shall be electrically compatible in:

- Voltage level
- Input threshold
- Output drive
- Pull-up or pull-down requirements
- Maximum frequency
- Signal direction

## 11.2 Signal Naming

Signal names shall identify interface and function.

Examples:

text IMU_SPI_SCK IMU_SPI_MISO IMU_SPI_MOSI IMU_CS IMU_INT ESC_M1 ESC_M2 UART1_TX UART1_RX SWDIO SWCLK 

Generic names such as WIRE1, DATA, or PIN4 shall be avoided in authoritative documentation.

## 11.3 Unused Inputs

Unused digital inputs shall not be intentionally left floating when their state can affect system behavior.

They shall be configured with an appropriate pull-up, pull-down, or defined external bias where required.

## 11.4 Cable Length

High-speed digital wiring shall be kept short.

Longer interfaces shall be evaluated for signal integrity, noise susceptibility, and grounding.

## 11.5 Twisted Pairs

Twisted conductors may be used for:

- Power and ground
- Clock and ground
- Sensitive signal and ground
- Differential interfaces

Twisting shall not be used without considering connector layout and serviceability.

---

# 12. Inertial Sensor Interface

## 12.1 Preferred Interface

The primary IMU shall use SPI for normal flight operation unless superseded by an approved architecture decision.

## 12.2 Required Signals

The IMU interface shall include, as applicable:

- Regulated power
- Ground
- SPI clock
- Controller-to-sensor data
- Sensor-to-controller data
- Chip select
- Interrupt
- Optional auxiliary signals

## 12.3 Chip Select

The IMU chip-select signal shall have a defined inactive state during reset and initialization.

## 12.4 Routing

IMU signal wiring shall be:

- Short
- Separated from motor phase wires where practical
- Separated from primary battery wiring where practical
- Mechanically restrained
- Referenced to a reliable ground
- Routed to minimize loop area

## 12.5 Sensor Power

The IMU shall be powered only from a rail compatible with the breakout board and sensor.

Compatibility shall be verified from the actual module documentation rather than assumed from the sensor IC alone.

## 12.6 Orientation and Pinout

The electrical pinout and mechanical axis orientation shall both be documented.

---

# 13. ESC and Motor-Control Interfaces

## 13.1 ESC Power

The ESC battery input shall use conductors and connectors rated for expected current and voltage.

## 13.2 Motor Phases

The three phase conductors between each ESC channel and motor shall:

- Use equal or reasonably similar lengths where practical
- Be mechanically retained
- Avoid propeller interference
- Avoid sharp bends
- Be sized for expected motor current

## 13.3 Motor Direction

Motor direction may be reversed by changing control configuration or exchanging two motor phase conductors.

The final motor direction shall be documented and verified without installed propellers.

## 13.4 Control Signals

Each ESC channel shall receive a distinct motor-control signal referenced to system ground.

Motor-output signal naming shall correspond consistently to the physical motor-numbering convention.

## 13.5 Bench Testing

Motor and ESC tests shall initially be performed:

- Without propellers
- With the airframe restrained
- With a readily accessible battery disconnect
- At minimum practical command level
- After verifying motor mapping and direction

## 13.6 Safe State

Motor-control outputs shall default to a non-commanding state during reset, boot, fault, and programming operations.

---

# 14. Development and Debug Interfaces

## 14.1 SWD

The Flight Controller shall provide access to:

- SWDIO
- SWCLK
- Ground
- Target-voltage reference where required
- Reset where practical

## 14.2 Debug Power

The target shall not be unintentionally powered simultaneously from multiple sources unless the interfaces are explicitly designed to permit it.

Before connecting debugger power:

- Identify whether the debugger pin is power output or voltage reference.
- Identify whether the target is already powered.
- Verify common ground.
- Confirm acceptable voltage.

## 14.3 USB DFU

USB DFU may be used as a firmware recovery or programming path when supported by the MCU and board.

DFU does not replace the need for SWD debugging during software development.

## 14.4 UART

A development UART should be reserved for:

- Diagnostic output
- Bring-up
- Telemetry prototyping
- Fault reporting

Default development settings should be documented, including baud rate, parity, data bits, and stop bits.

## 14.5 Test Equipment

Logic analyzers and oscilloscopes shall be connected only after verifying:

- Voltage compatibility
- Common ground
- Probe-ground behavior
- Maximum input voltage
- Suitable sample rate or bandwidth

---

# 15. Soldering and Termination

## 15.1 Joint Quality

Solder joints shall be:

- Mechanically secure
- Electrically continuous
- Properly wetted
- Free from unintended bridges
- Free from loose strands
- Free from excessive exposed conductor

## 15.2 Preparation

Stranded conductors shall be stripped without cutting a significant number of strands.

Conductors and pads may be pre-tinned where appropriate.

## 15.3 Heat

Soldering temperature and dwell time shall be controlled to avoid:

- Melted insulation
- Lifted pads
- Damaged connectors
- Delaminated PCB material
- Heat-damaged components

## 15.4 Heat Shrink

Heat-shrink tubing shall be used where practical to:

- Insulate exposed joints
- Provide strain relief
- Identify conductors
- Protect splices

Heat shrink shall not hide an uninspected or mechanically weak joint.

## 15.5 Splices

Splices should be minimized.

Where unavoidable, splices shall be:

- Mechanically secure
- Properly soldered or crimped
- Insulated
- Strain-relieved
- Documented if located inside a permanent harness

## 15.6 Crimping

Crimp terminals shall use tooling appropriate for the terminal family.

Crimping with generic pliers shall not be considered an acceptable production-intent termination method.

---

# 16. Harness Construction

## 16.1 Harness Definition

A harness shall document:

- Source
- Destination
- Signal names
- Wire gauge
- Wire color
- Connector type
- Pin assignments
- Approximate length
- Branch points
- Shielding or twisting where applicable

## 16.2 Branching

Harness branches shall not place unsupported stress on solder joints or connector terminals.

## 16.3 Service Loops

A small service allowance may be included where needed for connector access and assembly.

Service loops shall not be large enough to interfere with propellers, airflow, sensors, or structural movement.

## 16.4 Bundling

Wire bundles may use:

- Braided sleeving
- Spiral wrap
- Heat-shrink sections
- Releasable cable ties
- Printed routing clips

Bundling methods shall not crush insulation or prevent required movement.

## 16.5 Harness Replacement

Frequently serviced harnesses should be replaceable independently from major structural components.

---

# 17. Routing and Mechanical Protection

Wiring shall be routed to avoid:

- Propeller disks
- Motor bells
- Sharp edges
- Pinch points
- Hot components
- Moving joints
- Excessive flexing
- Direct contact with abrasive printed surfaces
- High-current noise sources where sensitive signals are present

Wiring shall be supported near connectors so that vibration is not transferred directly to solder joints.

Pass-through holes shall use adequate edge radius, grommets, sleeving, or another protective method where abrasion is possible.

Routing shall comply with the mechanical-clearance requirements in SES-001.

---

# 18. Electrical Protection

## 18.1 Reverse Polarity

Polarized connectors shall be used where possible.

Battery polarity shall be verified before initial connection.

## 18.2 Short-Circuit Prevention

Exposed battery-level conductors shall be minimized and insulated.

Loose conductive tools and hardware shall be kept away from powered assemblies.

## 18.3 Overcurrent Protection

Bench power supplies should use a current limit during initial subsystem bring-up where practical.

Any fuse or protection device shall be rated for the expected normal and transient current.

## 18.4 Transient Protection

Sensitive electronics shall be protected from expected switching transients and supply noise through appropriate architecture, component selection, filtering, and layout.

## 18.5 Battery Safety

LiPo batteries shall be:

- Charged with a compatible balance charger
- Inspected before use
- Stored at an appropriate storage voltage
- Kept away from conductive debris
- Removed from service when swollen, punctured, overheated, or otherwise damaged
- Charged in a suitable fire-resistant location or enclosure
- Never left charging unattended

## 18.6 Propulsion Safety

Electrical tests capable of commanding motors shall be treated as powered propulsion tests, even when low command values are expected.

Propellers shall remain removed until motor mapping, direction, safe-state behavior, and command limits have been verified.

---

# 19. Electrical Inspection and Test

## 19.1 Pre-Power Inspection

Before first power application, inspect:

- Battery polarity
- Connector orientation
- Exposed conductors
- Solder bridges
- Loose wire strands
- Wire gauge
- Harness routing
- Ground continuity
- Power-to-ground resistance
- Regulator orientation
- Component voltage ratings
- Mechanical strain on terminals

## 19.2 Continuity Testing

Continuity testing shall verify:

- Intended point-to-point connections
- Ground continuity
- Absence of unintended shorts
- Correct connector pinout
- Correct motor-channel mapping where practical

## 19.3 Initial Power-Up

Initial power-up should use one or more of:

- Current-limited bench supply
- Smoke stopper
- Inline current monitor
- Low-risk subsystem power source

Full propulsion-battery connection shall not be the first diagnostic method for an unverified electrical assembly.

## 19.4 Rail Verification

Regulated voltages shall be measured before connecting sensitive loads where practical.

## 19.5 Functional Test

Electrical interfaces shall be verified incrementally:

1. Power rails
2. MCU programming and debugging
3. GPIO
4. UART
5. SPI
6. IMU identity
7. Sensor data
8. ESC control without propellers
9. Motor direction
10. Integrated system operation

## 19.6 Post-Test Inspection

Following abnormal behavior, high-current testing, or a hard landing, inspect for:

- Heat damage
- Discoloration
- Loose connectors
- Broken strands
- Damaged insulation
- Lifted pads
- Cracked solder joints
- Battery damage
- Unexpected odor

---

# 20. Documentation and Identification

Electrical documentation shall include, where applicable:

- System wiring diagram
- Harness drawings
- Connector pinouts
- Signal names
- Wire gauges
- Wire colors
- Power-rail definitions
- Grounding strategy
- Test points
- Revision identifier
- Interface ownership
- Expected voltage and current

Connector diagrams shall identify the viewing orientation.

Ambiguous pin numbering shall be avoided.

Changes to wiring or pin assignments shall be reflected in documentation before the affected configuration is considered released.

---

# 21. Deviations and Exceptions

A deviation from this standard is permitted when:

- A commercial component requires another interface.
- A validated electrical constraint requires an alternative.
- Testing identifies a safer or more reliable solution.
- A temporary bring-up configuration is clearly identified as non-flight hardware.
- The deviation is necessary to support future architecture.

Significant deviations shall be documented in the applicable:

- Architecture Decision Record
- Hardware Decision Record
- Interface-control documentation
- Wiring diagram
- Revision history
- Test record

Temporary wiring shall not silently become the released flight configuration.

---

# 22. References

- SPEC-001 — Stratus Rev A System Specification
- REQ-001 — Stratus Rev A Requirements Specification
- ARC-001 — Stratus System Architecture
- BOM-001 — Bill of Materials
- SES-001 — Stratus Mechanical Engineering Standard
- ADR-001 — STM32H743 Architecture
- ADR-004 — Custom Flight Software
- HDR-001 — ICM-20602 IMU
- HDR-003 — Aero Selfie 45A 4-in-1 ESC
- HDR-005 — 4S 850mAh Power System
- HDR-007 — Wiring Materials Standard

---

# 23. Related Documents

## Upstream

- SPEC-001
- REQ-001
- ARC-001

## Peer

- SES-001 — Mechanical Engineering Standard
- BOM-001 — Bill of Materials

## Supporting

- ADR-001 — Flight Controller Architecture
- ADR-004 — Custom Flight Software
- HDR-001 — IMU Selection
- HDR-003 — ESC Selection
- HDR-005 — Battery and Power-System Selection
- HDR-007 — Wiring-Material Selection