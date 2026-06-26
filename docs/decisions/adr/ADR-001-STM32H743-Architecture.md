# Decision

- Use the STM32H743 as the primary flight controller architecture for Stratus Rev A.

# Status

- Accepted

# Context

The flight controller serves as the central processing unit for all aircraft functions, including sensor acquisition, state estimation, control loops, motor output, telemetry, and future autonomous navigation.

The selected platform must support future software complexity while remaining suitable for learning low-level embedded development.

# Selection Criteria

- Processing performance
- Memory capacity
- Peripheral availability
- Community support
- Long-term scalability
- Development ecosystem
- Compatibility with future custom PCB design

# Decision Criteria

- High-performance Cortex-M7 processor
- Large Flash and RAM capacity
- Multiple SPI, UART, I2C, CAN and timer peripherals
- Excellent STM32CubeIDE support
- Extensive documentation
- Large embedded systems community
- Sufficient headroom for future autonomous capabilities

# Alternatives Considered

## STM32H723

### Pros

- Lower cost
- Similar architecture
- High performance

### Cons

- Reduced RAM
- Fewer available peripherals
- Less long-term expansion headroom

## STM32F405/F411

### Pros

- Extremely common
- Large hobby ecosystem
- Lower cost

### Cons

- Significantly lower processing capability
- Less memory
- Limited future scalability

## Pixhawk Flight Controller

### Pros

- Mature ecosystem
- Proven flight hardware
- Ready to fly

### Cons

- Reduces educational value
- Limited hardware ownership
- Does not support long-term custom PCB objectives

# Consequences

## Advantages

- Significant performance headroom
- Supports future custom flight software
- Enables future computer vision and advanced navigation
- Direct migration path to a custom PCB

## Disadvantages

- Slightly higher cost
- Larger learning curve than prebuilt flight controllers

# Future Considerations

Future Stratus revisions should maintain firmware portability by abstracting hardware-specific interfaces to simplify migration to custom STM32H743-based PCBs.

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 2026-06-26 | Initial decision |