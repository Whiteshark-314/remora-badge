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
