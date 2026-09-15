# Decompilation Baseline — Platinum

This document records the first ROM-derived structural baseline for **Platinum**.

## Target identity

- Game title field: `POKEMON PL`
- Game code: `CPUK`
- Region / language: Korea / Korean
- Header ROM version byte: `0`
- ROM size: `134217728` bytes
- SHA-256: `51050f65776f402f86b8b2b2d3b84ab5bbe80dbec75129c86f8bd9b447f11d7b`
- SHA-1: `f811d9c7ab5262f593012da794c2fa81dbcdbcc1`
- MD5: `e28b4ba15f1810ce26087a66cbb411ff`
- Verification status: **Internal identity verified; external preservation hash verification pending**

## Executable layout

- ARM9: ROM offset `0x4000`, size `1061624` bytes, RAM `0x02000000`, entry `0x02000800`
- ARM7: ROM offset `0x40A800`, size `161788` bytes, RAM `0x02380000`, entry `0x02380000`
- ARM9 overlays: `122`
- ARM7 overlays: `0`

## NitroFS / FAT

- FAT entries: `461`
- NitroFS named files: `339`
- Verified boundary: FAT entries = ARM9 overlays + NitroFS files = `122 + 339 = 461`
- Header CRC matches: `true`

### Top-level NitroFS counts

- `data`: 140
- `graphic`: 45
- `poketool`: 35
- `resource`: 32
- `fielddata`: 18
- `arc`: 14
- `application`: 12
- `battle`: 12
- `wazaeffect`: 8
- `demo`: 6
- `itemtool`: 4
- `particledata`: 4
- `msgdata`: 3
- `pokeanime`: 2
- `contest`: 1
- `debug`: 1
- `dwc`: 1
- `frontier`: 1

## Evidence status

- **Observed**: Values above were parsed directly from the supplied ROM image.
- **Reproduced**: Header CRC verification and FAT/overlay/NitroFS accounting were reproduced by `tools/nds_inventory.py`.
- **Matched**: Only targets explicitly noted as externally hash-matched should be treated as preservation-verified.

Raw ROM images are not stored in this repository.
