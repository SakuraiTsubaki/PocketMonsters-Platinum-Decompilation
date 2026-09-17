# ROM structure inventory: 포켓몬스터Pt 기라티나 (Korea, CPUK, header ROM version 0)

## Provenance

- Tool: `nds_rom_analyzer 1.0.0`
- Input basename: `포켓몬스터Pt 기라티나.nds`
- Input SHA-256: `51050f65776f402f86b8b2b2d3b84ab5bbe80dbec75129c86f8bd9b447f11d7b`
- ROM bytes committed: no
- Confidence: **Confirmed** for directly parsed offsets, fields, hashes, and CRC results.

## Core structure

| Field | Value |
| --- | --- |
| Game code | `CPUK` |
| ROM/header size | `134217728` / `16384` bytes |
| ARM9 ROM / RAM / entry / size | `0x4000` / `0x02000000` / `0x02000800` / `1061624` |
| ARM7 ROM / RAM / entry / size | `0x40a800` / `0x02380000` / `0x02380000` / `161788` |
| FNT / FAT files / directories | `0x432000` / `461` / `105` |
| ARM9 / ARM7 overlays | `122` / `0` |
| NARC archives | `215` |
| Recognized signatures | `283` |
| Header/logo CRC valid | `True` / `True` |
| Structural validation checks | `True` |
| Secure-area raw encrypted bytes / decrypted CRC validation | `f44e60d2c6696f0f9f76dc93754aaf287c64f6bad6c7864a4d6296aa0822d0b6` / `not performed` |

## Outputs

- `structure.json`: complete machine-readable inventory.
- `nitrofs-files.csv`: every FAT file with path, offsets, size, SHA-256, extension, and detected signature.
- `directories.csv`: complete FNT directory table.
- `overlays-arm9.csv` and `overlays-arm7.csv`: complete overlay tables and RAM placement.
- `unreferenced-ranges.csv`: physical gaps and trailing padding. `unreferenced` does not prove unused.

## Reproduction

```console
python tools/nds_rom_analyzer/analyzer.py /path/to/input.nds --output analysis/generated/rom-structure --label "포켓몬스터Pt 기라티나 (Korea, CPUK, header ROM version 0)"
```

## Unknowns

The secure-area bytes and header checksum field are recorded, but decrypted secure-area CRC validation is not performed; a mismatch against CRC of encrypted raw bytes is not corruption evidence. Magic detection identifies only known leading signatures and compression markers. Unknown or extensionless files remain unclassified rather than receiving inferred names. Semantic analysis of NARC members, text, maps, scripts, Pokémon, moves, and items is deferred.
