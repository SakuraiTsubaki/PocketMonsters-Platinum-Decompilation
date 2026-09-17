# Upstream Bug-Fix Reference: Pokémon Platinum

This record maps confirmed upstream source-level findings to the local Korean Platinum target. It is a reference for reconstruction and does **not** assume that source paths or offsets are identical in the Korean ROM. Each item must be re-located and verified against `CPUK` before a target patch is accepted.

Source surveyed: `pret/pokeplatinum`, `docs/bugs_and_glitches.md` (checked 2026-09-17).

## Confirmed source-level defect families

| ID | Defect | Upstream root-cause area | Semantic correction to verify locally |
|---|---|---|---|
| G4-BAT-018 | Acid rain / acid weather | Pursuit battle subscript | Correct the variable assignment after a switching target faints; the original operation mutates field-condition bits instead of setting the fainted battler variable. |
| G4-BAT-002 | Fire Fang bypasses Wonder Guard | `MoveIsOnDamagingTurn` battle helper | Replace the mistakenly listed Fire Fang effect with the intended Shadow Force effect in the damaging-turn exception set. |
| G4-PT-001 | Post-KO switch-in AI score overflow | post-KO trainer AI scoring | Widen score storage so high matchup scores cannot wrap in an 8-bit value. |
| G4-BAT-005 | Rage clears unrelated volatile state | pre-move Rage cleanup | Clear Rage while preserving other volatile flags; the original mask operation preserves Rage and clears the rest. |
| G4-PT-002 | Trainer Pokémon forms use base-form stats | trainer party construction | Recalculate stats after assigning a non-base form for every trainer-party data format. |
| G4-BAT-006A | Facade animation cumulative Y shift | Facade animation script | Correct overlapping timing so the sprite returns to its intended position. |
| G4-BAT-006B | DynamicPunch animation cumulative X shift | DynamicPunch animation script | Correct shake timing to prevent permanent position drift. |
| G4-BAT-006C | Helping Hand animation cumulative X shift | Helping Hand animation script | Correct loop timing so repeated shakes do not leave a permanent offset. |
| G4-BAT-006D | Strength animation cumulative X shift | Strength battle-animation task | Restore the attacker sprite to its default X position after the task completes. |
| G4-BAT-006E | Spit Up animation cumulative X shift | shake/scale attacker task | Restore the attacker sprite to its default X position after the task completes. |
| G4-ENC-002 | Sticky Hold/Suction Cups fishing bonus missing | encounter-rate modifier | Actually store the doubled encounter-rate value; the original expression computes a product and discards it. |
| G4-PT-003 | Surf/fishing Magnet Pull slot overwritten | water encounter slot selection | Only evaluate Static/random fallback when Magnet Pull did not already choose a Steel-type slot. |
| G4-UI-003 | Defog HM uses Water palette | HM05 item icon data | Use the Flying-type TM/HM palette for Defog. |
| G4-PT-004 | Giratina title-screen hover range too small | title-screen hover calculation | Pass the angle in the unit expected by the sine helper instead of pre-scaling it incorrectly. |
| G4-PT-005 | Wrong VRAM manager initializer | 3D pipeline initialization | Initialize palette VRAM with the palette manager when frame mode is requested, rather than initializing a second texture manager. |

## Local verification requirements

For every item above:

1. Locate the equivalent routine/data in the `CPUK` ROM instead of copying an upstream address.
2. Confirm original Korean behavior with a minimal reproduction or binary/source-equivalent evidence.
3. Record overlay/NitroFS ownership and pre-fix hashes.
4. Apply the smallest semantic correction.
5. Verify adjacent behavior and compare D/P/Pt/HG/SS implementations.
6. Record post-fix hashes and regression evidence in the bugfix matrix.

The upstream list is useful because it supplies root causes, but it is not treated as exhaustive. The project-wide discovery tracks remain mandatory.
