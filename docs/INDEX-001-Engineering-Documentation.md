# Stratus Engineering Documentation Index

**Document ID:** INDEX-001

**Revision:** 1.0

**Status:** Draft

**Classification:** Public

**Project:** Stratus

**Author:** Austin Fellows

**Created:** 2026-06-27

**Last Updated:** 2026-06-27

---

# Purpose

This document serves as the master index for all engineering documentation associated with the Stratus project.

The purpose of this document is to provide a single point of entry into the engineering documentation package and define the relationships between specifications, requirements, architecture, standards, decision records, and future verification artifacts.

---

# Documentation Hierarchy

```text
Project Philosophy
        │
        ▼
SPEC-001
        │
        ▼
REQ-001
        │
        ▼
ARC-001
        │
        ├── SES Series
        ├── ADR Series
        ├── HDR Series
        └── Implementation
                │
                ▼
            Verification
                │
                ▼
            Flight Test
```

---

# Specifications

| Document | Description |
| --- | --- |
| SPEC-001 | Stratus Rev A System Specification |
| REQ-001 | Requirements Specification |
| ARC-001 | System Architecture |
| BOM-001 | Bill of Materials |

---

# Standards

| Document | Description |
| --- | --- |
| SES-001 | Mechanical Engineering Standard |
| SES-002 | Electrical Engineering Standard |

---

# Architecture Decision Records

| Document | Description |
| --- | --- |
| ADR-001 | STM32H743 Architecture |
| ADR-002 | Rev A Platform Size |
| ADR-003 | Modular Airframe Architecture |
| ADR-004 | Custom Flight Software |
| ADR-005 | Flight Stack Strategy |

---

# Hardware Decision Records

| Document | Description |
| --- | --- |
| HDR-001 | ICM-20602 IMU |
| HDR-002 | HappyModel EX1404 Motors |
| HDR-003 | Aero Selfie 45A ESC |
| HDR-004 | Gemfan Hurricane 3520 Propellers |
| HDR-005 | 4S Power System |
| HDR-006 | Mechanical Hardware |
| HDR-007 | Wiring Materials |

---

# Future Documentation

- Requirements Traceability Matrix
- Verification and Validation Plan
- Flight Test Procedures
- Integration Test Reports
- Bring-Up Procedures
- CAD Documentation
- PCB Design Documentation
- Simulation Documentation
- Build Logs
- Flight Logs

---

# Related Documents

## Upstream

- README.md

## Peer

- SPEC-001
- REQ-001
- ARC-001

## Supporting

- ADR Series
- HDR Series
- SES Series