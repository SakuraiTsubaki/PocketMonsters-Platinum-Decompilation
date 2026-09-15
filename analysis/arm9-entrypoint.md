# ARM9 entrypoint — Phase 1

Target: `CPUK` / Korea Korean / ROM version byte `0`.

## Observed boundaries

| Address | Working identity | Evidence |
|---:|---|---|
| `0x02000800` | `_start` | Exact ROM entrypoint; startup structure matches the Generation IV NitroSDK crt0 sequence |
| `0x02000954` | `INITi_CpuClear32` | Three direct clear calls; instruction sequence equivalent to the D/P startup helper |
| `0x02000970` | `MIi_UncompressBackward` | Direct startup call; instruction sequence equivalent to the D/P decompressor helper |
| `0x02000A1C` | `do_autoload` | Direct startup call; structure continues the same crt0 autoload path |
| `0x02000AB0` | `init_cp15` | First startup call; CP15 initialization pattern |
| `0x02000B98` | `NitroStartUp` | Startup call position and shared runtime pattern |
| `0x020E3388` | `_fp_init` | Reference-supported from startup call ordering |
| `0x020E4AFC` | `__call_static_initializers` | Reference-supported from startup call ordering |

The `NitroMain` literal is `0x02000C89`; bit 0 marks Thumb state, giving code address `0x02000C88`.

## Startup fingerprint

Within the first `0x200` bytes, the Platinum startup is nearly identical to HeartGold: only five bytes differ. Those differences are the two external branch displacements used by runtime initialization plus the `NitroMain` literal. The common body, helper layout, stack setup, memory clearing, BSS/cache handling, and autoload path are otherwise shared in this window.

## Confidence

- Addresses and bytes: **Observed** from the verified Korean Platinum ROM.
- Runtime identities: **Reference-supported / sequence-matched** against the verified D/P NitroSDK startup reconstruction; not treated as a claim that the entire Platinum executable matches D/P.
- Game-specific code beyond the startup chain remains address-named until independently reconstructed.
