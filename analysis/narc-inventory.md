# NARC and member analysis

This repository records the complete NARC/member inventory for the verified input in `config/target.json`.

- Top-level NARCs: **215**
- Valid top-level NARCs: **215**
- Malformed top-level NARCs: **0**
- Nested NARCs: **2**
- Total members: **53565**
- Confirmed LZ10/LZ11 members: **2490**
- Unknown members: **35025**

The common parser and tests are pinned to [SakuraiTsubaki/Decompilation commit `70cf09995eaf676f2481353ac0bfa5ef654bb957`](https://github.com/SakuraiTsubaki/Decompilation/commit/70cf09995eaf676f2481353ac0bfa5ef654bb957). Complete per-member records are in ordered CSV shards under `analysis/generated/narc-inventory/members/`. ROM and raw member payload bytes are not committed.

Evidence terms follow Confirmed / Probable / Hypothesis. A known magic or compression marker remains Probable until its structure or stream is validated.
