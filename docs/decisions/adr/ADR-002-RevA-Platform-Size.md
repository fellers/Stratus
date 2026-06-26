# Decision

- Adopt a 3.5-inch quadcopter platform for Stratus Rev A.

# Status

- Accepted

# Context

The first hardware revision is intended to validate the flight software, electronics architecture, and modular design philosophy while minimizing development cost and crash risk.

## Selection Criteria

- Cost
- Manufacturability
- Crash survivability
- Flight stability
- Component availability
- Future scalability

# Decision Criteria

- Reduced component cost
- Lower kinetic energy during crashes
- Compatible with desktop 3D printing
- Adequate payload capacity for Rev A electronics
- Simple transition to a future 5-inch platform

# Alternatives Considered

## 5-inch Platform

### Pros

- Greater payload capacity
- Longer flight times
- Higher performance

### Cons

- More expensive
- Larger crash energy
- Larger frame and motors

## 2.5-inch Platform

### Pros

- Extremely compact
- Low cost
- Indoor capable

### Cons

- Limited payload capacity
- Reduced expansion potential
- Tighter packaging constraints

# Consequences

## Advantages

- Fast development iteration
- Affordable replacement components
- Simplified manufacturing
- Supports educational objectives

## Disadvantages

- Limited payload margin
- Shorter endurance than larger aircraft

# Future Considerations

The modular architecture should support migration to a 5-inch platform while preserving as much software and electronics infrastructure as practical.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |