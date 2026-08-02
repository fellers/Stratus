# Stratus Rev A Bill of Materials

**Document ID:** BOM-001  
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
| 1.0 | 2026-06-26 | Initial Rev A bill of materials | Austin Fellows |
| 1.1 | 2026-08-02 | Corrected document references and added NUCLEO-F401RE development debugger | Austin Fellows |

---

# 1. Purpose

This document identifies the baseline components, development equipment, materials, and quantities selected for Stratus Rev A.

Component-selection rationale is maintained in the associated Architecture Decision Records and Hardware Decision Records.

Purchase links are provided for procurement reference only. The component manufacturer and part number remain authoritative if a retailer listing changes or becomes unavailable.

---

# 2. Rev A Bill of Materials

| Category | Component | Manufacturer or Model | Qty | Recorded Cost | Procurement Link | Decision Record |
| --- | --- | --- | ---: | ---: | --- | --- |
| Flight Controller | STM32H743 development platform | STM32H743XIH6-based board | 1 | $27 | [Amazon](https://www.amazon.com/dp/B0F28SFPB3) | [ADR-001](../decisions/adr/ADR-001-STM32H743-Architecture.md) |
| Development Debugger | STM32 Nucleo-64 development board | NUCLEO-F401RE | 1 | $25 | [Amazon](https://www.amazon.com/dp/B07JYBPWN4) | [ADR-006](../decisions/adr/ADR-006-NUCLEO-F401RE-Debugger.md) |
| IMU | Six-axis inertial measurement unit | ICM-20602 | 1 | $10 | [Amazon](https://www.amazon.com/dp/B0FXWL157Q) | [HDR-001](../decisions/hdr/HDR-001-ICM20602-IMU.md) |
| ESC | Four-in-one electronic speed controller | Aero Selfie 45A | 1 | $26 | [Amazon](https://www.amazon.com/dp/B0DQXPW3H4) | [HDR-003](../decisions/hdr/HDR-003-AeroSelfie-45A-ESC.md) |
| Motors | Brushless motors | HappyModel EX1404 | 4 | $55 | [Amazon](https://www.amazon.com/dp/B08QML2D7S) | [HDR-002](../decisions/hdr/HDR-002-HappyModel-EX1404-Motors.md) |
| Propellers | 3.5-inch propellers | Gemfan Hurricane 3520 | 8 | $14 | [Amazon](https://www.amazon.com/dp/B099F4YCX9) | [HDR-004](../decisions/hdr/HDR-004-Gemfan-Hurricane-3520-Props.md) |
| Batteries | Lithium-polymer batteries | Ovonic 850 mAh 4S | 2 | $25 | [Amazon](https://www.amazon.com/dp/B0C3J3T5C3) | [HDR-005](../decisions/hdr/HDR-005-4S-850mAh-Power-System.md) |
| Battery Charger | 4S-compatible LiPo charger | TBC | 1 | $24 | [Amazon](https://www.amazon.com/dp/B0GWT9WP6Q) | Not assigned |
| Mechanical Hardware | Stainless metric hardware kit | TBC | 1 | $9 | [Amazon](https://www.amazon.com/dp/B0D636MJ1N) | [HDR-006](../decisions/hdr/HDR-006-Mechanical-Hardware-Standard.md) |
| Mechanical Hardware | Brass heat-set inserts | TBC | 1 | $14 | [Amazon](https://www.amazon.com/dp/B0D5V3TZLB) | [HDR-006](../decisions/hdr/HDR-006-Mechanical-Hardware-Standard.md) |
| Mechanical Hardware | Nylon M2 standoff kit | TBC | 1 | $12 | [Amazon](https://www.amazon.com/dp/B07D78PFQL) | [HDR-006](../decisions/hdr/HDR-006-Mechanical-Hardware-Standard.md) |
| Wiring | 18 AWG silicone-insulated wire | TBC | 1 | $12 | [Amazon](https://www.amazon.com/dp/B0G4JWWVH7) | [HDR-007](../decisions/hdr/HDR-007-Wiring-Materials-Standard.md) |
| Wiring | 22 AWG silicone-insulated wire | TBC | 1 | $14 | [Amazon](https://www.amazon.com/dp/B01K4RP8PU) | [HDR-007](../decisions/hdr/HDR-007-Wiring-Materials-Standard.md) |
| Wiring | 24 AWG silicone-insulated wire | TBC | 1 | $8 | [Amazon](https://www.amazon.com/dp/B089CRSLG8) | [HDR-007](../decisions/hdr/HDR-007-Wiring-Materials-Standard.md) |

---

# 3. Cost Summary

| Cost Category | Recorded Cost |
| --- | ---: |
| Flight Controller | $27 |
| Development debugger | $25 |
| IMU | $10 |
| ESC | $26 |
| Motors | $55 |
| Propellers | $14 |
| Batteries | $25 |
| Battery charger | $24 |
| Mechanical hardware | $35 |
| Wiring | $34 |
| **Recorded total** | **$275** |

The recorded total represents the listed purchase costs and does not include:

- Taxes
- Shipping
- Consumables
- Replacement parts
- 3D-printing material
- Tools
- Test equipment
- Future communications hardware
- Future navigation sensors

---

# 4. Configuration Notes

## 4.1 Flight Controller

The exact manufacturer, board name, processor package, regulator arrangement, connector layout, and schematic revision of the STM32H743 development platform shall be confirmed in **ICD-001** before final pin allocation.

The processor designation alone does not completely define the Flight Controller board.

---

## 4.2 Development Debugger

The NUCLEO-F401RE is development equipment and is not intended to fly aboard the aircraft.

Its onboard ST-LINK/V2-1 interface is intended to program and debug the STM32H743 Flight Controller through SWD.

The Nucleo target section and external-target connection shall be configured according to the applicable ST documentation and **ADR-006**.

---

## 4.3 IMU Module

The exact ICM-20602 breakout-module manufacturer and electrical implementation shall be confirmed.

The following shall be verified before wiring:

- Supply-voltage requirements
- Logic-voltage compatibility
- Presence of onboard regulation
- Presence of level shifting
- Connector pinout
- SPI signal naming
- Interrupt availability
- Sensor orientation

---

## 4.4 Propulsion Components

Motor, ESC, propeller, and battery compatibility shall be confirmed through:

- Manufacturer-rating review
- Current and voltage analysis
- Propeller-free motor testing
- Controlled propulsion testing
- Temperature observation

---

## 4.5 Battery Charger

The exact charger manufacturer, model, supported cell count, balancing capability, input-power requirements, and safety documentation shall be recorded before it is treated as approved equipment.

---

# 5. Procurement Control

A retailer link is not the authoritative component specification.

Before accepting a substituted component, verify:

- Manufacturer
- Exact part or model number
- Voltage rating
- Current rating
- Dimensions
- Connector type
- Pinout
- Firmware compatibility
- Mechanical compatibility
- Applicable decision record

A materially different substitute shall receive engineering review and may require an updated ADR, HDR, ICD, requirement, or BOM revision.

---

# 6. References

- [SPEC-001 — Stratus Rev A System Specification](SPEC-001-Stratus-RevA.md)
- [REQ-001 — Stratus Rev A Requirements Specification](../requirements/REQ-001.md)
- [ARC-001 — Stratus System Architecture](../design/ARC-001-System-Architecture.md)
- [ICD-001 — Stratus Rev A Interface Control Document](../design/ICD-001-Interface-Control-Document.md)
- [RTM-001 — Requirements Traceability Matrix](../requirements/RequirementsTraceabilityMatrix.md)
- [SES-001 — Mechanical Engineering Standard](../standards/SES-001-Hardware.md)
- [SES-002 — Electrical Engineering Standard](../standards/SES-002-Wiring.md)
- ADR Series
- HDR Series

---

# 7. Related Documents

## Upstream

- SPEC-001
- REQ-001

## Peer

- ARC-001
- ICD-001
- SES-001
- SES-002

## Supporting Decisions

- ADR-001
- ADR-006
- HDR-001
- HDR-002
- HDR-003
- HDR-004
- HDR-005
- HDR-006
- HDR-007

## Downstream

- Wiring diagram
- Harness definitions
- Assembly procedure
- Hardware configuration record
- Bring-up procedures
- Verification records