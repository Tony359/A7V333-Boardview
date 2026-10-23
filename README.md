# ASUS A7V333 (PCB R1.01A): board view and boot path schematics

An interactive board view of the ASUS A7V333 Socket A motherboard, PCB revision 1.01A, plus hand-traced schematics of its boot path.

- **[Open the board view](https://tony359.github.io/A7V333-Boardview/):** every part with its value, and every pin with its net. Click a part to see what it is, or click a pin to highlight everything on the same net. It shows the top and bottom of the board, and you can search for a part, net or value.
- **[Open the boot path schematics](https://tony359.github.io/A7V333-Boardview/schematics.html):** four sheets covering everything the board needs to get from power-on to its first POST code.

You can also download `index.html` or `schematics.html` and open them in any browser. Each one is a single file that works offline.

This is an **unofficial** reconstruction from the board's factory data. It is not an ASUS document, and I'm not affiliated with ASUS. It may contain errors, so check against your own board before relying on it.

## The board view

The data is from build 60-M7A50G-A0, the version without RAID and FireWire. Parts that aren't fitted on that build show as empty footprints, so your board may have parts there if it's a different build. The parts list covers surface-mount parts only, so through-hole parts such as electrolytic capacitors, connectors and crystals have no value listed.

## The schematics

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

My own work here, the viewer pages and the traced schematics, is licensed under [CC BY-SA 4.0](LICENSE). You can share and adapt it, as long as you give credit and share your changes under the same licence. The underlying board data comes from ASUS.
