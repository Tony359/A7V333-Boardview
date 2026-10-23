# ASUS A7V333 (PCB R1.01A): boot path schematics

These are hand-traced schematics of the boot path of the ASUS A7V333 Socket A motherboard, PCB revision 1.01A. They cover everything the board needs to get from power-on to its first POST code.

**[Open the schematics](https://tony359.github.io/A7V333-Boardview/)**, or download `index.html` and open it in any browser.

This is an **unofficial reconstruction** traced from the board view. It is not an ASUS document, and I'm not affiliated with ASUS. It may contain errors, so check against your own board before relying on it.

## What's in it

There are four sheets, with a search box to find parts, test pads and nets:

1. **Power-good and reset:** from the PSU power-good to the southbridge, the CPU PWROK and the PCI and CPU resets
2. **Clocks:** the ICS94228 clock generator, the CPU clock and the BIOS clock
3. **LPC bus and BIOS:** the southbridge, the BIOS chip (SST 49LF020), the Super I/O and the other parts on the LPC bus
4. **CPU control pins:** the Socket A control, start-up and reference pins

## A tip from my repair

My board powered on but showed no POST code at all, and the BIOS chip was never accessed. The CPU, the VRM, the clocks, reset and the BIOS chip all checked out.

The fault was the **USB_EN** jumper, which had its cap on one pin only. That jumper connects the reset of the VIA VT6202 USB 2.0 chip:

- **Pins 1-2:** normal PCI reset (USB 2.0 enabled)
- **Pins 2-3:** reset held to ground (USB 2.0 disabled)
- **No jumper:** the USB chip's reset input floats. The chip can then wake up in a random state and jam the shared PCI bus, and the whole board stops before the first POST code.

If your A7V333 is dead with no POST code, check that USB_EN is on 1-2 or 2-3.

## Licence

The schematics are licensed under [CC BY-SA 4.0](LICENSE). You can share and adapt them, as long as you give credit and share your changes under the same licence.
