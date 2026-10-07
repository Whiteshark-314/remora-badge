# Remora Badge

A custom RP2350B electronic badge, derived from Pimoroni's Tufty 2350 and the
GitHub Universe 2026 badge. It keeps the colour LCD, Wi-Fi/Bluetooth module,
IMU and capacitive touch from that design, and adds LoRa (SX1262, IN865), GPS,
an I2C battery fuel gauge and addressable RGB case lighting.

Longer term, the board is meant to be able to run
[Meshtastic](https://meshtastic.org/) as well as its own firmware.

## Status

Phase 1: project setup and requirements. No schematic yet.

## Repository layout

| Path | Contents |
| --- | --- |
| [`docs/`](docs/) | Requirements, pin map, decision log and part candidates |
| [`hardware/`](hardware/) | KiCad project and project-specific libraries |
| [`firmware/`](firmware/) | Arduino-Pico firmware, starting with a bring-up sketch |
| [`reference/`](reference/) | Third-party reference designs (not tracked; see its README) |

## Key documents

- [Requirements](docs/requirements.md): what the board must do, block by block
- [Pin map](docs/pinmap.md): RP2350B GPIO and RM2 GPIO assignments
- [Decision log](docs/decisions.md): what changed from the reference design and why
- [Part candidates](docs/parts.md): chosen and candidate parts, with checks still to do

## Plan

1. **Setup:** folders, documentation, git repository
2. **Schematic:** KiCad, sheet by sheet, starting from the reference blocks
3. **PCB layout:** outline, placement, routing, DRC, 3D check
4. **Fabrication:** Gerbers, BOM and placement files for JLCPCB assembly
5. **Firmware:** Arduino-Pico bring-up, then application firmware; Meshtastic variant later

## Licence

| Content | Licence |
| --- | --- |
| Hardware (`hardware/`) | [CERN-OHL-P v2](hardware/LICENSE) (permissive open hardware) |
| Firmware (`firmware/`) | [MIT](firmware/LICENSE) |
| Documentation | [CC BY 4.0](docs/LICENSE) |

## Credits

The core circuit is derived from the GitHub Universe 2026 badge by Pimoroni and
GitHub (MIT License), which is itself based on the
[Tufty 2350](https://shop.pimoroni.com/products/tufty-2350). See [NOTICE](NOTICE).
This project is not affiliated with or endorsed by Pimoroni or GitHub.
