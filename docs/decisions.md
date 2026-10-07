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
| D-024 | 2026-10-07 | Sourcing from any online distributor (Mouser, DigiKey, LCSC); local assembly allowed | JLCPCB stock is not a constraint |
| D-025 | 2026-10-07 | Board size within the GitHub Universe 2026 / Tufty 2350 envelope (84 × 76 × 20 mm in case) | User's choice; battery mounts on the back |
| D-026 | 2026-10-07 | Proposed: charger BQ25601D instead of SGM41511 | SGM41511 is LCSC-only; the D variant adds USB charger-type detection |
| D-027 | 2026-10-07 | Proposed: Wio-SX1262 module, with RF_SW driven by DIO2 through a 74LVC1G04 inverter | Best stocked; the inverter avoids needing a GPIO (none left) |
| D-028 | 2026-10-07 | Proposed: SK6812MINI-E LEDs powered from the charger SYS rail through a load switch on SW_POWER_EN; firmware turns them off below about 3.7 V | No true 3.3 V addressable LED found; 3.3 V data still meets 0.7 × VDD |

## Open items

- [x] **CHARGE_STAT:** LED only (D-019).
- [x] **GPIO12:** MAX17048 `ALRT` (D-019).
- [x] **GPS antenna:** chip antenna plus u.FL footprint (D-018).
- [x] **GPS module:** MIA-M10Q-00B in stock at Mouser (parts.md). Confirm the
      local assembler can place its 4.5 mm LGA.
- [ ] **LoRa module:** Wio-SX1262 proposed (D-027). Its tuning is 868–960 MHz,
      just above IN865; decide whether that is acceptable or look for a
      module tuned for 865 MHz.
- [x] **RGB LEDs:** SK6812MINI-E proposed (D-028).
- [ ] **Confirm proposals:** D-026, D-027 and D-028 need the user's go-ahead.
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
- [ ] **Charger:** USB-C input current. The BQ25601D detects BC1.2 adapters;
      decide whether USB-C CC current advertisement (1.5 A / 3 A) also needs
      detecting.
- [ ] **Board:** exact PCB outline (within D-025), layer count, case.
- [ ] **Battery:** source a 104050-size 2500 mAh LiPo with 10k NTC and a
      JST PH 3-pin plug; check its wire order.
- [x] **Licence:** decided (D-015).
- [x] **Remote:** public at https://github.com/Whiteshark-314/remora-badge
