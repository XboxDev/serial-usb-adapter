# Original Xbox Serial USB Adapter

This device allows for serial communication with an original Xbox and is primarily used for kernel debugging.

For questions or support, contact xbox7887 in the [XboxDev on Discord](https://discord.gg/WxJPPyz).

![Xbox Serial USB Adapter Image, REV A](images/adapter.png?raw=true "Xbox Serial USB Adapter, REV A")

## Requirements

### Hardware

Any original Xbox of any version (although versions 1.3-1.5 require LFRAME# reconnect and version 1.6 requires full LPC port rebuild, including LFRAME#).
Debug and development kits will work without modification, however, retail boxes need to use a hacked kernel (X2 5035 or iND 5004 for example) that initializes superio as well as have a 2x8 2.54mm pin header soldered to the LPC port.

### Software

A Windows OS capable of running WinDbg; versions 4.0.0018.0 (XDK) or [6.12.0002.633](http://download.microsoft.com/download/A/6/A/A6AC035D-DA3F-4F0C-ADA4-37C8E5D34E3D/setup/WinSDKDebuggingTools/dbg_x86.msi) have been tested successfully.

Optionally, [KiCad 7.0](http://kicad-pcb.org/download/) if you need to work with the PCB project files.

## Usage

Connect a USB-C cable from your PC to the serial adapter, then the IDC cable ends into the serial adapter and Xbox LPC port pin headers respectively, ensuring the correct alignment and orientation as shown in the image above. **Incorrect orientation may result in damage to the adapter and/or your Xbox, you have been warned!**

Within WinDbg press `CTRL+K` to bring up the connection dialog and enter `115200` for the baud rate along with the `COM#` port as detected by your computer in device manager.

![WinDbg Connection Image](images/windbg-connect.png?raw=true "WinDbg Connection")

`CTRL+Break` can be used to pause execution, `F5` to continue, and `F10/F11` to step over or through instructions.
`CTRL+ALT+D` will toggle verbose windbg protocol output for troubleshooting if needed.
The adapter's blue RX LED indicates signals sent from the PC and the green TX LED from the Xbox. 

![WinDbg Runtime Image](images/windbg-runtime.png?raw=true "WinDbg Runtime")

## Components

Bold designators are the bare minimum required for basic functionality but stability may be questionable. The entire UART to USB circuit and/or LED output is optional and can be replaced with an external 3.3V UART to USB cable jumpered to J2 instead.

| Count | Part/Value | Description | Designators | Notes |
| - | - | - | - | - |
| 1  | 2x8 2.54mm | Pin Header | **JP1** | |
| 1  | Stewart SS-52400-003 | USB-C Connector  | **J1** | |
| 1  | 1x3 2.54mm | Pin Header | J2 | Optional UART breakout |
| 1  | SG5032CAN | 14.318MHz 5032 Crystal Oscillator | **Y1** | |
| 1  | LPC47M192 | SuperIO | **U1** | The LPC47M157 is also compatible |
| 1  | FT231XS | UART to USB | **U2** | |
| 2  | 27R | 0603 SMD Resistor | **R1**, **R3** | Filtering |
| 2  | 10k | 0603 SMD Resistor | **R2**, **R4** | Configuration pull-ups/downs |
| 1  | 470R | 0603 SMD Resistor | R5 | LED power dissipation |
| 1  | 1.2k | 0603 SMD Resistor | R6 | LED power dissipation  |
| 2  | 5.1k | 0603 SMD Resistor | **R7**, **R8** | USB-C Configuration pull-downs |
| 2  | 100R | 4x0603 SMD Resistor Network | **RN1**, **RN2** | Terminating resistors for longer LPC ribbons (10+ inches) |
| 1  | 33 Ohm | 0603 Ferrite Bead | **FB1** | Filtering, can be substituted with a 0 ohm resistor or solder bridge |
| 3  | 47pF | 0603 SMD Capacitor | C6, C7 | Filtering |
| 6  | 10nF | 0603 SMD Capacitor | C3, **C8**, C9, **C10**, C12, C13 | Decoupling |
| 2  | 100nF | 0603 SMD Capacitor | C2, C11 | Decoupling |
| 1  | 4.7uF | 0603 SMD Capacitor | C1 | Bulk |
| 1  | 10uF | 0603 SMD Capacitor | C5 | Bulk |
| 1  | Green | 0603 SMD LED | D1 | |
| 1  | Blue | 0603 SMD LED | D2 | |

### External Components

| Count | Part/Value | Description | Designators | Notes |
| - | - | - | - | - |
| 1 | 2x8 2.54mm | Pin Header | N/A | Retail Xbox LPC Connector |
| 1 | 16 Wire 2.54mm | Female to Female IDC Ribbon Cable | N/A | Keep length under 18 inches for best results |
| 1 | USB-C Cable | Cable | N/A | |

### Component Retailers

* [Mouser](https://www.mouser.com/)
* [Digi-Key](https://www.digikey.com/)
* [Arrow](https://www.arrow.com/)
* [Utsource](https://www.utsource.net/)
* [AliExpress](https://www.aliexpress.com/)
* [JLCPCB](https://jlcpcb.com/)

## Reference

![Schematic Image](images/schematic.png?raw=true "Schematic Runtime")

![PCB Copper Image](images/pcb-copper.png?raw=true "PCB Copper Runtime")

![PCB Top Image](images/pcb-top.png?raw=true "PCB Top Runtime")

![PCB Bottom Image](images/pcb-bottom.png?raw=true "PCB Bottom Runtime")

![PCB Render](images/pcb-render.png?raw=true "PCB Render")

![Assembled PCBs](images/assembled.jpg?raw=true "Assembled PCBs")

## Copyright

Copyright Mike Davis 2019.

This documentation describes Open Hardware and is licensed under the
CERN OHL v. 1.2 or later.

You may redistribute and modify this documentation under the terms of the
CERN OHL v.1.2 or later. (http://ohwr.org/cernohl). This documentation is distributed
WITHOUT ANY EXPRESS OR IMPLIED WARRANTY, INCLUDING OF
MERCHANTABILITY, SATISFACTORY QUALITY AND FITNESS FOR A
PARTICULAR PURPOSE. Please see the CERN OHL v.1.2 or later for applicable
conditions
