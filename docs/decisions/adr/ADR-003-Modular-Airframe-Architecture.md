# Decision

- Design Stratus around a modular airframe architecture with standardized mounting interfaces.

# Status

- Accepted

# Context

Stratus is intended to serve as a long-term engineering platform rather than a single aircraft design. Individual subsystems should be replaceable without redesigning the entire vehicle.

## Selection Criteria

- Maintainability
- Expandability
- Ease of prototyping
- Component reuse
- Manufacturing simplicity

# Decision Criteria

- Replaceable modules
- Standardized mounting patterns
- Heat-set insert integration
- Future custom PCB compatibility
- Independent subsystem development

# Alternatives Considered

## Integrated Monolithic Frame

### Pros

- Lower weight
- Higher structural rigidity

### Cons

- Difficult repairs
- Poor upgrade path
- Requires complete redesign for major changes

## Commercial Off-the-Shelf Frame

### Pros

- Proven geometry
- Minimal design effort

### Cons

- Limited customization
- Does not support project objectives
- Reduced educational value

# Consequences

## Advantages

- Faster hardware iteration
- Easier maintenance
- Reusable modules
- Supports future payload expansion

## Disadvantages

- Slight increase in weight
- Increased CAD complexity

# Future Considerations

Future revisions should preserve module interfaces wherever practical to maintain backwards compatibility across the Stratus platform.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |