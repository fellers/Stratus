# Decision

- Use the Aero Selfie 45A 4-in-1 Electronic Speed Controller (ESC) as the primary motor controller for Stratus Rev A.

# Status

- Accepted

# Context

The ESC converts flight controller motor commands into three-phase power for each brushless motor. A single 4-in-1 ESC simplifies wiring, reduces weight, and improves packaging compared to four independent ESCs.

## Selection Criteria

- Current capacity
- Reliability
- Wiring simplicity
- Cost
- Community adoption
- Future compatibility

# Decision Criteria

- 45A current rating provides significant headroom
- Integrated 4-in-1 design simplifies wiring
- Compact form factor
- Compatible with DShot protocols
- Suitable for future platform expansion

# Alternatives Considered

## Individual ESCs

### Pros

- Easier replacement of individual failures
- Greater layout flexibility

### Cons

- Increased wiring complexity
- Higher weight
- Larger packaging volume

## Lower Current 20A–30A ESCs

### Pros

- Lower cost
- Slightly lighter

### Cons

- Reduced safety margin
- Limited future scalability

# Consequences

## Advantages

- Simplified electrical architecture
- Reduced assembly complexity
- Supports future propulsion upgrades
- Provides ample current headroom

## Disadvantages

- Failure requires replacement of the complete ESC assembly
- Higher cost than lower-current alternatives

# Future Considerations

Future revisions should maintain compatibility with digital ESC protocols while evaluating integrated current sensing and telemetry features.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |