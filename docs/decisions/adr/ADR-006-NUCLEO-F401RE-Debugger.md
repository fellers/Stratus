# Use the NUCLEO-F401RE as the Rev A Development Debugger

**Document ID:** ADR-006  
**Revision:** 1.0  
**Status:** Accepted  
**Classification:** Public  
**Project:** Stratus  
**Author:** Austin Fellows  
**Created:** 2026-08-02  
**Last Updated:** 2026-08-02  

---

# Revision History

| Version | Date | Description | Author |
| --- | --- | --- | --- |
| 1.0 | 2026-08-02 | Initial decision to use the NUCLEO-F401RE onboard ST-LINK for external-target debugging | Austin Fellows |

---

# Approval

| Role | Name | Status |
| --- | --- | --- |
| Systems Engineer | Austin Fellows | Accepted |

---

# 1. Title

Use the NUCLEO-F401RE Onboard ST-LINK/V2-1 as the Stratus Rev A Development Debugger

---

# 2. Status

**Accepted**

---

# 3. Context

Stratus Rev A uses an STM32H743-class Flight Controller.

Firmware development requires a reliable interface for:

- Firmware programming
- Processor reset
- Breakpoints
- Single-step execution
- Register inspection
- Memory inspection
- Fault diagnosis
- Startup debugging
- Recovery from invalid firmware

An earlier generic ST-Link-compatible debugger did not provide sufficiently reliable operation for continued development.

A genuine STMicroelectronics debugging solution was therefore required.

The selected product is:

```text
STMicroelectronics NUCLEO-F401RE
STM32 Nucleo-64 development board
Onboard STM32F401RE MCU
Onboard ST-LINK/V2-1 debugger/programmer
ST Morpho and Arduino-compatible connectivity
```

The NUCLEO-F401RE is not being selected as the Stratus Flight Controller.

It is being selected as development equipment whose onboard ST-LINK/V2-1 section can be configured to program and debug an external STM32 target through Serial Wire Debug.

---

# 4. Decision

Stratus Rev A development shall use the onboard ST-LINK/V2-1 debugger/programmer of a genuine STMicroelectronics NUCLEO-F401RE board as the primary external SWD debugger for the STM32H743 Flight Controller.

The NUCLEO-F401RE target MCU shall not perform flight-control functions.

The Nucleo board shall remain external development equipment and shall not be installed on the flight vehicle.

---

# 5. Decision Drivers

The decision is based on the following factors:

- Genuine STMicroelectronics hardware
- Compatibility with STM32 development tools
- Integrated ST-LINK/V2-1 debugger/programmer
- Support for SWD programming and debugging
- Target reset capability
- Firmware-upgradable debugger
- Availability of official board documentation
- Lower risk than an unverified clone debugger
- Ability to reuse the Nucleo board for other STM32 experiments
- Reasonable procurement cost
- Immediate availability

---

# 6. Intended Use

The onboard ST-LINK/V2-1 shall support:

- Programming the STM32H743 Flight Controller
- Erasing target flash
- Debugging startup behavior
- Setting breakpoints
- Single-stepping firmware
- Inspecting processor registers
- Inspecting variables and memory
- Observing processor faults
- Resetting the target
- Recovering from invalid firmware where SWD remains available

The interface may be used with:

- STM32CubeProgrammer
- STM32CubeIDE
- OpenOCD-compatible development workflows
- Visual Studio Code debugging tools
- Other compatible STM32 development software

Tool use remains subject to successful configuration and target support.

---

# 7. External-Target Interface

The required external-target signals are:

| Signal | Purpose | Direction Relative to STM32H743 Target |
| --- | --- | --- |
| SWDIO | Serial Wire Debug data | Bidirectional |
| SWCLK | Serial Wire Debug clock | Input to target |
| GND | Common electrical reference | Reference |
| VTREF | Target logic-voltage reference | Supplied as a reference by target |
| NRST | Target reset | Input to target |

At minimum, SWDIO, SWCLK, GND, and a compatible target-voltage reference shall be provided.

NRST should be connected to improve reset and recovery behavior.

---

# 8. Configuration Constraints

Before connecting the NUCLEO-F401RE to the STM32H743 target:

1. Confirm the Nucleo board revision.
2. Consult the applicable ST user manual and board schematic.
3. Configure the onboard ST-LINK for external-target use.
4. Isolate or disconnect the Nucleo target MCU from the ST-LINK signals as required by the documented jumper arrangement.
5. Confirm target and debugger ground continuity.
6. Confirm that the STM32H743 target logic voltage is compatible.
7. Connect VTREF as a voltage reference rather than assuming it is a target power source.
8. Prevent unintended back-powering through SWD, USB, or another attached interface.
9. Verify SWDIO and SWCLK orientation before applying power.
10. Connect NRST when supported by the target.
11. Begin with the aircraft propulsion battery disconnected.
12. Keep propellers removed during firmware bring-up.

Exact jumper positions and connector pins shall be recorded in **ICD-001** after the physical NUCLEO-F401RE board revision is inspected.

---

# 9. Power Policy

The NUCLEO-F401RE shall not be assumed to power the STM32H743 Flight Controller through the SWD interface.

The STM32H743 target shall use a defined and verified power source.

The debugger shall receive the target-voltage reference required to determine the target I/O level.

Before simultaneous connection of:

- Nucleo USB power
- STM32H743 USB power
- External bench power
- Aircraft regulated power
- Propulsion battery power

the permitted power paths and back-powering risks shall be reviewed.

---

# 10. Safety Behavior

Debugger connection, disconnection, reset, halt, erase, or programming shall not intentionally command motor rotation.

During development-debugger use:

- Propellers shall be removed.
- Motor outputs shall default to a non-commanding state.
- The propulsion battery should remain disconnected unless specifically required by a controlled test.
- Initial powered tests should use current limiting where practical.
- SWD wiring shall be checked before power is applied.
- The debugger and target shall share ground.
- Unsupported voltage shall not be applied to target pins.

---

# 11. Alternatives Considered

## 11.1 Continue Using the Generic Debugger

**Rejected**

The generic debugger had already created reliability concerns.

Continued use would increase uncertainty during firmware bring-up because failures could originate from either:

- Target firmware
- Target hardware
- Debugger hardware
- Debugger firmware
- USB communication
- Tool compatibility

A genuine ST development board reduces debugger uncertainty.

---

## 11.2 Purchase a Standalone Genuine ST-LINK

**Not selected for Rev A**

A standalone genuine ST-LINK would also satisfy the primary need.

The NUCLEO-F401RE was selected because it provides:

- A genuine onboard ST-LINK
- A separate STM32 development target
- General-purpose development capability
- Acceptable cost and availability

A standalone probe may still be purchased later.

---

## 11.3 Use USB DFU Exclusively

**Rejected as the primary development method**

USB DFU may support programming and recovery, but it does not replace full source-level debugging.

DFU does not provide the same breakpoint, stepping, register-inspection, and fault-analysis capabilities as SWD.

---

## 11.4 Use the NUCLEO-F401RE as the Flight Controller

**Rejected**

The NUCLEO-F401RE is too large and mechanically unsuitable for the intended Rev A aircraft integration.

The STM32F401RE target MCU also does not represent the selected STM32H743 Flight Controller architecture.

The board is development equipment only.

---

# 12. Consequences

## 12.1 Positive Consequences

- Provides a genuine ST debugging implementation
- Reduces uncertainty caused by clone hardware
- Supports STM32 programming and source-level debugging
- Provides reset and recovery support
- Integrates with the STM32 development ecosystem
- Provides a secondary STM32 development platform
- Avoids immediate purchase of a more expensive standalone probe

## 12.2 Negative Consequences

- Requires correct external-target jumper configuration
- Requires a temporary SWD harness
- Occupies more bench space than a standalone probe
- Creates a possible back-powering risk if power paths are misunderstood
- Requires documentation of the exact Nucleo board revision
- The Nucleo target section must be isolated correctly during external-target use

## 12.3 Neutral Consequences

- The NUCLEO-F401RE does not alter the selected flight processor.
- Flight firmware still targets the STM32H743.
- The Nucleo board is not part of the flight mass or aircraft BOM configuration.
- USB DFU remains a possible secondary recovery path.

---

# 13. Verification

This decision shall be verified through the following sequence:

1. Identify the exact NUCLEO-F401RE board revision.
2. Update the onboard ST-LINK firmware if required.
3. Configure the ST-LINK for external-target operation.
4. Connect ground and target-voltage reference.
5. Connect SWDIO and SWCLK.
6. Connect NRST where available.
7. Apply verified power to the STM32H743 target.
8. Confirm that the target is detected.
9. Read the target device identification.
10. Erase target flash.
11. Program a minimal test image.
12. Reset and run the target.
13. Halt the processor.
14. Set and reach a breakpoint.
15. Single-step firmware.
16. Inspect registers and memory.
17. Confirm that motor-control outputs remain non-commanding.

The verification record should be identified as:

```text
VER-HW-001 — Flight Controller Programming and Debug Test
```

---

# 14. Interface-Control Actions

The following information shall be added to **ICD-001**:

- NUCLEO-F401RE board revision
- ST-LINK external-target jumper configuration
- Nucleo connector or header pin numbers
- STM32H743 SWD connector pinout
- SWDIO connection
- SWCLK connection
- NRST connection
- Ground connection
- VTREF connection
- Target power source
- Permitted simultaneous USB and power connections

---

# 15. Traceability

This decision supports:

- REQ-COM-001 — SWD Programming Support
- REQ-COM-002 — SWD Debug Support
- REQ-COM-003 — Reset Access
- REQ-HW-013 — Debug Access
- REQ-HW-042 — SWD Debugger Compatibility
- REQ-HW-043 — External Debug Connection
- REQ-HW-054 — No Unintended Propulsion
- REQ-EL-022 — Debug Ground
- REQ-EL-051 — SWD Signals
- REQ-EL-052 — Debug Voltage Compatibility
- REQ-EL-053 — Debug Power Clarification
- REQ-EL-054 — Multiple-Power-Source Prevention
- REQ-SW-066 — Software Reset Safety
- ICD-001 — Debug and Programming Interfaces
- RTM-001 — Requirements Traceability Matrix

---

# 16. References

- STMicroelectronics, **NUCLEO-F401RE Product Page**  
  <https://www.st.com/en/evaluation-tools/nucleo-f401re.html>

- STMicroelectronics, **STM32 Nucleo-64 Board User Manual**, applicable MB1136 revision

- STMicroelectronics, **STM32F401RE Product Documentation**

- STM32CubeProgrammer documentation

- STM32CubeIDE documentation

---

# 17. Related Documents

## Upstream

- SPEC-001 — Stratus Rev A System Specification
- REQ-001 — Stratus Rev A Requirements Specification
- ARC-001 — Stratus System Architecture

## Peer

- ADR-001 — STM32H743 Architecture
- ICD-001 — Stratus Rev A Interface Control Document
- BOM-001 — Stratus Rev A Bill of Materials

## Supporting Requirements

- REQ-FR-004 — Communications Functional Requirements
- REQ-HW-001 — Hardware Requirements
- REQ-SW-001 — Software Requirements
- REQ-EL-001 — Electrical Requirements

## Downstream

- VER-HW-001 — Flight Controller Programming and Debug Test
- SWD harness definition
- External-target connection diagram
- STM32H743 bring-up notes