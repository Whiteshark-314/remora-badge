# Project status

Last updated: 2026-10-07. Read this first when picking the project up again.

## Where things stand

| Phase | State |
| --- | --- |
| 1. Setup: folders, docs, git, licences, GitHub | **Done** |
| 2. Schematic | **Not started.** Requirements, pin map and most parts are decided |
| 3. PCB layout | Not started |
| 4. Fabrication | Not started |
| 5. Firmware | Not started (Arduino-Pico + RadioLib chosen) |

## What has been decided

- **Design basis:** GitHub Universe 2026 badge (a Pimoroni Tufty 2350
  derivative); reference clone in `reference/badger-home`.
- **Blocks:** see [requirements.md](requirements.md).
- **All 48 GPIOs are assigned:** see [pinmap.md](pinmap.md). Only the RM2's
  GPIO0–2 are spare.
- **Every decision and its reason:** see [decisions.md](decisions.md)
  (D-001 to D-028).
- **Parts with MPNs, prices and stock:** see [parts.md](parts.md).

## Summary of changes from the reference

- Removed: IR transmitter and receiver.
- Added: SX1262 LoRa module (IN865), u-blox MIA-M10Q GPS with chip antenna
  and u.FL option, MAX17048 fuel gauge.
- Changed: 4 white case LEDs → 4 SK6812-style RGB LEDs on one pin;
  MCP73831 → BQ25601D switching charger with power path and NTC;
  RT9080 LDO → TPS63802 buck-boost; 1000 mAh → 2500 mAh battery (1C max).
- Kept: RP2350B, flash, PSRAM, RM2, 320×240 parallel LCD, CAP1208 touch,
  LSM6DS3TR-C IMU, light sensor, 5 buttons, BOOT and RESET buttons (both
  readable on GPIOs), 3V3_SW load switch, Qw/ST, SWD.
- Future: Meshtastic compatibility (RP2350 port uses Arduino-Pico + RadioLib;
  no Bluetooth there yet, display would need its own driver).

## Next steps

1. Confirm the proposed parts (D-026 to D-028) and the LoRa module's 868 MHz
   tuning vs IN865.
2. Datasheet checks:
   - RP2350B pin 53 (GPIO42, used for LORA_NRESET; tied to 1V1 in the
     reference)
   - XB6096I2S over-current trip vs the 1C (2.5 A) limit
   - MAX17048 behaviour with the internal I2C pull-ups unpowered in sleep
   - BQ25601D USB input-current detection vs USB-C CC advertisement
3. Power budget at a 3.0 V cell (LoRa TX, RM2, backlight, LEDs, GPS).
4. Board outline within 84 × 76 mm; layer count; case.
5. Start the KiCad schematic in `hardware/`, sheet by sheet.

All remaining open items are listed at the end of [decisions.md](decisions.md).

## Working notes

- Project folder: `D:\Documents\Personal Projects\remora-badge` (Windows).
- GitHub: https://github.com/Whiteshark-314/remora-badge (public). The GitHub
  CLI is installed and signed in as Whiteshark-314.
- Commits carry a `Co-Authored-By: Claude` trailer by choice.
