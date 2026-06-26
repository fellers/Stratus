# Decision

- Standardize the mechanical hardware used throughout Stratus to simplify manufacturing, maintenance, and future revisions.

# Status

- Accepted

# Context

A consistent hardware standard reduces assembly complexity, minimizes required tooling, and improves interchangeability between future hardware revisions.

Mechanical standardization also supports the project's modular design philosophy.

## Selection Criteria

- Simplicity
- Availability
- Durability
- Cost
- Manufacturability
- Modularity

# Decision Criteria

- M2 fasteners for electronics
- M3 fasteners for structural assemblies
- Brass heat-set inserts for all removable printed components
- Nylon standoffs for PCB mounting
- Stainless steel fasteners throughout the airframe

# Alternatives Considered

## Mixed Fastener Sizes

### Pros

- Optimized for individual components

### Cons

- Increased inventory
- More assembly complexity
- Additional tooling requirements

## Threaded Plastic Components

### Pros

- Reduced component count

### Cons

- Lower durability
- Limited service life
- Poor suitability for repeated maintenance

# Consequences

## Advantages

- Simplified maintenance
- Reduced spare hardware inventory
- Consistent CAD design practices
- Improved modularity

## Disadvantages

- Slight increase in hardware cost
- Some components may use larger fasteners than strictly required

# Future Considerations

Future Stratus revisions should preserve the M2/M3 hardware philosophy whenever practical to maintain compatibility across modules and simplify maintenance.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |