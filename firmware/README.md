# Firmware

Arduino-Pico (earlephilhower core) firmware for the Remora badge.

Planned:

| Path | Contents |
| --- | --- |
| `bringup/` | Hardware test sketch: exercises each peripheral and does a LoRaWAN join on IN865 |
| `remora/` | Application firmware |

Libraries: RadioLib (SX1262, LoRaWAN), Adafruit NeoPixel (case LEDs), plus
drivers for the CAP1208, LSM6DS3TR-C, MAX17048 and GPS.

Pin assignments: see [../docs/pinmap.md](../docs/pinmap.md).

A Meshtastic variant may be added later; the hardware is kept compatible (see
[../docs/requirements.md](../docs/requirements.md)).
