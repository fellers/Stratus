# Decision

- Use the ICM-20602 as the primary inertial measurement unit (IMU) for Stratus Rev A

# Status

- Accepted

# Context

The flight controller requires a six-axis inertial measurement unit capable of providing low-latency gyroscope and accelerometer data for attitude estimation and stabilization.

## Selection criteria included:

- SPI support
- Community adoption
- Availability
- Cost
- Long-term software support
- Compatibility with STM32H743

# Decision Criteria

- Low cost
- SPI interface
- Proven in numerous flight controllers
- Well-understood characteristics
- Excellent documentation
- Suitable update rates for high-frequency control loops

# Alternatives Considered

## ICM-42688-P

### Pros

- Lower noise
- More modern

### Cons

- More Expensive
- Long shipping times
- Less readily available

## BMI160

### Pros

- Common

### Cons

- Mixed reputation
- Less common in modern FPV flight controllers

## BN0080

### Pros

- Built in sensor fusion

### Cons

- Removes educational value
- Additional complexity
- Less control over estimation algorithms

# Consequences

## Advantages

- Mature device
- Plenty of example code
- Supports educational objectives
- Easy to replace

## Disadvantages

- Higher noise than newest IMUs
- Future revisions may migrate to newer devices

# Future Considerations

Stratus Rev C custom PCB should support replacing the ICM-20602 with newer SPI-compatible IMUs through abstraction layer

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |