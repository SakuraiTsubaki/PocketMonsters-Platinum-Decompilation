# Platinum Korean observed ROM — structural baseline

**Date observed:** 2026-09-14  
**Verification:** Observed  
**Target:** project-provided Korean Platinum (`CPUK`, header version 0)

This target is useful as direct structural evidence, but its whole-ROM cryptographic identity is currently kept separate from the project's canonical-clean-dump question. The observations below are byte-level facts about the supplied target.

## Nintendo DS container overview

- ROM size: 128 MiB.
- ARM9 overlays: 122.
- FAT entries: 461.
- FNT-named files: 339.
- NARC files identifiable by extension: 215.
- The FNT contains explicit top-level `debug` and `frontier` areas.

## D/P-era archives retained alongside Platinum archives

Platinum does not simply replace all Diamond/Pearl-era resources. Several D/P archives remain present byte-for-byte while Platinum-specific archives are stored alongside them.

Confirmed exact matches against the observed Diamond USA Rev 5 target include:

| Platinum retained path | Relationship |
| --- | --- |
| `poketool/personal/personal.narc` | byte-identical to Diamond `personal.narc` |
| `poketool/personal/growtbl.narc` | byte-identical growth-table archive |
| `poketool/waza/waza_tbl.narc` | byte-identical D/P move-data archive |
| `itemtool/itemdata/item_data.narc` | byte-identical D/P item-data archive |
| D/P encounter archives | retained alongside Platinum encounter data |

Likewise, large base resources coexist with Platinum replacements, including both base and `pl_*` graphics, messages, and sound archives. This means future reconstruction must distinguish **retained compatibility/source resources** from the **active Platinum data path** rather than treating every present archive as an independent active subsystem.

## Active Platinum data counts

Observed active Platinum archives include:

| Data | Archive/member count |
| --- | ---: |
| `pl_personal.narc` | 508 × 44-byte records |
| `evo.narc` | 508 × 44-byte records |
| `wotbl.narc` | 508 variable-length members |
| `pl_waza_tbl.narc` | 471 × 16-byte records |
| `pl_item_data.narc` | 446 × 34-byte records |
| trainer data | 928 records |
| trainer party data | 928 members |
| `pl_enc_data.narc` | 183 × 424-byte members |
| field script archive | 1,124 members |
| `pl_msg.narc` | 714 members |

## D/P → Platinum record-level deltas

Against Diamond's corresponding data:

- `pl_personal`: among the first 501 records, exactly six differ (`114, 125, 239, 352, 357, 466`); seven additional records are present after the D/P range.
- `evo.narc`: the first 501 evolution records are byte-identical to D/P and seven records are appended.
- level-up learnsets: 81 of the first 501 members differ, plus seven added members.
- move table: among all 471 move records, only record ID `95` differs between observed Diamond and Platinum data.
- item table: 242 of the first 442 records differ and four records are appended. These raw differences require field decoding before being interpreted as 242 distinct player-facing behavior changes.

## Form-data architecture

The public source reconstruction distinguishes alternate-form resources by capability: some forms have unique species data, some unique icons, and some only unique sprites. Platinum's moveset indices extend after the National Dex range for Deoxys forms, Wormadam Sandy/Trash, Giratina Origin, Shaymin Sky, and the five Rotom appliance forms. This matches the expanded record counts observed in the ROM and must be reconstructed as form-aware data, not as ordinary new National Dex species.

## Debug/development-named content

`debug/cb_edit/d_test.narc` is present in the FNT and is 11,744 bytes with 12 archive members. Its members include standard Nintendo 2D resource containers (`RGCN`, `RLCN`, `RCSN`, `RECN`, `RNAN`).

Presence is confirmed. Runtime reachability is not yet proven, so the archive is currently classified as **debug/development-named data pending call-site analysis**, not automatically as unused.

## Reconstruction implications

1. Track retained D/P resources and active Platinum replacements separately.
2. Decode all personal/evolution/move/item record fields and convert raw byte deltas into semantic version differences.
3. Resolve the seven additional data records through the form/index registry before assigning species/form labels.
4. Trace all references to `debug/cb_edit/d_test.narc` and other development-named resources.
5. Expand member-level comparison into encounters, scripts, trainers, messages, maps, graphics, audio, and event flags.
