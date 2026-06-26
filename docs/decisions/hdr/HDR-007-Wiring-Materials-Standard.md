# Decision

- Standardize the wiring materials and conductor specifications used throughout Stratus.

# Status

- Accepted

# Context

The aircraft electrical system requires flexible, durable wiring capable of withstanding vibration while remaining easy to assemble and maintain.

Standardizing wire materials and gauge selection simplifies manufacturing and reduces wiring errors.

## Selection Criteria

- Flexibility
- Durability
- Solderability
- Weight
- Current capacity
- Availability

# Decision Criteria

- Silicone insulation throughout the aircraft
- Stranded tinned copper conductors
- 18 AWG for battery power distribution
- 22 AWG for moderate-current accessory wiring
- 24 AWG for sensors and communication interfaces
- Standardized color coding across all revisions

# Alternatives Considered

## PVC Insulated Wire

### Pros

- Lower cost
- Readily available

### Cons

- Reduced flexibility
- Lower heat resistance
- More difficult routing

## Solid Core Wire

### Pros

- Easy breadboard prototyping

### Cons

- Unsuitable for vibration environments
- Increased risk of fatigue failure

## Copper-Clad Aluminum (CCA)

### Pros

- Lower cost
- Lightweight

### Cons

- Higher electrical resistance
- Reduced durability
- Inferior solderability

# Consequences

## Advantages

- Improved reliability
- Simplified wiring practices
- Easier maintenance
- Better soldering performance
- Consistent electrical architecture

## Disadvantages

- Slightly higher material cost
- Requires maintaining multiple wire gauges

# Future Considerations

Future Stratus revisions should preserve the existing wiring standards while expanding connector standards and modular harnesses as the electrical architecture becomes more sophisticated.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |