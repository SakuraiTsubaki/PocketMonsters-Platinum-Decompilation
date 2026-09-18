# NARC and member inventory

## Provenance

- Input: `포켓몬스터Pt 기라티나 (Korea, CPUK, header ROM version 0)`
- ROM SHA-256: `51050f65776f402f86b8b2b2d3b84ab5bbe80dbec75129c86f8bd9b447f11d7b`
- Tool: `narc_inventory 1.0.0`
- ROM bytes committed: **no**

## Confirmed totals

| Metric | Count |
| --- | ---: |
| Top-level NARC candidates | 215 |
| Valid top-level NARCs | 215 |
| Malformed top-level NARCs | 0 |
| Nested NARCs | 2 |
| Total members, including nested containers | 53565 |
| Named members | 0 |
| Compression-marker members (Probable or Confirmed) | 4457 |
| Structurally decoded LZ10/LZ11 members (Confirmed) | 2490 |
| Invalid LZ-like leading markers | 536 |
| Huffman/RLE markers not decoded in this phase | 1431 |
| Unknown members | 35025 |

## Evidence language

Offsets, sizes, hashes, block layouts, and successful structural checks are **Confirmed**. A leading magic or compression marker without complete structural validation remains **Probable**. No semantic field names are inferred from payload shape alone.

No raw member payload is retained. `narc-inventory.json` and the CSV files preserve the complete reproducible structure and hash evidence.
