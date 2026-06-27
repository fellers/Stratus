# Stratus STM32 Bring-Up Notes

## Board

- MCU: STM32H743XIH6
- Board: EC Buying STM32H743XIH6 development board
- Debug: DFU currently, ST-Link pending
- USB: DFU in FS Mode confirmed on macOS

## Bring-Up Status

- CubeIDE project created
- Project builds successfully
- Binary output generated
- STM32CubeProgrammer connects over USB DFU
- Firmware successfully flashed to address `0x08000000`

## Next Steps

- Connect ST-Link
- Confirm debug connection
- Halt at `main()`
- Add external LED blink
- Bring up UART
- Bring up SPI
- Read ICM-20602 WHO_AM_I register