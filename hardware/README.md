# Hardware

The KiCad project for the Remora badge goes here.

Planned layout:

| Path | Contents |
| --- | --- |
| `remora-badge.kicad_pro` | KiCad project (created in Phase 2) |
| `lib/symbols/` | Project-specific symbols |
| `lib/footprints/` | Project-specific footprints (`.pretty`) |
| `lib/3dmodels/` | STEP models |
| `fab/` | Gerbers, BOM and placement files for each release |

Libraries are project-local, so the design opens the same way on any machine.

Licence: [CERN-OHL-P v2](LICENSE). Put `SPDX-License-Identifier: CERN-OHL-P-2.0`
and the copyright line in each schematic and PCB title block.
