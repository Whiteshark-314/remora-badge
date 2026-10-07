# Part candidates

Parts carried over from the reference design are listed in
[requirements.md](requirements.md). This file tracks new or changed parts.

| Function | Candidate | Package | Status | To check |
| --- | --- | --- | --- | --- |
| Fuel gauge | Analog Devices MAX17048 | 2 × 2 mm DFN-8 / WLP | Chosen | Stock; I2C behaviour with bus pull-ups unpowered |
| LoRa | SX1262 module, e.g. Seeed Wio-SX1262 or Heltec HT-RA62 | Module | Candidates | 865 MHz coverage, antenna switch on DIO2, TCXO, stock, price |
| GPS | u-blox MIA-M10Q | 4.5 × 4.5 mm LGA SiP | Preferred | Stock, price, antenna design, assembly |
| GPS (fallback) | Quectel L76K | 10.1 × 9.7 mm | Fallback | Stock |
| RGB LEDs | WS2812B-compatible, 3.3 V-rated | TBD | Open | Minimum supply voltage and data-high threshold at 3.3 V |
| LoRa antenna connector | u.FL (IPEX MHF1) | SMD | Chosen | Footprint |
| GPS antenna | Ceramic GNSS chip antenna + u.FL footprint | SMD | Chosen | Part, keep-out area, matching |
| Charger | SG Micro SGM41511 or TI BQ25601 | QFN-24 4 × 4 mm | Chosen | Stock; inductor; input-current detection |
| 3.3 V regulator | TI TPS63802 buck-boost | 2 × 3 mm QFN | Preferred | Stock; peak current at 3.0 V input; inductor |
| Battery | 1-cell LiPo, 2500 mAh, ≤ 50 × 40 × 10 mm, 10k NTC, 3-pin | — | Chosen | Supplier; connector (e.g. JST PH 3-pin); pinout |
| Battery protection | XB6096I2S (from reference) | — | To check | Over-current trip vs 1C |
