# Requirements

Baseline: the GitHub Universe 2026 badge (a Pimoroni Tufty 2350 derivative).
Anything not listed as changed below is carried over from that design. The
reasons for each change are in [decisions.md](decisions.md).

## Goals

- A personal, wearable badge with a colour display, touch and button input,
  motion sensing and ambient lighting.
- Long-range, off-grid messaging over LoRa (IN865 band).
- Own firmware first (Arduino-Pico), with hardware kept compatible with a
  future Meshtastic port.
- Good battery life: peripherals can be powered off completely during sleep.

## Blocks

| Block | Part | Status vs reference |
| --- | --- | --- |
| MCU | RP2350B (QFN-80, 48 GPIO) | Same |
| Flash | Winbond W25Q128JVPIQ, 16 MB QSPI | Same |
| PSRAM | APS6404L-3SQR-ZR, 8 MB, CS on GPIO8 | Same |
| Wi-Fi / Bluetooth | RM2 module (CYW43439) | Same; its spare GPIOs reassigned |
| LoRa | SX1262 module, IN865 (865–867 MHz), u.FL antenna connector | **New** |
| GPS | Small GNSS module on UART0 (candidate: u-blox MIA-M10Q) | **New** |
| Display | 320×240 LCD, 8-bit parallel, AP2502 backlight | Same (to be reviewed) |
| Capacitive touch | CAP1208, 8 pads | Same |
| IMU | LSM6DS3TR-C | Same |
| Ambient light | PT19-21C phototransistor | Same; moved to GPIO40 |
| IR transmit / receive | — | **Removed** |
| Case lighting | 4 × WS2812B-style addressable RGB LEDs, one data pin | **Changed** (was 4 white LEDs on 4 GPIOs) |
| Buttons | 5 physical (Up, Down, A, B, C) with diode-combined wake interrupt | Same |
| BOOT button | Bootloader on QSPI_CS, also read on GPIO22 | Same |
| RESET button | 74LVC1G57 pulse circuit to RUN, also read on GPIO14 | Same |
| Battery monitoring | MAX17048 I2C fuel gauge | **Changed** (was a resistor divider into the ADC) |
| Charger | MCP73831/2, about 455 mA | Same (charge current to be reviewed) |
| Battery protection | XB6096I2S | Same |
| 3.3 V rail | RT9080-33GJ5 LDO, always on | Same |
| Switched 3.3 V (3V3_SW) | AP22802AW5 load switch, enabled by GPIO2 | Same; enable moved to GPIO2 |
| USB | USB-C, VBUS detect on GPIO1 | Same; detect moved to GPIO1 |
| Expansion | Qw/ST I2C connector (GPIO4/5) | Same |
| Debug | 3-pin SWD header | Same |

## Electrical requirements

- All RP2350 I/O is 3.3 V. No GPIO may see 5 V.
- Peripherals that can be shut down for sleep (sensors, touch, LEDs, LoRa,
  Qw/ST) are powered from 3V3_SW.
- The GPS keeps its backup supply (V_BCKP) powered so it can hot-start after
  sleep.
- Peak current must stay within the 3.3 V LDO's rating (600 mA). This needs a
  power budget: LoRa transmit at +22 dBm is about 120 mA, and the four RGB LEDs
  at full white are about 240 mA. Firmware will cap LED brightness.
- RF: three antennas on one small board (LoRa, GNSS, RM2). Keep them apart,
  and keep the LoRa antenna away from USB-C and the touch pads.

## Firmware requirements

- **Primary:** Arduino-Pico (earlephilhower core) with RadioLib for LoRa and
  LoRaWAN (IN865).
- **Future:** a Meshtastic variant. The Meshtastic RP2350 port also uses
  Arduino-Pico and RadioLib. Hardware choices that keep this possible:
  - SX1262 with antenna switch on DIO2 and a TCXO powered from DIO3
  - MAX17048 fuel gauge (Meshtastic has a driver)
  - GPS on a hardware UART
  - LSM6DS3-family IMU (Meshtastic has a driver)
- Known Meshtastic gaps on RP2350 (firmware only, no board impact): no
  Bluetooth, limited Wi-Fi, no driver for the parallel LCD.

## Still to define

See the open items in [decisions.md](decisions.md#open-items).
