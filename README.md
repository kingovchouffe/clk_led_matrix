# GNSS LED Matrix Clock Hardware

This repository contains KiCad hardware designs for a GNSS-oriented clock and LED matrix display. The primary design combines an STM32C0-series controller with an ATGM336H GNSS receiver; separate files capture a CH32V003-based 5x7 display design.

## Designs

### Main clock controller

The root KiCad project (`clk_led_matrix`) contains the main schematic, PCB layout, and an STM32CubeMX configuration. The schematic includes:

- An STM32C0-series MCU and ATGM336H-5N31 GNSS module.
- GNSS UART and I2C signal connections, plus USB 2.0 over a USB-C receptacle.
- Power circuitry, a reset switch, and a 2x3 debug/programming header.
- A four-layer PCB layout.

The `.ioc` file configures RTC, USB device, two I2C peripherals, and two UART peripherals. It is MCU configuration metadata, not firmware source code.

### CH32 LED display design

The `ch32_led/` directory contains a separate two-layer KiCad project built around a CH32V003 and a Lite-On LTP-305G green 5x7 dot-matrix display. Its schematic also includes a three-position DIP switch, address-selection signals, and a six-pin connector.

`5x7_MCU_Block.kicad_sch` is a standalone schematic for the CH32V003/display circuit, useful as a reference or reusable block. It is not a hierarchical sheet currently included in the root schematic.

## Repository contents

| Path | Description |
| --- | --- |
| `clk_led_matrix.kicad_pro` | Main KiCad project settings |
| `clk_led_matrix.kicad_sch` | Main clock-controller schematic |
| `clk_led_matrix.kicad_pcb` | Main four-layer PCB layout |
| `clk_led_matrix.ioc` | STM32CubeMX configuration for the main MCU |
| `ch32_led/` | Separate CH32V003 5x7 display schematic and PCB project |
| `5x7_MCU_Block.kicad_sch` | Standalone CH32V003 and 5x7 display schematic block |
| `fp-lib-table` | KiCad footprint library table |

## Opening the designs

Open `clk_led_matrix.kicad_pro` in KiCad to work on the main design. Open `ch32_led/ch32_led.kicad_pro` for the CH32 display board. The design files use KiCad 10-era file formats; older KiCad versions may not open them correctly.

The repository currently contains hardware design files, not embedded application source, generated firmware, a bill of materials, or fabrication exports. No firmware build or flashing procedure is defined here.

## Design note

Before ordering parts for the main controller, verify the exact STM32 package: the schematic symbol is named `STM32C071KBUx`, while `clk_led_matrix.ioc` identifies `STM32C071KBT6`. Confirm that the schematic, footprint, PCB, and MCU configuration all target the intended orderable part.