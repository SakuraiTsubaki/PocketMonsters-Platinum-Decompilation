# Analysis: complete Nintendo DS ROM structure inventory

## Target and applicability

This analysis applies only to the selected `CPUK` input with SHA-256
`51050f65776f402f86b8b2b2d3b84ab5bbe80dbec75129c86f8bd9b447f11d7b`. ROM bytes and extracted payloads are not
included.

## Claim

The standard Nintendo DS header, ARM9/ARM7 regions, FNT, FAT, NitroFS namespace,
overlay tables, banner, header-referenced regions, physical gaps, and trailing
padding have been inventoried without omitting any table entry. Every FAT file
has an offset, size, and SHA-256 in the generated results.

## Evidence

| Item | Confirmed value |
| --- | --- |
| Actual / used ROM size | `134217728` / `102630460` bytes |
| ARM9 ROM offset / RAM / entry / size | `0x4000` / `0x02000000` / `0x02000800` / `1061624` |
| ARM7 ROM offset / RAM / entry / size | `0x40a800` / `0x02380000` / `0x02380000` / `161788` |
| FNT / FAT offset and size | `0x432000` / `7427`; `0x433e00` / `3688` |
| Directories / FAT files / FNT-mapped files | `105` / `461` / `339` |
| ARM9 / ARM7 overlays | `122` / `0` |
| Banner offset / version | `0x434e00` / `3` |
| NARC / recognized leading signatures | `215` / `283` |
| Unreferenced and trailing physical ranges | `454` |
| Structural validation checks | all passed |

FAT contains 122 entries without FNT paths. All of
them are accounted for by overlay table file IDs; this is not treated as missing
filesystem data. FAT payload ranges do not overlap.

## Method

Analyzer: [`SakuraiTsubaki/Decompilation@dbc8272`](https://github.com/SakuraiTsubaki/Decompilation/commit/dbc8272172cfc051e1108b14291a437d1c56bafb)

```console
python tools/nds_rom_analyzer/analyzer.py /path/to/input.nds --output analysis/generated/rom-structure --label "포켓몬스터Pt 기라티나 (Korea, CPUK, header ROM version 0)"
```

Recorded environment: Windows `10.0.26200`, PowerShell Core `7.6.5`, Python
`3.12.14`. The complete generated evidence is under
[`analysis/generated/rom-structure/`](generated/rom-structure/).

## Confidence

- **Confirmed:** numeric header fields, region bounds, RAM addresses, table
  entries, paths, hashes, CRC calculations, file counts, and comparisons.
- **Probable:** semantic file-format labels based only on recognized leading
  magic or Nintendo compression markers.
- **Hypothesis:** none automatically assigned; unrecognized files remain unknown.

## Verification

All checks in `config/structure-inventory.json` passed: actual versus nominal
capacity, used-ROM bounds, header/logo/banner CRCs, FAT non-overlap, complete
overlay-to-FAT references, and complete accounting of FAT entries by FNT or
overlay reference.

The raw secure-area range and hash are recorded. Decrypted secure-area CRC
validation is explicitly **not performed**; CRC of encrypted raw bytes is not
used as corruption evidence.

Cross-version evidence is stored in
[`SakuraiTsubaki/Decompilation/research/generation-iv-rom-structure`](https://github.com/SakuraiTsubaki/Decompilation/tree/dbc8272172cfc051e1108b14291a437d1c56bafb/research/generation-iv-rom-structure).

## Unknowns and next work

Semantic parsing of NARC members, message/text banks, Pokémon personal data,
moves, items, maps, event scripts, graphics, audio, and individual executable
functions remains pending. Physical ranges labeled `unreferenced` are not
claimed to be unused until code references are analyzed.
