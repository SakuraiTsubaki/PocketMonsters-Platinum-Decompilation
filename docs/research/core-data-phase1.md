# Core data Phase 1 — Platinum active tables and HGSS transition

## Target / evidence status

The locally available Korean Platinum image (`CPUK`, version 0) is preserved as a **comparison source**, not a whole-ROM clean-match target. `manifests/clean_reference.json` records the external clean-reference identity separately. All findings below are therefore content-level **Observed** results unless independently matched elsewhere.

## Active Platinum core archives

| Dataset | Members | Record form |
| --- | ---: | --- |
| `pl_personal` | 508 | 44-byte `SpeciesData` records |
| evolution | 508 | 44-byte fixed records |
| level-up learnsets | 508 | packed 16-bit entries + `0xFFFF` sentinel |
| `pl_waza_tbl` | 471 | 16-byte move records |
| `pl_item_data` | 446 | 34-byte item records |
| `pl_growtbl` | 8 | 404-byte growth tables |

Platinum retains multiple Diamond/Pearl-era archives alongside the active `pl_*` tables; retained and active datasets must not be conflated.

## Diamond/Pearl → Platinum structural delta

- personal: 501 → 508 records.
- evolution: 501 → 508 records; all seven new evolution records are zero-filled.
- learnsets: 501 → 508 records; 81 shared species/form learnsets change.
- moves: 471 → 471; exactly one record changes: Hypnosis (95), accuracy `70 → 60`.
- items: 442 → 446; raw-index comparison includes insertion/reordering effects and is not yet treated as a semantic change count.
- growth tables: unchanged byte-for-byte.

### Seven new data-form indexes

| Index | Form |
| ---: | --- |
| 501 | Giratina Origin |
| 502 | Shaymin Sky |
| 503 | Rotom Heat |
| 504 | Rotom Wash |
| 505 | Rotom Frost |
| 506 | Rotom Fan |
| 507 | Rotom Mow |

These are alternate-form personal/learnset records, not separate evolution targets.

## Platinum → HeartGold/SoulSilver core delta

HeartGold and SoulSilver are byte-identical to each other for all six core datasets listed here.

| Dataset | Pt → HGSS |
| --- | --- |
| personal | 272 / 508 records differ |
| evolution | 0 / 508 differ |
| learnsets | exactly 14 records differ |
| move table | exactly 1 / 471 differs (Hail, ID 258) |
| item table | 446 → 514; raw shared-index diff 29, with key-item insertion/reordering present |
| growth | byte-identical |

### Personal-data field distribution

The 272 changed personal records are dominated by two systems:

- TM/HM compatibility masks: 170 records change.
- Safari flee rate: 134 records change.

Other directly isolated changes include:

- Electabuzz (125), Magmar (126), Elekid (239), Magby (240): the rare Electirizer/Magmarizer entries present in Platinum are cleared in HGSS.
- Electivire (466) and Magmortar (467): their rare Electirizer/Magmarizer entries remain.
- Shuckle (213): both held-item slots change from Oran Berry (155) to Berry Juice (43).
- Pichu (172): `bodyColor/flipSprite` byte changes `0x02 → 0x82`; color remains 2 and only the `flipSprite` bit changes `0 → 1`.

## All 14 Platinum → HGSS level-up-learnset changes

The following table gives the complete record contents for every changed learnset. No other Platinum learnset differs from HGSS.

