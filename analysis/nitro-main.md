# ARM9 `NitroMain` analysis

## Verified target
- Game: Pokémon Platinum
- Game code: `CPUK`
- Region/language: Korea / Korean
- ROM identity: `manifests/rom-baseline.json`

## Entry and boundary
- `_start` loads `0x02000C89`; bit 0 selects Thumb state.
- `NitroMain` Thumb entry: `0x02000C88`.
- Observed main-function instruction/literal boundary: `0x02000C88..0x02000E17`.
- Literal pool begins at `0x02000E18`.
- Code span size: `0x190` (400) bytes.
- SHA-256 of that observed code span: `d352e8f7fd6854aafcd123a0f4cacd4cad2528893eb57f5ac75568fe64bcfdab`.
- Call sites in the observed body: 49 total, including one register-indirect `BLX` callback site.

## Matched high-level flow
The local Korean target follows the `pret/pokeplatinum` `NitroMain` organization: system/VRAM/input initialization, GBA-cartridge state setup, backlight, RTC and application initialization, font managers, save-data creation, sound/timer startup, DWC/save checks, reset-parameter based application selection, RNG/brightness/play-time initialization, and the permanent main loop.

The Platinum frame loop additionally exposes the application-manager and communication-system organization clearly: communication update gates application/task execution, then RTC, play-time, VBlank, brightness, fade, callback, sound, and post-VBlank task processing are performed each frame.

## Generation IV comparison
- Entry remains under the same ARM9 startup framework as D/P, but the startup helper offsets and `NitroMain` entry have moved.
- The observed Platinum body is 20 bytes larger than the D/P body.
- Function naming and subsystem organization are tracked from Platinum-specific reconstruction rather than copied from D/P.

## Evidence
- Local Korean ROM disassembly and literal targets.
- Cross-check: `pret/pokeplatinum`, `src/main.c`.

## Next mapping pass
1. Resolve every direct target to Platinum names where confirmed.
2. Map `RunApplication`, application enqueueing, communication update, fade, and task-manager paths.
3. Trace the opening/game-start overlays.
4. Compare the Korean target against other language/region revisions without conflating addresses.
