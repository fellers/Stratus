# Decision

- Adopt a 4S 850mAh XT30 LiPo battery platform as the standard power system for Stratus Rev A.

# Status

- Accepted

# Context

The aircraft power system must provide sufficient energy for stable flight while balancing weight, flight time, safety, and future scalability.

Rather than selecting a battery solely for maximum flight time, Stratus prioritizes rapid development, low replacement cost, and compatibility with the 3.5-inch platform.

## Selection Criteria

- Weight
- Flight time
- Cost
- Availability
- Community adoption
- Connector standard
- Future scalability

# Decision Criteria

- 4S provides excellent performance for the selected propulsion system.
- 850mAh capacity balances endurance and weight.
- XT30 connectors are widely adopted for aircraft in this size class.
- Batteries are readily available from multiple manufacturers.
- Low replacement cost encourages experimentation during development.

# Alternatives Considered

## Larger Capacity 4S Batteries (1000–1500mAh)

### Pros

- Longer flight times
- Greater energy capacity

### Cons

- Increased weight
- Reduced agility
- Larger airframe requirements

## 3S Battery Platform

### Pros

- Lower cost
- Lower operating voltage

### Cons

- Reduced motor performance
- Lower thrust margin
- Less representative of modern FPV platforms

## 6S Battery Platform

### Pros

- Higher efficiency
- Lower current draw

### Cons

- Increased system cost
- Larger batteries
- Outside the educational objectives of Rev A

# Consequences

## Advantages

- Excellent balance between performance and weight
- Large ecosystem of compatible components
- Low replacement cost
- Easily scalable to future revisions

## Disadvantages

- Shorter endurance than larger battery configurations
- May require larger batteries for future payload-heavy revisions

# Future Considerations

Future Stratus revisions should maintain connector compatibility where practical while evaluating larger battery capacities or higher voltage platforms as mission requirements evolve.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |