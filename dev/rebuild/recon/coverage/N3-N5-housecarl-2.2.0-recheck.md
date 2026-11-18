# N3–N5 recheck on houseCARL 2.2.0

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (finding). Follows [`N3-N5-scripts-assets-runtime.md`](N3-N5-scripts-assets-runtime.md) (2.1.2,
2026-10-31). Probed live on houseCARL **2.2.0** (`7f1d8baa`, same tree as tag `v2.2.0`), installed 2026-11-18,
against the ARR instance, profile `ARR Personal Profile` (3,260 active plugins; the eval profile is no longer
selected). Same subject: The Rot Below (`CJ03Elroy.esp`). Read-only throughout.*

## Verdict

**houseCARL's asset-layer project shipped whole in 2.2.0** (all 30 plan steps: one asset door, shared selectors, one
walk grammar, the runtime-layer reader). **The 2026-10-31 holds are met.** What's left open is tidying and
performance, which doesn't block us.

## What changed, against the 2.1.2 gaps

| 2.1.2 gap | 2.2.0 | Live result |
|---|---|---|
| Walk seeds refused `@file` | Every list parameter takes `@file` | `records=["@seeds.jsonl"]` (835 FormIDs) accepted |
| No orphan view | `exclude=` takes a walk's `to_file=` | `provider=… exclude=["@walk.jsonl"]` → 223 shipped-but-unreached files in one call |
| Decompile: one `.pex`, BSA needs extract | `decompile_script provider= / under= / paths=`, archives read directly | **156 of 156 scripts decompiled in one call, ~1 min**, no extract |
| No SPID/KID/BOS/FLM reader | `housecarl_layer` (replaces `housecarl_skypatcher_layer`, old name refused) reads all five | `plugins={names:[CJ03Elroy.esp]}`: **10 SkyPatcher + 2 SPID lines**, each labelled target / filter; KID, BOS, FLM 0. ~20 s |
| SkyPatcher filter by name only | `formids=` / `plugins=` select lines by what they name, EditorID lines included | As above: the 10 UBE lines the 2.1.2 filter missed |
| Who does a SPID/KID line reach | `records where=["spid reaches <line>"]` / `["kid reaches <line>"]` | Not run here |
| Walk pulled every nearby NPC's voice | Walk follows what a record is made of; `walk.through` takes edge kinds; NPCs past a seed are not entered | No stray voice from unseeded NPCs |
| Missing-facegen false alarms | FaceGen tools name the pair a face is drawn from | 46 creature-race NPCs now say "race has no FaceGenHead flag: no FaceGen, as the CK bakes none" |
| SKSE config audit swallowed SkyPatcher INIs | `skse findings="config"` leaves them to `housecarl_layer` | Not re-run |

The Rot Below job now takes **five calls and no shell step**: records `to_file`, then the walk on `@file`, then
`provider` + `exclude`, then `decompile_script provider=`, then `housecarl_layer plugins=`. Of the decompiled
scripts, 17 of 156 hold perk, spell, actor-value, spawn or item calls (a grep over the `.psc`).

Defects still visible, now cleanly:
- Nine human NPCs (`CJ03Livestock*`, `CJ03MoldCultist…`) have no FaceGen pair.
- Two scripts are attached but shipped by nothing: `CJ03DisableJournal1.pex` on the main quest, and
  `KillinWater.pex` on cell `CJ031OldPrison`.
- These are BUGS.md leads, not checked.

## Still open (houseCARL issues), none blocking

| Issue | What | Effect on us |
|---|---|---|
| #1288 | The `ksws03_quest.esp` exclusion paragraph still repeats in full on every answer | Tokens |
| #1289 | No elapsed time on asset, skse, decompile and layer answers | We can't time calls from the answer |
| #1290 | Spill files accumulate in the install folder | Housekeeping |
| #1291 | `links=` takes two lines per link | Tokens on mesh reads |
| #1287 | Still open, though the changelog ships batch, archive-reading decompile | Bookkeeping for houseCARL |
| — | Script call-site scan ("who calls AddPerk") | Not shipped. Decompile-by-provider plus a grep covers it |
| — | `housecarl_layer`: OAR, IED, DESC, DSD answered "not read"; LID "not read yet" | OAR is read by the OAR skill from files |

## New observations, for houseCARL

1. **The whole-mod walk is still slow on ARR.** About 3 min 50 s for 835 seeds at the default `max_nodes=2000`, about
   the same as 2.1.2's 233 s, because the dev-list speed-up was for templated-NPC walks. With `max_nodes=60000` it
   reached 5,395 nodes in about the same time; seeding cells pulls every placed object's vanilla mesh (4,269
   elsewhere nodes). Seeding without CELL is the cheaper whole-mod shape.
2. **The default `max_nodes=2000` cuts a whole-mod walk** (835 seeds plus what they pull). The walk and the
   `exclude=` answer both say so, but the orphan list still holds 101 `.pex` that a full walk may reach. A whole-mod
   seed probably wants a larger default, or a note that names the count it would need.
3. **Walk notes come before the census, even on `counts_only` and `to_file=`.** 46 one-line FaceGen-race notes (about
   6k chars) pushed the edge and standing tables out of a 3,000-char budget. Fold same-reason notes into one counted
   line, or render the census first.
4. **A `housecarl_layer plugins=` answer carries whole-layer noise.** It printed 23 SkyPatcher no-op writes about
   unrelated vanilla cells and two Milfactory same-path collisions, about 4.5k of its 12k, none naming the selected
   plugin. Under a selector, limit them to the selected lines, or reduce them to a count.
5. **Timing is uncertain from the caller's side**, because tool calls in one message may run concurrently: a `date`
   stamp sent beside a call does not bracket it. The times above come from stamps sent in separate messages. #1289
   would settle it.

## For the rebuild

- **Holds lifted** (`../../decisions.md`, 2026-10-31): the asset-layer PRs have landed, so graded and B1–B4 runs that
  measure asset or runtime calls can go ahead on 2.2.0. The spec can now name real calls, not just capabilities.
- **Coverage script (N2) scope shrinks.** houseCARL now answers each part:
  - which files a mod ships that no record reaches (walk + `exclude=`);
  - which runtime lines name its records (`layer plugins=`), and who a SPID or KID line reaches;
  - every script decompiled in one call.

  What's left for the script is joining these into one disposition list, plus the call-list grep over the
  decompiled scripts.
- **houseCARL's own skills now carry only framework knowledge**, with no tool or parameter names; the tool
  descriptions say how to call. That is a design input for our skills (A1–A5's "which tools" line) and for the
  trigger evals, which load houseCARL alongside ours.
- **Renamed parameters** in 2.2.0: `pex=` / `asset_paths=` / `mesh_paths=` → `paths=`; `npc=` → `formids=`;
  `skypatcher_layer` → `layer`; copy's `exclude_types=` → `exclusions=`. Our live docs and the 1.x skills name none
  of them. The 2.1.2 probe doc's reproduce steps use the old names (ARCHIVE, left as written).
