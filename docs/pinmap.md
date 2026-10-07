# Pin map

RP2350B (QFN-80), 48 GPIOs. "Ref" is the GitHub Universe 2026 badge
assignment, for comparison.

## RP2350B GPIO

| GPIO | Function | Net | Ref | Notes |
| ---: | --- | --- | --- | --- |
| 0 | PIO | `LED_DATA` | `CL0` | WS2812-style data, 4 LEDs chained |
| 1 | In | `VBUS_DETECT` | `CL1` | USB present, 5.1k/5.1k divider. Can wake from sleep |
| 2 | Out | `SW_POWER_EN` | `CL2` | Enables the 3V3_SW load switch |
| 3 | In | `CHG_INT` | `CL3` | SGM41511 charger interrupt (open drain, active low) |
| 4 | I2C0 SDA | `I2C_QWST_SDA` | same | Qw/ST connector |
| 5 | I2C0 SCL | `I2C_QWST_SCL` | same | Qw/ST connector |
| 6 | In | `SW_DOWN` | same | |
| 7 | In | `SW_A` | same | |
| 8 | QMI CS1 | `PSRAM_CS` | same | |
| 9 | In | `SW_B` | same | |
| 10 | In | `SW_C` | same | |
| 11 | In | `SW_UP` | same | |
| 12 | In | `FG_ALRT` | `VBUS_DETECT` | MAX17048 low-battery alert (open drain, active low) |
| 13 | In | `CAP_ALERT` | same | CAP1208 interrupt |
| 14 | In | `RESET_SW` | same | Reset button still held after boot |
| 15 | In | `SWITCH_INT` | same | Diode-combined button wake |
| 16 | UART0 TX | `GPS_RXD` | `IR_TX` | MCU TX to GPS RX |
| 17 | UART0 RX | `GPS_TXD` | `IR_RX` | GPS TX to MCU RX |
| 18 | I2C1 SDA | `I2C_INT_SDA` | same | Internal bus |
| 19 | I2C1 SCL | `I2C_INT_SCL` | same | Internal bus |
| 20 | In | `IMU_INT` | same | LSM6DS3TR-C INT1 |
| 21 | In | `LCD_VSYNC` | same | LCD tearing effect |
| 22 | In | `USER_SW` | same | BOOT button (also on QSPI_CS) |
| 23 | Out | `WL_ON` | same | RM2 |
| 24 | PIO | `WL_D` | same | RM2 |
| 25 | PIO | `WL_CS` | same | RM2 |
| 26 | Out | `LCD_BACKLIGHT` | same | |
| 27 | PIO | `LCD_CS` | same | |
| 28 | PIO | `LCD_RS` | same | |
| 29 | PIO | `WL_CLK` | same | RM2 |
| 30 | PIO | `LCD_WR` | same | |
| 31 | PIO | `LCD_RD` | same | |
| 32–39 | PIO | `LCD_DB0`–`LCD_DB7` | same | 8-bit parallel data |
| 40 | ADC0 | `LIGHT_SENSE` | `VBAT_SENSE` | Phototransistor; must be an ADC pin |
| 41 | In | `LORA_BUSY` | `SW_POWER_EN` | |
| 42 | Out | `LORA_NRESET` | tied to 1V1 | Check RP2350B pin 53 in the datasheet |
| 43 | In | `LORA_DIO1` | `LIGHT_SENSE` | LoRa interrupt |
| 44 | SPI1 RX | `LORA_MISO` | NC | |
| 45 | SPI1 CSn | `LORA_NSS` | NC | |
| 46 | SPI1 SCK | `LORA_SCK` | NC | |
| 47 | SPI1 TX | `LORA_MOSI` | NC | |

**Spare:** none. All 48 GPIOs are assigned; spare signals left are on the RM2 (below).

PIO note: the RP2350's PIO blocks each address 32 consecutive GPIOs. The LCD
(GPIO27–39) and the WS2812 data (GPIO0) need different PIO blocks; there are
three, so this is fine.

## RM2 (CYW43439) GPIO

Only readable after the wireless chip has been started (about 1 s after
boot), and cannot wake the MCU.

| RM2 GPIO | Use | Ref |
| --- | --- | --- |
| GPIO0 | *spare* | NC |
| GPIO1 | *spare* | NC |
| GPIO2 | *spare* (charge status now drives an LED and is readable over I2C) | `CHARGE_STAT` |

## I2C devices

| Bus | Address | Device |
| --- | ---: | --- |
| Internal (GPIO18/19) | 0x28 | CAP1208 touch |
| Internal (GPIO18/19) | 0x36 | MAX17048 fuel gauge |
| Internal (GPIO18/19) | 0x6A | LSM6DS3TR-C IMU |
| Internal (GPIO18/19) | 0x6B | SGM41511 charger |
| Qw/ST (GPIO4/5) | — | User add-ons |

## Dedicated pins (unchanged from reference)

QSPI (flash and PSRAM), USB D+/D-, SWDIO/SWCLK, RUN, XIN/XOUT, and the
on-chip regulator pins.
