# STM32F4-TEST BOARD

A compact STM32F405-based development/test board designed in **KiCad 10**. It breaks out the essentials needed to prototype and debug STM32F4 firmware: on-board power regulation, USB, SWD debugging, I²C and UART headers, and status LEDs.

**Author:** Vigneshwar G
**Revision:** 1.0
**Date:** 2026-11-17
**EDA:** KiCad 10.0.5

---

## Features

- **MCU:** STM32F405RGT6 (ARM Cortex-M4F, LQFP-64)
- **Power input:** 12 V via 2-pin screw terminal (J1), with P-MOSFET reverse-polarity protection (AO3401A) and fuse/ferrite filtering
- **Regulation:** MP2359DJ-LF-Z1 buck converter to 3.3 V, with inductor, Schottky diode and resistor-divider feedback
- **Power indicator:** Red LED on the 3.3 V rail
- **USB:** Micro-USB B connector (J5) with USBLC6-2SC6 ESD protection, connected to the MCU's USB D+/D- pins
- **Debug:** SWD header (J2) with SWDIO, SWCLK, SWO and NRST
- **Boot control:** SPDT switch (SW1) for BOOT0 selection
- **Clock:** External HSE crystal (Y1) with load capacitors
- **Expansion headers:**
  - J3: I²C1 (SCL/SDA) with 2.2 kΩ pull-ups
  - J4: USART3 (TX/RX)
- **LEDs:** Status LED and run indicator
- **Mechanical:** 4× mounting holes (H1–H4), rounded-corner board outline

## Repository Structure

```
.
├── STM32F4_testt.kicad_pro     # KiCad project
├── STM32F4_testt.kicad_sch     # Schematic
├── STM32F4_testt.kicad_pcb     # PCB layout
├── fp-lib-table / sym-lib-table
├── libraries/                  # Custom symbols & footprints (if any)
├── gerbers/                    # Manufacturing outputs
├── docs/                       # Schematic PDF, screenshots, BOM
└── README.md
```

> Adjust the structure above to match your actual folders.

## Pin Overview

| Function | Header / Part | MCU Pins |
|----------|---------------|----------|
| SWD | J2 | SWDIO, SWCLK, SWO, NRST |
| I²C1 | J3 | PB6 (SCL), PB7 (SDA) |
| USART3 | J4 | PB10 (TX), PB11 (RX) |
| USB | J5 | PA11 (D-), PA12 (D+) |
| BOOT0 | SW1 | BOOT0 |
| HSE crystal | Y1 | PH0 / PH1 |

> Verify against the schematic before wiring.

## Getting Started

### Requirements
- [KiCad 10.x](https://www.kicad.org/)
- An ST-Link (or compatible SWD probe) for programming
- 12 V DC supply (or USB 5 V for USB-only testing, depending on your power routing)

### Open the project
```bash
git clone https://github.com/<your-username>/STM32F4-Test-Board.git
cd STM32F4-Test-Board
```
Open `STM32F4_testt.kicad_pro` in KiCad.

### Programming
1. Connect an ST-Link to the SWD header (J2).
2. Power the board.
3. Flash using STM32CubeProgrammer, OpenOCD, or STM32CubeIDE.

To use the USB DFU bootloader, set SW1 to pull BOOT0 high, reset the board, and connect via USB.

## Hardware Notes

- Place the 3.3 V buck converter's switching loop (inductor, diode, input/output caps) as tightly as possible.
- Decoupling capacitors are placed close to each VDD pin.
- USB differential pair should be routed with matched length and controlled impedance.
- Check polarity of the screw terminal before applying power.

## Status

- [x] Schematic complete
- [x] PCB layout
- [ ] Fabrication
- [ ] Bring-up and firmware testing

## Screenshots

Add images to `docs/` and reference them here:

```markdown
![Schematic](docs/schematic.png)<img width="1217" height="837" alt="Screenshot 2026-11-17 203849" src="https://github.com/user-attachments/assets/6bd35043-40f3-4751-a537-6def25fa506d" />

![PCB](docs/pcb.png)<img width="1217" height="837" alt="Screenshot 2026-11-17 203849" src="https://github.com/user-attachments/assets/6e95302a-ea00-4181-ae5e-0bebf2b9f333" />

```

## License

Released under the MIT License (or choose your own, e.g. CERN-OHL-P for hardware). Add a `LICENSE` file to the repository.

## Acknowledgements

- STMicroelectronics STM32F4 documentation
- Monolithic Power Systems MP2359 datasheet
- KiCad community libraries
