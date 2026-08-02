# Stratus Mechanical Engineering Standard

Document ID: SES-001

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
4. Units and Coordinate Conventions
5. Standard Fasteners
6. Threaded Inserts
7. Standoffs and Spacers
8. Module Mounting Standards
9. Airframe Architecture
10. Additive Manufacturing Standards
11. Material Selection
12. Vibration and Sensor Mounting
13. Cable and Connector Accommodation
14. Serviceability and Repair
15. CAD Standards
16. Drawing and Dimensioning Standards
17. Mechanical Inspection
18. Deviations and Exceptions
19. References
20. Related Documents

---

# 1. Purpose

This document establishes the mechanical engineering standards governing the design, fabrication, assembly, inspection, and maintenance of the Stratus platform.

The purpose of this standard is to ensure that mechanical components remain modular, compatible, serviceable, and repeatable across Stratus revisions.

This document defines standard practices rather than component-selection rationale. Specific hardware selections and architectural decisions are documented in the applicable Hardware Decision Records and Architecture Decision Records.

---

# 2. Scope

This standard applies to mechanical components and assemblies developed for Stratus Rev A, including:

- Airframe components
- Electronics mounting structures
- Battery mounting features
- Motor mounting features
- Fasteners
- Threaded inserts
- Standoffs and spacers
- Protective structures
- Additive-manufactured parts
- Module interfaces
- Cable-routing features
- Mechanical CAD models and drawings

Commercial off-the-shelf components are not required to conform internally to this standard; however, their integration into Stratus shall conform to the applicable mounting, clearance, fastening, and serviceability requirements defined here.

---

# 3. Governing Principles

Mechanical development for Stratus shall follow these principles:

### Modularity

Subsystems shall be removable and replaceable without requiring destructive disassembly of unrelated subsystems.

### Standardization

Common fasteners, mounting patterns, insert sizes, and interface conventions shall be reused wherever practical.

### Serviceability

Frequently accessed components shall remain accessible using common hand tools.

### Repairability

Damage to one structural module should not require replacement of the complete airframe.

### Repeatability

Parts shall be designed so that multiple instances can be fabricated and assembled with consistent results.

### Progressive Refinement

Rev A designs shall prioritize architecture validation, manufacturability, and iteration speed over minimum weight or maximum structural optimization.

### Compatibility

Mechanical interfaces shall support future subsystem upgrades without unnecessary redesign of validated neighboring components.

---

# 4. Units and Coordinate Conventions

## 4.1 Units

All mechanical dimensions shall use SI units.

- Linear dimensions: millimeters
- Angular dimensions: degrees
- Mass: grams or kilograms
- Force: newtons
- Torque: newton-millimeters or newton-meters

Decimal values shall use a period as the decimal separator.

## 4.2 Aircraft Coordinate System

Unless otherwise specified, the aircraft coordinate system shall be defined as:

- Positive X: forward
- Positive Y: right
- Positive Z: downward

This convention shall be used consistently in mechanical, electrical, software, and sensor-orientation documentation.

## 4.3 Origin

The preferred aircraft reference origin shall be located at the geometric center of the motor layout or another explicitly documented central datum.

Subsystem-specific coordinate systems shall document their relationship to the aircraft coordinate system.

---

# 5. Standard Fasteners

## 5.1 Preferred Thread Series

Metric fasteners shall be used throughout Stratus.

Preferred sizes are:

| Size | Preferred Use |
| --- | --- |
| M2 | Electronics, lightweight modules, sensor mounts, and small printed components |
| M2.5 | Intermediate mounting where component interfaces require it |
| M3 | Structural joints, motor mounts, major frame members, and higher-load connections |

Imperial fasteners shall not be introduced unless required by a commercial component for which no practical metric alternative exists.

## 5.2 Preferred Head Style

Socket-head cap screws shall be the default fastener type.

Button-head screws may be used where reduced profile is required and the lower tool engagement is acceptable.

Countersunk screws shall only be used when:

- A flush surface is required.
- The receiving part is designed with the correct countersink geometry.
- The reduced material thickness does not compromise the joint.

Phillips-head and slotted fasteners should be avoided.

## 5.3 Fastener Material

Stainless steel fasteners shall be the default for general structural and electronics assembly.

Nylon fasteners may be used for:

- Electrically sensitive mounting
- Low-load electronics retention
- Intentional mechanical isolation
- Sacrificial or breakaway features
- Weight reduction where structural strength is not required

Nylon fasteners shall not be used for motor mounting or primary structural joints.

## 5.4 Engagement

Thread engagement shall be sufficient to prevent stripping or loosening under expected service loads.

As a general design objective:

- Metal-to-metal joints should provide at least one nominal fastener diameter of thread engagement.
- Polymer joints should use inserts or greater engagement where practical.
- Fasteners shall not bottom out before clamping the joint.

## 5.5 Fastener Retention

Thread-locking compound may be used on metal-to-metal joints subject to vibration.

Thread-locking compound shall not be applied to:

- Nylon fasteners
- Polymer threads
- Heat-set inserts where chemical compatibility is unknown
- Components requiring frequent adjustment unless explicitly justified

---

# 6. Threaded Inserts

## 6.1 Preferred Type

Brass heat-set threaded inserts shall be the preferred reusable thread interface in additive-manufactured structural components.

## 6.2 Preferred Sizes

M2 and M3 inserts shall be used as the primary insert sizes.

M2.5 inserts may be used when required by component interfaces.

## 6.3 Insert Geometry

Insert holes shall be designed according to the actual insert manufacturer’s recommended dimensions.

When manufacturer dimensions are unavailable, test coupons shall be printed before finalizing the production geometry.

## 6.4 Installation

Heat-set inserts shall be installed:

- Perpendicular to the mating surface
- At a controlled temperature
- Without excessive axial force
- Flush with or slightly below the designed reference surface
- Without visible cracking, distortion, or material displacement that interferes with assembly

## 6.5 Design Restrictions

Heat-set inserts shall not be placed:

- Too close to thin walls
- In unsupported cantilever features
- Where insertion heat may deform critical geometry
- Where insufficient surrounding material exists to transfer load

---

# 7. Standoffs and Spacers

## 7.1 Preferred Standoff Material

Nylon standoffs are acceptable and preferred for initial Rev A electronics mounting where:

- Loads are low.
- Electrical isolation is beneficial.
- Elevated temperatures are not expected.
- The standoff is not part of the primary load path.

Metal standoffs shall be used where greater stiffness, temperature resistance, or thread durability is required.

## 7.2 Preferred Size

M2 standoffs shall be the default for lightweight electronics modules unless the component uses another established mounting pattern.

## 7.3 Standoff Selection

Standoff length shall provide adequate clearance for:

- Solder joints
- Pin headers
- Wiring
- Connectors
- Component height
- Airflow
- Assembly tools

## 7.4 Stack Stability

Tall standoff stacks shall be evaluated for bending and vibration.

Multiple short adapters should not be stacked when a correctly sized single standoff is available.

---

# 8. Module Mounting Standards

## 8.1 Standard Mounting Patterns

Modules shall use recognized mounting patterns wherever practical.

Preferred patterns include:

- 20 × 20 millimeter electronics mounting
- 25.5 × 25.5 millimeter electronics mounting where required
- 30.5 × 30.5 millimeter electronics mounting for larger modules
- Component-specific motor mounting patterns
- Explicitly documented Stratus module patterns for custom assemblies

Hole-to-hole dimensions shall describe hole-center spacing.

## 8.2 Standard Interface Definition

Each module interface shall define:

- Mounting-hole pattern
- Fastener size
- Maximum component envelope
- Connector-access requirements
- Cable-exit direction
- Required clearances
- Orientation
- Datum or alignment features
- Expected mass where relevant

## 8.3 Slotted Features

Slots may be used during prototyping to accommodate uncertain or variable dimensions.

Production-intent revisions should replace unnecessary slots with fixed holes once interfaces have been validated.

## 8.4 Direct Polymer Threads

Repeatedly serviced components shall not rely on self-tapped threads directly in printed polymer unless the connection is explicitly considered temporary or sacrificial.

---

# 9. Airframe Architecture

## 9.1 Modular Construction

The Rev A airframe shall be divided into replaceable mechanical modules wherever practical.

Potential modules include:

- Central electronics structure
- Individual arms
- Motor mounts
- Battery mount
- Protective covers
- Sensor mounts
- Landing features
- Payload interfaces

## 9.2 Structural Load Paths

Primary thrust and landing loads shall be transferred through intentional structural paths.

Electronics enclosures, cosmetic covers, and cable-routing features shall not unintentionally serve as primary structural members.

## 9.3 Arm Replacement

Where practical, individual arms shall be replaceable without removing the complete electronics stack.

## 9.4 Propeller Clearance

The design shall provide adequate clearance among:

- Propellers
- Frame components
- Wiring
- Battery
- Payloads
- Landing structures
- Adjacent propeller disks

Propeller clearance shall account for manufacturing tolerances, structural deflection, and minor crash deformation.

## 9.5 Center of Mass

Heavy components should be positioned near the aircraft center where practical.

Battery mounting shall permit reasonable adjustment of longitudinal and lateral center of mass.

## 9.6 Expansion

The mechanical architecture shall reserve practical routes or mounting provisions for future:

- Navigation sensors
- Radio modules
- Telemetry
- Cameras
- Companion computing
- Payloads
- Custom electronics

---

# 10. Additive Manufacturing Standards

## 10.1 Preferred Manufacturing Method

Stratus Rev A structural and integration components shall be designed primarily for fused-filament fabrication unless another process is explicitly required.

## 10.2 Design for Printing

Parts should be designed to:

- Minimize unsupported overhangs
- Reduce unnecessary support material
- Avoid trapped support structures
- Maintain consistent wall thickness
- Provide appropriate fillets at stress concentrations
- Orient layer lines with expected loads in mind
- Allow dimensional adjustment through parameters

## 10.3 Minimum Features

Minimum wall thickness, hole diameter, clearance, and feature size shall be validated against the selected printer, material, nozzle, and process settings.

Critical interfaces shall be validated using test coupons where uncertainty exists.

## 10.4 Hole Compensation

Printed holes may require dimensional compensation.

Nominal CAD diameter shall not be assumed to produce an equal finished diameter.

Final dimensions shall be established through calibration and documented where the interface is critical.

## 10.5 Layer Orientation

Parts shall be oriented so that primary service loads do not unnecessarily separate layer bonds.

Motor mounts, arms, and fastener interfaces shall receive explicit layer-orientation review.

## 10.6 Supports

Support-generated surfaces shall not be used as precision mating surfaces unless post-processing is planned.

## 10.7 Print Records

For flight-intent structural parts, the following should be recorded:

- Material
- Manufacturer
- Printer
- Nozzle diameter
- Layer height
- Wall count
- Top and bottom layers
- Infill type and percentage
- Print orientation
- Supports
- Part revision
- Date printed

---

# 11. Material Selection

## 11.1 Prototype Materials

PLA may be used for:

- Dimensional prototypes
- Fit checks
- Bench fixtures
- Low-temperature non-flight testing

PLA should not be assumed suitable for final flight hardware exposed to heat, sunlight, sustained stress, or impact.

## 11.2 Flight-Intent Materials

PETG, ASA, nylon, fiber-reinforced polymers, or other engineering materials may be selected based on:

- Strength
- Toughness
- Temperature resistance
- Creep resistance
- Printability
- Environmental resistance
- Required stiffness
- Expected impact behavior

## 11.3 Material Qualification

A material shall not be considered flight-qualified solely because it printed successfully.

Critical parts shall be evaluated for:

- Layer adhesion
- Fastener retention
- Insert retention
- Impact resistance
- Heat resistance
- Creep
- Dimensional stability

## 11.4 Material Traceability

Material type and significant print settings shall be associated with the part revision for flight-intent components.

---

# 12. Vibration and Sensor Mounting

## 12.1 Inertial Sensor Mounting

The IMU shall be mounted:

- Rigidly enough to preserve the intended sensor orientation
- Away from direct mechanical interference
- With a documented axis relationship to the airframe
- In a location that minimizes unnecessary vibration and flexure
- As close to the aircraft center of rotation as practical

## 12.2 Isolation

Vibration-isolation materials may be introduced when testing demonstrates a need.

Isolation shall not permit excessive sensor movement or introduce poorly controlled resonant behavior.

## 12.3 Orientation

Sensor orientation shall be mechanically keyed, marked, or otherwise documented to prevent ambiguous installation.

## 12.4 Propulsion Vibration

Motor, propeller, and arm interfaces shall be inspected for looseness, imbalance, and resonance before attributing vibration solely to the sensor mount.

---

# 13. Cable and Connector Accommodation

Mechanical designs shall provide adequate accommodation for wiring and connectors.

The design shall:

- Avoid sharp edges contacting insulation
- Prevent wire interference with propellers
- Avoid excessive bend radius
- Provide strain relief where required
- Preserve connector access
- Avoid crushing wires between structural parts
- Separate high-current wiring from sensitive sensor wiring where practical
- Allow disassembly without cutting permanent wiring wherever practical

Cable-routing features shall comply with SES-002.

---

# 14. Serviceability and Repair

## 14.1 Tool Access

Fasteners intended for routine access shall be reachable using common tools without dismantling unrelated modules.

## 14.2 Replaceable Components

Motors, arms, electronics modules, battery straps, and protective components should be replaceable independently where practical.

## 14.3 Captive Hardware

Captive nuts or inserts may be used to simplify field maintenance, provided they remain inspectable and replaceable.

## 14.4 Assembly Order

Assemblies shall have a defined installation and removal sequence where order affects serviceability or wire access.

## 14.5 Wear Items

Parts expected to wear, deform, or absorb crash energy should be:

- Inexpensive
- Easy to manufacture
- Easy to replace
- Separable from costly electronics

---

# 15. CAD Standards

## 15.1 Parametric Design

Mechanical parts shall use parametric dimensions where practical.

Critical interface values should be driven by named parameters rather than repeated manual dimensions.

## 15.2 Component Separation

Distinct physical components shall be represented as separate CAD components or bodies according to the capabilities of the CAD system.

## 15.3 Naming

CAD objects shall use descriptive names.

Avoid default names such as:

- Body1
- Sketch7
- Component12
- Copy of Part

Preferred names include:

- CenterPlate
- FrontLeftArm
- ImuMount
- BatteryTray
- MotorMount
- ElectronicsCover

## 15.4 Revision Identification

Exported mechanical files shall include sufficient naming information to identify:

- Project
- Part
- Revision
- Manufacturing representation where relevant

Example:

text STRATUS-REV-A-IMU-MOUNT-R01.stl 

## 15.5 Source and Export Files

Editable source models shall be retained.

Manufacturing exports such as STL, STEP, or 3MF files shall not replace the authoritative parametric source model.

## 15.6 Reference Models

Commercial component models shall be marked as reference geometry unless they are internally verified.

Unverified downloaded CAD shall not be treated as dimensionally authoritative.

---

# 16. Drawing and Dimensioning Standards

Critical components and interfaces should include sufficient drawings or documented dimensions to support independent reproduction.

Dimensions shall be taken from defined datums.

Critical dimensions may include:

- Mounting-hole spacing
- Hole diameter
- Insert bore diameter
- Plate thickness
- Motor-axis location
- Propeller clearance
- Connector envelope
- Standoff height
- Sensor orientation
- Battery envelope

Redundant or conflicting dimensions shall be avoided.

---

# 17. Mechanical Inspection

Mechanical assemblies shall be inspected before powered testing and flight.

Inspection should include:

- Correct fastener installation
- Insert seating
- Cracks or layer separation
- Warped parts
- Motor security
- Propeller clearance
- Wiring clearance
- Battery retention
- Sensor orientation
- Connector accessibility
- Loose components
- Center-of-mass concerns
- Evidence of heat or material deformation

Flight-intent assemblies shall not proceed to powered propulsion testing with known structural damage or unsecured components.

---

# 18. Deviations and Exceptions

A deviation from this standard is permitted when:

- A commercial component requires another interface.
- Testing identifies a better technical solution.
- A documented constraint makes compliance impractical.
- The deviation improves safety, reliability, or maintainability.

Significant deviations shall be documented in the applicable:

- Architecture Decision Record
- Hardware Decision Record
- Design note
- Part documentation
- Revision history

A deviation shall not silently redefine the project standard.

---

# 19. References

- SPEC-001 — Stratus Rev A System Specification
- REQ-001 — Stratus Rev A Requirements Specification
- ARC-001 — Stratus System Architecture
- BOM-001 — Bill of Materials
- SES-002 — Stratus Electrical Engineering Standard
- ADR-002 — Rev A Platform Size
- ADR-003 — Modular Airframe Architecture
- HDR-002 — HappyModel EX1404 Motors
- HDR-004 — Gemfan Hurricane 3520 Propellers
- HDR-006 — Mechanical Hardware Standard

---

# 20. Related Documents

## Upstream

- SPEC-001
- REQ-001
- ARC-001

## Peer

- SES-002 — Electrical Engineering Standard
- BOM-001 — Bill of Materials

## Supporting

- ADR-002 — Rev A Platform Size
- ADR-003 — Modular Airframe Architecture
- HDR-002 — Motor Selection
- HDR-004 — Propeller Selection
- HDR-006 — Mechanical Hardware Selection