| Index | Species/form | Platinum | HGSS |
| ---: | --- | --- | --- |
| 155 | Cyndaquil | L1 Tackle; L1 Leer; **L4 Smokescreen**; L10 Ember; L13 Quick Attack; L19 Flame Wheel; L22 Defense Curl; L28 Swift; L31 Lava Plume; L37 Flamethrower; L40 Rollout; L46 Double-Edge; L49 Eruption | same except **L6 Smokescreen** |
| 156 | Quilava | L1 Tackle; L1 Leer; L1 Smokescreen; **L4 Smokescreen**; L10 Ember; L13 Quick Attack; L20 Flame Wheel; L24 Defense Curl; L31 Swift; L35 Lava Plume; L42 Flamethrower; L46 Rollout; L53 Double-Edge; L57 Eruption | same except second Smokescreen is **L6** |
| 157 | Typhlosion | L1 Gyro Ball; L1 Tackle; L1 Leer; L1 Smokescreen; L1 Ember; **L4 Smokescreen**; L10 Ember; L13 Quick Attack; L20 Flame Wheel; L24 Defense Curl; L31 Swift; L35 Lava Plume; L42 Flamethrower; L46 Rollout; L53 Double-Edge; L57 Eruption | same except second Smokescreen is **L6** |
| 249 | Lugia | L1 Whirlwind; L9 Safeguard; L15 Gust; L23 Recover; L29 Hydro Pump; L37 Rain Dance; L43 Swift; L51 Natural Gift; L57 AncientPower; L65 Extrasensory; L71 Punishment; L79 Future Sight; L85 Aeroblast; L93 Calm Mind; L99 Sky Attack | L1 Whirlwind; **L1 Weather Ball**; L9 Gust; **L15 Dragon Rush**; L23 Extrasensory; L29 Rain Dance; L37 Hydro Pump; **L43 Aeroblast**; L50 Punishment; L57 AncientPower; L65 Safeguard; L71 Recover; L79 Future Sight; L85 Natural Gift; L93 Calm Mind; L99 Sky Attack |
| 250 | Ho-Oh | L1 Whirlwind; L9 Safeguard; L15 Gust; L23 Recover; L29 Fire Blast; L37 Sunny Day; L43 Swift; L51 Natural Gift; L57 AncientPower; L65 Extrasensory; L71 Punishment; L79 Future Sight; L85 Sacred Fire; L93 Calm Mind; L99 Sky Attack | L1 Whirlwind; **L1 Weather Ball**; L9 Gust; **L15 Brave Bird**; L23 Extrasensory; L29 Sunny Day; L37 Fire Blast; **L43 Sacred Fire**; L50 Punishment; L57 AncientPower; L65 Safeguard; L71 Recover; L79 Future Sight; L85 Natural Gift; L93 Calm Mind; L99 Sky Attack |
| 382 | Kyogre | L1 Water Pulse; L5 Scary Face; L15 AncientPower; L20 Body Slam; L30 Calm Mind; L35 Ice Beam; L45 Hydro Pump; L50 Rest; L60 Sheer Cold; L65 Double-Edge; L75 Aqua Tail; L80 Water Spout | L1 Water Pulse; L5 Scary Face; L15 Body Slam; **L20 Muddy Water**; **L30 Aqua Ring**; L35 Ice Beam; L45 AncientPower; L50 Water Spout; L60 Calm Mind; L65 Aqua Tail; L75 Sheer Cold; L80 Double-Edge; **L90 Hydro Pump** |
| 383 | Groudon | L1 Mud Shot; L5 Scary Face; L15 AncientPower; L20 Slash; L30 Bulk Up; L35 Earthquake; L45 Fire Blast; L50 Rest; L60 Fissure; L65 Solar Beam; L75 Earth Power; L80 Eruption | L1 Mud Shot; L5 Scary Face; **L15 Lava Plume**; **L20 Hammer Arm**; L30 Rest; L35 Earthquake; L45 AncientPower; L50 Eruption; L60 Bulk Up; L65 Earth Power; L75 Fissure; L80 Solar Beam; **L90 Fire Blast** |
| 384 | Rayquaza | L1 Twister; L5 Scary Face; L15 AncientPower; L20 Dragon Claw; L30 Dragon Dance; L35 Crunch; L45 Fly; L50 Rest; L60 ExtremeSpeed; L65 Hyper Beam; L75 Dragon Pulse; L80 Outrage | L1 Twister; L5 Scary Face; L15 Crunch; **L20 Hyper Voice**; L30 Rest; **L35 Air Slash**; L45 AncientPower; L50 Outrage; L60 Dragon Dance; L65 Fly; L75 ExtremeSpeed; L80 Hyper Beam; **L90 Dragon Pulse** |
| 449 | Hippopotas | L1 Tackle; L1 Sand-Attack; L7 Bite; L13 Yawn; L19 Take Down; L25 Sand Tomb; L31 Crunch; L37 Earthquake; L44 Double-Edge; L50 Fissure | same, plus **L19 Dig** |
| 450 | Hippowdon | L1 Ice Fang; L1 Fire Fang; L1 Thunder Fang; L1 Tackle; L1 Sand-Attack; L1 Bite; L1 Yawn; L7 Bite; L13 Yawn; L19 Take Down; L25 Sand Tomb; L31 Crunch; L40 Earthquake; L50 Double-Edge; L60 Fissure | same, plus **L19 Dig** |
| 483 | Dialga | L1 Dragon Breath; L1 Scary Face; L10 Metal Claw; L20 AncientPower; L30 Dragon Claw; L40 Roar of Time; L50 Heal Block; L60 Earth Power; L70 Slash; L80 Flash Cannon; L90 Aura Sphere | L1 Dragon Breath; L1 Scary Face; L6 Metal Claw; L10 AncientPower; L15 Slash; **L19 Power Gem**; **L24 Metal Burst**; L28 Dragon Claw; L33 Earth Power; L37 Aura Sphere; L42 Flash Cannon; **L46 Roar of Time** |
| 484 | Palkia | L1 Dragon Breath; L1 Scary Face; L10 Water Pulse; L20 AncientPower; L30 Dragon Claw; L40 Spacial Rend; L50 Heal Block; L60 Earth Power; L70 Slash; L80 Aqua Tail; L90 Aura Sphere | L1 Dragon Breath; L1 Scary Face; L6 Water Pulse; L10 AncientPower; L15 Slash; **L19 Power Gem**; L24 Aqua Tail; L28 Dragon Claw; L33 Earth Power; L37 Aura Sphere; **L42 Hydro Pump**; **L46 Spacial Rend** |
| 487 | Giratina Altered | L1 Dragon Breath; L1 Scary Face; L10 Ominous Wind; L20 AncientPower; L30 Dragon Claw; L40 Shadow Force; L50 Heal Block; L60 Earth Power; L70 Slash; L80 Shadow Claw; L90 Aura Sphere | L1 Dragon Breath; L1 Scary Face; L6 Ominous Wind; L10 AncientPower; L15 Slash; **L19 Shadow Sneak**; **L24 Destiny Bond**; L28 Dragon Claw; L33 Earth Power; L37 Aura Sphere; L42 Shadow Claw; **L46 Shadow Force** |
| 501 | Giratina Origin data form | identical to Platinum Altered-form list above | identical to HGSS Altered-form list above |

## Move-table deltas

### Move 95 — Hypnosis

Diamond/Pearl: accuracy 70. Platinum/HGSS: accuracy 60. No other field changes.

### Move 258 — Hail

Platinum: flags byte `0x02` (`MOVE_FLAG_CAN_PROTECT`). HGSS: `0x00`. Effect, class, type, PP, range, priority, contest fields, and every other byte remain identical.

## Item-table caution and confirmed HGSS-level changes

The Platinum `ItemData` layout is documented in `include/item.h`, but raw index comparison across games is not sufficient because key-item insertions/reordering occur. Name-aligned semantic comparison is the required next step.

Already confirmed without relying on index-shift interpretation:

- Growth/Damp/Stable/Gooey Mulch (IDs 95–98 in Platinum) lose their Platinum field-use function in HGSS.
- The HGSS table expands from 446 to 514 members and includes Johto/HGSS key-item space.

## Verification

Record counts and byte-level deltas are direct ROM observations. Structure interpretation is cross-checked against PRET's Platinum/HGSS source reconstructions. Whole-ROM `Matched` status is not claimed for the project-provided Korean Platinum/HGSS comparison images.
