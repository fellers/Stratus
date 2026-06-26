# Decision

- Do not use an existing flight stack as the primary flight software for Stratus. Existing flight stacks may be referenced for research and validation but will not be integrated into the production firmware.

# Status

- Accepted

# Context

Numerous open-source flight stacks exist that provide complete flight control implementations. While these projects represent excellent engineering efforts, adopting them would shift the focus of Stratus from engineering the platform to integrating existing software.

The project objective is to understand and implement the complete flight software stack from sensor acquisition through autonomous mission execution.

## Selection Criteria

- Alignment with project philosophy
- Educational value
- Engineering ownership
- Architectural flexibility
- Long-term maintainability

# Decision Criteria

- Preserve first-principles engineering approach
- Encourage implementation of core algorithms
- Maintain complete control over software architecture
- Avoid unnecessary architectural constraints imposed by existing projects

# Alternatives Considered

## Adopt ArduPilot

### Pros

- Immediate flight capability
- Extensive documentation
- Proven reliability

### Cons

- Large inherited codebase
- Reduced engineering ownership
- Less opportunity to design core systems

## Fork ArduPilot

### Pros

- Existing infrastructure
- Faster development

### Cons

- High maintenance burden
- Complex upstream synchronization
- Project identity becomes tied to another codebase

## Hybrid Architecture

### Pros

- Faster development
- Reuse mature components

### Cons

- Mixed architectural philosophies
- Increased integration complexity
- Reduced educational benefit

# Consequences

## Advantages

- Independent software architecture
- Consistent engineering philosophy
- Improved understanding of flight systems
- Greater flexibility for future experimentation

## Disadvantages

- Increased implementation effort
- Additional verification and testing required
- Longer path to autonomous flight

# Future Considerations

Research into existing flight stacks should continue throughout the project to compare algorithms, validate implementation approaches, and identify industry best practices. However, Stratus should remain an independently developed flight software platform.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |