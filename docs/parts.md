# Part candidates

Parts carried over from the reference design are listed in
[requirements.md](requirements.md). This file tracks new or changed parts.
Sourcing: any online distributor (Mouser, DigiKey, LCSC); assembly may be
local, so JLCPCB stock is not required. Prices are single-unit, checked
2026-10-07.

| Function | Part (MPN) | Package | Price / stock | Status | Notes and checks |
| --- | --- | --- | --- | --- | --- |
| Fuel gauge | Analog Devices MAX17048G+T10 | 2 × 2 mm TDFN-8 | Mouser $4.45 (19k), DigiKey $4.61 (24k) | Proposed | Check behaviour with internal I2C pull-ups unpowered |
| Charger | TI BQ25601DRTWR | 4 × 4 mm WQFN-24 | DigiKey $3.45 (9.7k), Mouser $3.39 (773) | Proposed | "D" variant adds USB charger-type detection (BC1.2) on D+/D-, shared with the RP2350 USB lines. SGM41511 is LCSC-only |
| 3.3 V regulator | TI TPS63802DLAR | 2 × 3 mm VSON-10 | DigiKey $3.40 (19.5k) | Proposed | 2 A buck-boost, 1.3–5.5 V in |
| LoRa | Seeed Wio-SX1262 (bulk, 114993390) | SMD module with IPEX | DigiKey $5.95 (2.2k) | Proposed | TCXO on DIO3; antenna switch needs DIO2 **and** RF_SW (inverse of DIO2): drive RF_SW from DIO2 through an inverter (74LVC1G04), no GPIO. Tuned for 868–960 MHz; IN865 (865–867) is just below, so expect a small loss |
| GPS | u-blox MIA-M10Q-00B | 4.5 × 4.5 mm LGA | Mouser $9.31 (31.8k); DigiKey out of stock | Proposed | Fine-pitch LGA: check the local assembler can place it |
| GPS antenna | Johanson 1575AT43A0040001E chip antenna | 1206-size chip | DigiKey $0.94 (26k) | Proposed | Plus u.FL footprint and 0 Ω selector; needs ground clearance per datasheet |
| RGB LEDs | Opsco SK6812MINI-E (reverse mount) | 3.2 × 2.8 mm | LCSC (140k) | Proposed | Rated 3.7–5.5 V, so no true 3.3 V part found. Power from the charger's SYS rail through a load switch on SW_POWER_EN; 3.3 V data is above 0.7 × VDD while SYS ≤ 4.7 V; firmware turns LEDs off below about 3.7 V battery |
| Battery connector | JST S3B-PH-SM4-TB(LF)(SN), 3-pin PH, SMD right-angle | — | Mouser/DigiKey $0.57 (35k+) | Proposed | No standard polarity for 3-pin LiPo packs: check the battery's pinout |
| Battery | 1-cell LiPo, about 2500 mAh, ≤ 50 × 40 × 10 mm (e.g. 104050 size), 10k NTC, 3-wire | — | — | To source | |
| LoRa antenna connector | On the Wio-SX1262 module (IPEX) | — | — | Proposed | |
| Battery protection | XB6096I2S (from reference) | — | — | To check | Over-current trip vs 1C |
