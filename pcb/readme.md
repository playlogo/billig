# Kontakt - Fan & LED control board

| <img src="../assets/planning/pcb_raytraced.png" height="400" width="500" style="object-fit: cover;" alt="PCB routing"/> |<img src="../assets/pcb_case_unshaded.png" height="400" width="500" style="object-fit: cover;" alt="PCB components"/> |
| ---------------------------------------|------------------------------------|
| <img src="../assets/planning/pcb_routing.png" height="420" width="500" style="object-fit: cover;" alt="Case render"/> | <img src="../assets/planning/pcb_rp2040.png" height="340" width="500" style="object-fit: cover;" alt="Case side view"/> |

Features:

- 24V power input
- Build-in 5V 3A Stepdown (for RP2040 and external RPI)
- RP2040 with 128MB Flash
- 3 Port USB hub
- 1x UART connection
- 1x ARGB connection
- 2x High current 24V PWM outputs (5A)
- 4x Low current 24V PWM outputs (2A)
- [A 3D printable case](case/) with an included 30mm fan, can be mounted to a DIN rail with [this adapter](https://www.printables.com/model/259120-horizontal-ssr-din-rail-mount/files)

Why ?: I originally only wanted to slap a rpi pico onto a pcb and add 6 mosfets to it, but like you can see I got sidetracked and added my own rp2040 (my first one!), a step-down converter (also a first) and a USB hub...

It'll be used to control the fans inside the electronics enclosure and connect the 2 control boards to the one usb port of the RPI Zero 2w, which it will also power. The high current PWM outputs are for eventual LED bar upgrades, which might or might not happen.

Firmware: I'll be using Klipper on the RP2040 with [this extension module](https://github.com/julianschill/klipper-led_effect) to control the Neopixel

Schematic: [Here](../files/schematic.pdf)

Libraries:

- [easyeda2kicad](https://github.com/uPesy/easyeda2kicad.py), needs to be installed separately, used for downloading LCSC schematics & footprints
  - Run `easyeda2kicad --full --lcsc_id=<id>` to download each component (one-by-one, yes...)

## Components

LCSC IDs:

- C2040 - RP2040
- C26537 - LDO
- C778164 - 2x Button
- C113767 - SPI Flash
- C20625731 - Crystal
- C7429053 - High current mosfet
- C5364313 - Low current mosfet
- C10002 - LM2596 3A Step down - [datasheet](https://www.lcsc.com/datasheet/lcsc_datasheet_2410010301_Texas-Instruments-LM2596SX-5-0-NOPB_C10002.pdf)
  - L1: 47uH L39 - C7529419
  - Cout: 330uF/35V - C242140
  - D1: C7503125
  - Cin: 680uF/35V - C178718
- C2915639 - Screw terminal
- C2988369 - USB C Female connector
- C192893 - USB Hub chip
- C503996 - USB Female plug

Resistors & Capacitors

- 10K C5140188
- 5.1k C26023
- 1k C17513
- 27.4ohm C2079437

- 100nF C29926
- 1uF C541528
- 10uF C1713
- 15pF C5186731

## BOM

### Parts

> Note: This is my first time soldering a rp2040 (QFN-* package in general) :D

| LCSC ID   | Name                          | Amount      |
|-----------|-------------------------------|-------------|
| C2040     | RP2040                        | 1x          |
| C26537    | LDO                           | MOQ (5)     |
| C778164   | 2x Button                     | MOQ (5)     |
| C113767   | SPI Flash                     | 1x          |
| C20625731 | Crystal                       | 1x          |
| C7429053  | High current mosfet           | 2x          |
| C5364313  | Low current mosfet            | MOQ(10)     |
| C10002    | LM2596 3A Step down           | 1x          |
| C7529419  | LM2596 3A Step down (L1)      | 1x          |
| C242140   | LM2596 3A Step down (Cout)    | MOQ (5)     |
| C7503125  | LM2596 3A Step down (D1)      | MOQ (5)     |
| C178718   | LM2596 3A Step down (Cin)     | 1x          |
| C2915639  | Screw terminal                | MOQ (5)     |
| C2988369  | USB C Female connector        | MOQ (5)     |
| C192893   | USB Hub chip                  | MOQ (5)     |
| C503996   | USB Female plug               | MOQ (10)    |
| C5140188  | 10K                           | MOQ (100)   |
| C26023    | 5.1k                          | MOQ (100)   |
| C17513    | 1k                            | MOQ (100)   |
| C2079437  | 27.4ohm                       | MOQ(50)     |  
| C29926    | 100nF                         | MOQ(50)     |
| C541528   | 1uF                           | MOQ(50)     |
| C1713     | 10uF                          | MOQ(20)     |
| C5186731  | 15pF                          | MOQ(100)    |
