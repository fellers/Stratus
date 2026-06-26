# Decision

- Develop a custom flight software stack specifically for Stratus rather than relying on an existing flight control implementation.

# Status

- Accepted

# Context

The primary objective of Stratus is to serve as an educational and engineering platform for embedded systems, robotics, autonomous control, and aerospace software development.

While mature open-source flight stacks provide production-ready functionality, they abstract many of the engineering challenges that this project is intended to explore. Developing the flight software from first principles provides significantly greater educational value and enables complete ownership of the software architecture.

## Selection Criteria

- Educational value
- Software ownership
- System understanding
- Extensibility
- Long-term maintainability
- Portfolio value

# Decision Criteria

- Complete ownership of all flight software
- Deep understanding of embedded software architecture
- Ability to optimize software for Stratus-specific hardware
- Support for future autonomous capabilities
- Demonstrates embedded software engineering proficiency

# Alternatives Considered

## ArduPilot

### Pros

- Mature and feature rich
- Large community
- Extensive hardware support

### Cons

- Significant software complexity
- Reduced educational value
- Less ownership of the flight stack

## Betaflight

### Pros

- Excellent flight performance
- Large FPV community
- Well optimized

### Cons

- Primarily designed for manual FPV flight
- Limited focus on autonomous systems
- Less suitable for long-term research objectives

## PX4

### Pros

- Modern architecture
- Strong autonomous capabilities
- Professional ecosystem

### Cons

- Large codebase
- Steep learning curve
- Reduced opportunity to design core flight software

# Consequences

## Advantages

- Complete understanding of every software subsystem
- Highly modular architecture
- Excellent portfolio project
- Easier experimentation with new control algorithms
- Software architecture tailored specifically to Stratus

## Disadvantages

- Significantly increased development effort
- Longer time to first flight
- Requires implementation of foundational flight algorithms

# Future Considerations

As Stratus evolves, the custom flight software should remain modular, testable, and hardware-agnostic where practical. New capabilities such as GPS navigation, computer vision, mission planning, and swarm coordination should build upon the same software architecture established in Rev A.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |