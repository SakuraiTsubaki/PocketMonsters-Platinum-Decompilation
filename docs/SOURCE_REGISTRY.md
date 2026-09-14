# Public Source Registry — Pocket Monsters Platinum

This registry tracks public material used to reconstruct and compare Pocket Monsters Platinum without assuming access to an original ROM image.

## Rules

- Japanese earliest retail release is the historical baseline.
- Record every official region, language, and revision separately.
- Do not mark releases identical without positive evidence.
- Preserve conflicting claims and their sources.
- Record redistribution/licensing status before copying external material into this repository.
- Every research result derived from a source should link back to a registry entry.
- The registry is an exhaustive-census index, not a representative reading list. Historical, superseded, forked, archived, and conflicting public research remains in scope.

## Evidence status

- `CONFIRMED_IDENTICAL`
- `CONFIRMED_DIFFERENT`
- `UNVERIFIED`
- `CONFLICTING_EVIDENCE`

## Source registry

| ID | Source | Source type | Game | Region | Language | Revision | Component / scope | Original or derived | Redistribution status | Verification | Cross-check | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `PT-SRC-0001` | [pret/pokeplatinum](https://github.com/pret/pokeplatinum) | Public decompilation | Platinum | USA target | English | Rev 0 / Rev 1 | Code, data, scripts, assets, build/reconstruction | Derived source-reconstruction project | Follow upstream terms; no retail ROM | Strong technical reference | `PT-SRC-0002`, revision metadata | Builds USA Rev 1 SHA-1 `0862ec35b24de5c7e2dcb88c9eea0873110d755c` and supports USA Rev 0 SHA-1 `ce81046eda7d232513069519cb2085349896dec7`. INSTALL documents the Rev 0 GTS wanted-level display bug and its correction in the second North American shipment. |
| `PT-SRC-0002` | [JimB16/PokePlat](https://github.com/JimB16/PokePlat) | Historical disassembly/source project | Platinum | USA target | English | Rev 1, other-revision code present | ARM9, ITCM/DTCM, overlays, scripts, battle AI, NARC, text, trainers, items, encounters, moves, Pokémon data, Battle Tower, events, sprites | Derived technical project | Follow upstream terms; no retail ROM | Major historical technical reference | PRET; PPRE; SDSME | Reports 99% script disassembly and compilable data classes. Also records its technical lineage from PPRE and SDSME, making those upstream tools part of the research graph. |
| `PT-SRC-0003` | [Project Pokémon PPRE](https://github.com/projectpokemon/PPRE) | Historical ROM-editor source | Platinum / Gen IV | USA-focused | English | multiple supported games | Pokémon, text, move editing; file-format/tool lineage | Derived technical tooling | Follow upstream terms | Historical technical reference | PokePlat; other editors | PPRE supports all Gen IV mainline games and is explicitly cited by PokePlat as a source for interpretation/conversion tooling. |
| `PT-SRC-0004` | [DS-Pokemon-Rom-Editor/scrcmd-database](https://github.com/DS-Pokemon-Rom-Editor/scrcmd-database) | Script-command research database | D/P/Pt/HGSS | Multi-game | Technical metadata | current V2 + legacy | Script opcodes, movement commands, macros, sounds, flags/vars, comparisons, special overworld IDs | Derived from DSPRE/decomp/community | Follow upstream license | Strong living technical reference | PRET Platinum/HGSS; DSPRE | V2 is source of truth. Platinum command tables and movement IDs are synchronized from PRET decompilation. |
| `PT-SRC-0005` | [Project Pokémon — Gen IV BDHC terrain research](https://projectpokemon.org/home/forums/topic/37816-gen-iv-bdhc-files-terrain-settings/) | Reverse-engineering research | D/P/Pt/HGSS | Multi-game | English research notes | N/A | BDHC terrain/collision format | Derived community research | Citation/link only | Technical reference; reproduce before promoting | Editors/decomp | Documents BDHC structure shared across Gen IV research; verify exact Platinum usage and regional variants. |
| `PT-SRC-0006` | [Bulbapedia — List of glitches in Generation IV](https://bulbapedia.bulbagarden.net/wiki/List_of_glitches_in_Generation_IV) | Specialist glitch index | D/P/Pt/HGSS | Multi-region | English | multiple | GTS wanted-level display oversight, Member Card name error, shared battle/overworld/GTS/save glitches | Derived | Citation/link only | Secondary index | PRET code, technical threads, contemporary reports | Used as a discovery index only; each glitch must be mapped to exact revision/region and stronger evidence. |

## Difference registry

| ID | Japanese baseline | Compared release | Component | Difference class | Evidence status | Source IDs | Notes |
|---|---|---|---|---|---|---|---|
| `PT-DIFF-0001` | Japanese Platinum baseline | USA Rev 0 / Rev 1 branch | GTS wanted-level display | `REVISION_BUGFIX` | `CONFIRMED_DIFFERENT` | `PT-SRC-0001` | PRET documents a North American Rev 0 error where the GTS does not display the level range of a wanted Pokémon; Rev 1 fixes it. This does not yet map the Japanese baseline behavior, which remains a separate comparison task. |

## Census workstreams

The survey includes official/archived material; all public decomp/disassembly branches, forks, issues and history; tools and source dependencies; technical forums and attachments; preservation metadata; distributions/Wonder Cards/Wi-Fi/GTS; glitches and TAS research; unused/debug/development material; localization/censorship; demos/service software; databases/wikis as leads; and public web-archive recoveries.

## Coverage backlog

The registry is expected to cover release/revision inventories; ARM9/ARM7 and overlays; NitroFS/NARC; scripts; text; maps; Distortion World; events; Pokémon/trainer/item/move/encounter data; Super Contest; Battle Frontier/Tower; graphics/sprites/models/animation; audio; save; local wireless/NWC/GTS/Mystery Gift; distribution data; bugs/fixes; unused/debug/development remnants; localization/censorship; tools; specialist databases/wikis; and archival community research. Entries above are only the first census batch and do not define the final scope.
