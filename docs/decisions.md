# Decision log

Changes from the GitHub Universe 2026 badge, with the reasoning. Newest last.

| # | Date | Decision | Reason |
| --- | --- | --- | --- |
| D-001 | 2026-10-07 | Base the design on the Universe 2026 badge / Tufty 2350 schematic | Proven RP2350B design; most firmware and pin assignments can be reused |
| D-002 | 2026-10-07 | Remove the IR receiver and IR transmitter | Frees GPIO16/17; IR not needed |
| D-003 | 2026-10-07 | Add an SX1262 LoRa **module**, IN865 band, u.FL antenna connector | Long-range messaging. A module avoids RF matching and TCXO design |
| D-004 | 2026-10-07 | LoRa on GPIO41–47, with SPI on hardware SPI1 (GPIO44–47) | Keeps the radio pins together and on a hardware SPI peripheral |
| D-005 | 2026-10-07 | Firmware: Arduino-Pico + RadioLib first | Fastest route to working hardware; RadioLib supports LoRaWAN IN865 |
| D-006 | 2026-10-07 | Replace the VBAT resistor divider with a MAX17048 I2C fuel gauge | Reports state of charge directly; Meshtastic has a driver. Chosen over the BQ27441 for that reason and because it needs no sense resistor |
| D-007 | 2026-10-07 | Keep the CAP1208 capacitive touch | Wanted as a learning exercise |
| D-008 | 2026-10-07 | Replace the 4 white case LEDs with 4 WS2812B-style RGB LEDs on GPIO0 | Ambient lighting in colour, and frees 3 GPIOs |
| D-009 | 2026-10-07 | Keep the BOOT and RESET buttons, and their GPIO sense lines (GPIO22, GPIO14) | Both readable in firmware for experiments |
| D-010 | 2026-10-07 | Keep SW_POWER_EN and the 3V3_SW load switch; move enable to GPIO2 | Peripherals can be powered off fully during sleep |
| D-011 | 2026-10-07 | Move VBUS_DETECT to GPIO1 (MCU, not RM2) | USB plug-in can wake the badge |
| D-012 | 2026-10-07 | Move LIGHT_SENSE to GPIO40 | Needs an ADC pin; GPIO40–47 are the only ones |
| D-013 | 2026-10-07 | Add a GPS module on UART0 (GPIO16 TX, GPIO17 RX), smallest available | Position for Meshtastic and own apps. Candidate: u-blox MIA-M10Q (4.5 × 4.5 mm) |
| D-014 | 2026-10-07 | Keep the hardware Meshtastic-compatible | Future option; see requirements.md |
| D-015 | 2026-10-07 | Licences: hardware CERN-OHL-P v2, firmware MIT, docs CC BY 4.0; credit Pimoroni & GitHub in NOTICE | Hobby project, anyone may reuse it. The reference is MIT, which permits this as long as its notice is kept |
| D-016 | 2026-10-07 | No Tufty, GitHub or Pimoroni names or logos on the board or in the product name | Those are trademarks; the MIT licence covers copyright only |
| D-017 | 2026-10-07 | Keep the 320×240 8-bit parallel LCD | Proven, and the existing Pimoroni driver fits our pins |
| D-018 | 2026-10-07 | GPS antenna: ceramic chip antenna plus a u.FL footprint, chosen with a 0 Ω resistor | Compare both on the first boards |
| D-019 | 2026-10-07 | Charger STAT drives a charge LED only; MAX17048 ALRT on GPIO12 | LED works with the MCU off; fuel gauge reports charge state; alert can wake the MCU |
| D-020 | 2026-10-07 | Battery: 2500 mAh, up to 50 × 40 × 10 mm, max 1C charge and discharge, 3-wire with 10k NTC | Longer runtime with LoRa and GPS; NTC for safe charging above 1 A |
| D-021 | 2026-10-07 | Replace the MCP73831 with an SGM41511 / BQ25601 switching charger (I2C 0x6B, power path) | A linear 500 mA charger would take about 6 h and run hot at higher current |
| D-022 | 2026-10-07 | Charger INT on GPIO3; VBUS_DETECT stays on GPIO1 | Both signals on their own pins (uses the last spare GPIO) |
| D-023 | 2026-10-07 | Replace the RT9080 LDO with a buck-boost regulator (e.g. TPS63802) | Uses the battery down to 3.0 V instead of about 3.6 V |

## Open items

- [x] **CHARGE_STAT:** LED only (D-019).
- [x] **GPIO12:** MAX17048 `ALRT` (D-019).
- [x] **GPS antenna:** chip antenna plus u.FL footprint (D-018).
- [ ] **GPS module:** confirm MIA-M10Q stock and price; fallback is the Quectel L76K.
- [ ] **LoRa module:** choose one covering 865 MHz with the antenna switch on
      DIO2 and a TCXO; confirm stock.
- [ ] **RGB LEDs:** choose a WS2812-compatible part rated for 3.3 V supply and
      3.3 V data.
- [ ] **RP2350B pin 53 (GPIO42):** the reference ties it to 1V1. Check the
      datasheet before using it for LORA_NRESET.
- [ ] **Internal I2C pull-ups:** they are on 3V3_SW, but the MAX17048 runs from
      the battery. Check its behaviour with the bus unpowered during sleep.
- [ ] **Power budget:** confirm the buck-boost regulator covers LoRa TX, the
      RM2, the backlight and the LEDs at a 3.0 V cell.
- [x] **Display:** same LCD (D-017).
- [x] **Battery:** 2500 mAh, 1C max, NTC (D-020).
- [ ] **Battery protection:** check the XB6096I2S trip current suits a 1C
      (2.5 A) limit, or choose another protector.
- [ ] **Charger:** SGM41511 vs BQ25601 stock; USB-C input current (what the
      charger can detect from the source).
- [ ] **Board:** outline and size, layer count, assembly (full JLCPCB or partly
      by hand).
- [x] **Licence:** decided (D-015).
- [x] **Remote:** public at https://github.com/Whiteshark-314/remora-badge
