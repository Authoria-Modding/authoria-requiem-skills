# A6: root causes of the houseCARL tool traps T1–T5

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (finding). houseCARL 2.2.0.*

Recon target A6 (`../../recon.md`). The October eval ran on houseCARL 2.1.1; the "Fix: HC" column in
`../../eval-2026-10/distillation/DISTILLATION.md` §3e is re-derived here from the run traces, the 1.x skill text,
the Reqtificator source and the live 2.2.0 tools. Read-only throughout: no houseCARL write tool was called (dry
runs included). Live reads used the ARR instance, profile `ARR Personal Profile`, server `2.2.0+7f1d8baa`.

Refs: `R####` (main agent) and `L####` (lane) are the labels in each run's mined `trace.md`; rule ids are from the
eval's `drill/absolutes/` ledgers. Reqtificator paths are relative to
`Source/Reqtificator/Reqtificator/` in the mod "Authoria - Reqtificator And Requiem Tweak". houseCARL paths are
relative to the houseCARL repo.

## Verdict summary

| Trap | Root cause | Goal needed? | 2.2.0 route | Verdict |
|---|---|---|---|---|
| T1 PRKZ=0 / empty list | REQ_NULL "strip every one" emptied perk lists (AC, FS); "leave Reqtificator output alone" stripped baked perks (TR). npc#64/#104/#266 then called the zero count "an incomplete write" | **No.** The Reqtificator treats null and empty alike and refills the list; a SpellList-templated actor masks it | Empty a list: yes (by index, or ReplaceAll to empty). Unset a list (no count subrecord): no, and not needed | **Skill-induced → delete** npc#63, #64, #104, #266 and the strip rules behind them |
| T2 Remove-by-value; CopyFrom CLAS | Remove-by-value: the 1.x REQ_NULL strip recipe on `Perks` (rp#139, npc recipes). CopyFrom CLAS: the agent's own shape, not in any skill | Strip: no (same as T1). Setting a class: yes | Remove a perk by index; set `Class` by value. The refusals name both. Nothing was "lost": the batch was refused whole, by design | **Skill-induced → delete** (strip). CopyFrom CLAS: **non-problem** |
| T3 ConditionFloat compose | The cited call (FS s1 L1040) **passed**: a verification dry run of a nested one-op compose. No failed condition write found in any FS run | Yes (perk / keyword gates on recipes) | Nested compose in one Add, as the lane did | **Non-problem → nothing.** The 1.x two-op recipe goes with all recipes |
| T4 REQ_NULL scan with `plugins=` | 2.1.1 refused `plugins=` naming an off-order patch even with `source=` that file. The checklist's "none may remain" (rp#53, #114) turned the errored scan into a "clean" claim | A scan of what was written: yes (HP4). "None may remain": no | **Fixed in 2.2.0**: the same shape answers (#1389, live-checked on a disabled-mod patch); refusals are now MCP errors | **Real HC gap, closed.** Skill: delete the compliance absolute; keep one per-type scan |
| T5 capped reads taken as absence | Agents read a window as the whole. houseCARL says "showing first N of M" but not what the hidden rows are, nor the sort | Yes (absence claims drive skips) | Still open: a capped window names no hidden types/plugins and no sort order (live-checked) | **Real HC gap → issue** (draft below) + 1 capability line |

## T1: PRKZ=0 / SPCT=0 and "never an empty ReplaceAll"

**(a) What drove it.** The agents emptied perk lists to strip `REQ_NULL_*` perks. The router's "no REQ_NULL may
remain" family (rp#114, #137, #139, #53, on the fact rp#136) beat npc#43 ("don't clean masked NULLs") in AC s1 and
s3 (AC ledger, "What harmed"). Once a list was empty, npc#64 / #104 / #266 said a zero count is a defect, and the
recipe file added "a serialized zero count is an incomplete write: report the houseCARL bug and do not ship it"
(npc `references/housecarl-recipes.md` L195-L201). houseCARL 2.1.1 could empty a list but not unset it. So:
- AC s1: 84 PRKZ=0 records, 2 denied parser attempts, patch labelled unfinished.
- AC s2: refused `Set Perks = null` (R3753), then a TES4 binary rewriter over 74 records (R3966 states the plan).
- AC s3: fix.py three times over 90 records.
- FS s1 / s1n shipped empty lists after by-index refusals (s1 L1831); s3 used ReplaceAll.
- TR s1 ended with empty SPCT/PRKZ after stripping the MR patch's baked perks (rp#42, a separate wrong rule).

**(b) Was the goal needed? No.**
- *The REQ_NULL perk strip had no gameplay value.* REQ_NULL PERKs are emptied (147/154, DISTILLATION fact 2), and
  the judges scored the strips no_effect (npc distillation X7). So the list never needed emptying.
- *The Reqtificator does not care.* `Transformers/Actors/ActorGlobalPerks.cs:22-34`: every actor that is not
  SpellList-templated (and not `AlreadyReqtified`, `ActorAlreadyReqtifiedSkip.cs:11`) gets
  `record.Perks ??= new ExtendedList<PerkPlacement>()` and the global perks added. Null and empty are handled the
  same, and the output record carries a populated list. `ActorPerksFromRules.cs:34` and
  `ActorSpellsFromRules.cs:38` (ActorEffect) use the same `??=`. `MainLogicExecutor.cs:287-298` runs this over
  every winning NPC.
- *Templated actors mask the list.* With SpellList set, the engine uses the template's perks and spells, and the
  Reqtificator skips the actor (`ActorGlobalPerks.cs:23-24`, `ActorSpellsFromRules.cs:25`).
- *Nobody saw harm.* The controls also shipped zero-count PRKZ (4, 4, 5 and 82 records; AC process F4) and no
  judge flagged it. No engine-side evidence of harm was found; an in-game check was not run.
- *It is a shape no reference carries.* Live: all 776 Requiem.esp NPCs and all 149 NPCs in ARR's handmade AC patch
  with zero perks have the list absent, not empty. That makes it untidy, not wrong.

So the decisions.md 2026-10-30 note holds. The "zero count = incomplete write" rule was never verified, and it is
false for both consumers. One correction: the strip that emptied lists is the REQ_NULL **PERK** case, where the
fact is true but the strip is pointless. It is not the false non-PERK fact.

**(c) 2.2.0 route.** Emptying a list: Remove by index, or ReplaceAll with no elements. Unsetting a list: none. A
keyless Remove clears a whole nullable field only for scalars and sub-structs. On a list it means by-value or
by-index (`src/housecarl-core/CorpusRulebook.cs:369-378`). That is fine, because nothing needs it.

Read side, observed live: a fields read tells the shapes apart (`Perks = [list: 0 item(s)]` against
`ActorEffect = (absent)`), but `where= ["Perks missing"]` counts the present-empty lists as missing (104 of 104 on
the AC control-1-nothink patch, and `Perks exists` gave 0). That is a small read inconsistency, drafted below as
optional.

**(d) Skill-induced → delete** npc#63, #64, #104, #266, the recipe paragraph, and the matching paragraph in npc `references/perks.md` (L150-L153). Do not carry
"don't empty a list you don't own" as a tool rule either: its only trigger was the strip.

## T2: Remove-by-value at batch scale; CopyFrom CLAS

**(a)** *Remove-by-value* was the 1.x strip recipe, `{field_path:"Perks", verb:"Remove", value:"<REQ_NULL_* perk>"}`
(npc `references/housecarl-recipes.md` L188-L191; rp#139 "verb: Remove from the list"). `Perks` holds
`PerkPlacement` structs, and houseCARL refuses by-value removal of modeled elements, naming the by-index route.
- AC s3: a 526-op **dry run** was refused at pre-flight, 105 ops with that reason (R3585 → R3587).
- AC s1: a 346-op dry run was refused, 88 ops (R6256 → R6257).
- FS: s1 L1831, s3 L1819.

*CopyFrom CLAS* (AC s1 R6257, two ops) copied from a CLAS record into an NPC's `Class`. No skill line says CopyFrom
for a class (no `CopyFrom` in the npc skill or recipes). The agent fixed it to `Class = <FormID>` in one step
(R6370-R6372).

**(b)** The strip: not needed (T1). Setting a class: needed, and it worked.

**(c)** 2.2.0 is unchanged here. Value-based removal of a modeled element is still "a later surface"
(`CorpusRulebook.cs:775-781`). By-index Remove works after a read, and FormLink lists (`ActorEffect`,
`Keywords`) remove by value. The "lost ops" in the distillation are a misreading. Both were dry runs and `apply` is
all-or-nothing, so nothing was written and nothing was lost; the cost was one fix-and-rerun. AC consistency also found the
refusal came after the run's own decision (R1453), so it caused nothing.

**(d)** Remove-by-value: **skill-induced → delete** (it goes with the strip rule and the recipes). CopyFrom CLAS:
**non-problem**, because the refusal names the fix. A real perk swap (vanilla perk → Requiem analogue) is a
read-then-remove-by-index job that agents compose unaided. No issue needed.

## T3: ConditionFloat compose recipe

**(a)** The 1.x recipe (armor / ammo `references/housecarl-recipes.md` §E, crafting.md) says to add a
`ConditionFloat` shell, then Set `Conditions[0].Data` with a compose. The cited event, FS s1 (r48) loot lane
L1040, does not use that shape. It is a **dry run with `readback=true` that passed** (L1046: 2 conditions,
`HasKeyword(AD3A3B:Requiem.esp) == 1 OR`, then `HasPerk`). The lane re-ran it to check the OR flag (L1038). It used
the nested one-op form: `Add` with `composes=`, each element's `Data` built by a nested `compose`. A search of all
four FS skill traces finds no refused or failed condition write. The only "refused" hits are the skill text's own
"`Conditions[0].Data.Perk` is refused by design" line, quoted on load.

**(b)** Yes: perk and keyword gates on recipes are real work.

**(c)** The nested compose is the documented `apply` / `create` shape on 2.2.0 (the `compose.sets[].compose`
member in the schema). Whether the 1.x two-op shape still passes would need an apply dry run, which was not run.
It does not matter, since the rebuild ships no recipes.

**(d) Non-problem → nothing.** "FS r48 L1040 failed" in DISTILLATION §3e and the process table is wrong. The cost
was one verification dry run.

## T4: REQ_NULL scan with `plugins=` on an unregistered patch

**(a)** This is the checklist's final scan (rp#114 item 5, rp#53). MC s2 L1561 asked for
`plugins={names:[<own patch>]}, source=<own patch>, types=[LVLI]` with a `REQ_NULL` where-term. FQ s2 and MC s3
made the same call. houseCARL 2.1.1 refused it: "plugins= names nothing the load order carries". The patch sat in
an UNLISTED folder (MC s2 L1564, FQ s2 L1064, MC s3 just after L1448). MC s2 then reported no REQ_NULL (L1607), and FQ
s2 did the same: 2 clear errored-as-pass cases, both skill arm (U12). No skill line put `plugins=` on the patch.
The agents carried over the router's enumerate-by-`plugins=` shape.

**(b)** A scan of what was written is worth keeping: it caught the RB knockdown spell and the FS Apocrypha chest
(HP4). "None may remain" is not: it is the false-fact absolute (HU-F1), and it is what made an errored scan read as
a pass.

**(c) Fixed in 2.2.0.** The changelog has it: `records` over an off-order `source=` file keeps every record of
that file when `plugins=` names its own filename, for a file in a disabled mod or unticked (#1389). Every refusal is
now an MCP error (`isError`). Checked live: the same shape over `HC_Eval_animated-carriages_r23.esp` (disabled mod
`HC_Eval_Scoring`) answered "scan: 104 matches". The UNLISTED folder case (written, MO2 not yet refreshed) is the
exact eval state. It **needs a write test**: write a fresh patch to a new mod folder, do not refresh MO2, then run
the MC s2 L1561 query unchanged. It should answer, not refuse.

**(d) Real houseCARL gap, closed in 2.2.0.** Skill side: delete "none may remain" (with HU-F1), and keep one final
per-type scan of the written plugin.

## T5: truncated or capped reads taken as absence

**(a)** No skill rule. The skills add query volume and absence-driven skips (armor#18 "already consistent, leave
it"). Evidence from U12 (7 claims in 7 runs, 5 skill):
- MC s1n L312-L336: `max_chars=5000` rendered 22 of 44; the four Enchantment FLSTs were in the spill (r37 g3
  not_done/major).
- FQ s3 L275: `limit=60` of 76 hid the DEPRECATED bounty lists (contributory to the failed run r57).
- RB s1-s3 race lanes: reverse-reference heads of 15-40 rows, in load order, so all vanilla, generalised to
  "per-NPC".

**(b)** Yes. A skip or "Requiem has none" claim needs the whole set.

**(c) Still open on 2.2.0** (live, `references=[0A8657:Skyrim.esm]` over FLST/PERK/MGEF/SPEL, `limit=5`):
- Text says "34 matches (showing first 5; raise limit=, page with offset=, or narrow…)".
- Dense says `"total": 34, "capped": true` at the top, which fixes U12's "flag at 97% of the body" point.
- Neither says what the hidden 29 are (types, winning plugins), or that rows come in load-order scan order. The
  sort and `type_counts` appear only in a spill manifest.
- RB's trap was exactly a vanilla-first head.

**(d) Real houseCARL gap → issue** (draft below), plus one capability line in the rebuild's general layer.

## For the spec

**Carry** (≤1 line each, capability-phrased):
- A capped, cut or errored read is not evidence of absence; get the full count or the whole set before claiming
  none or skipping.
- End with one scan of the written plugin for references whose meaning depends on type (REQ_NULL by type), read
  from the file itself.

**Delete:**
- npc#63, #64, #104, #266; the "zero count is an incomplete write" paragraph; perks.md L150-L153.
- Every Remove-by-value and two-op ConditionFloat recipe (all nine `housecarl-recipes.md` files, with N3).
- rp#53 / #114 / #137 / #139 "none may remain / strip every one" (with HU-F1); rp#42 as applied to baked perks
  (handled elsewhere).
- DISTILLATION §3e corrections: T3 "failed" is wrong; T2 "lost 105/526" was one refused batch, re-run.

## Draft houseCARL issues (not filed)

**1. `records`: a capped window should say what it hides and in what order** (T5). Checked: no open or closed
issue covers this (searched "hidden rows", "sort order", "capped window", "limit window").

> **A `records` answer cut by `limit=`, `max_chars=` or a walk budget names how many rows it hid, but not which.**
> On 2.2.0, `references=[0A8657:Skyrim.esm] types=[FLST,PERK,MGEF,SPEL] limit=5` says "34 matches (showing first
> 5…)" and lists five Skyrim.esm FormLists. Nothing says the other 29 include Requiem and Magic Redone records, or
> that rows come in load-order scan order, so the visible head is always vanilla-first. In a 42-run eval, 7 false
> "none exists" claims came from such windows, 1 of them a lost major change. In 3 of 4 consequential cases, a
> one-line summary would have shown the error.
> Ask: on any cut answer, text and dense/json alike, add one line giving the hidden rows' counts by type and by
> winning (or scoped) plugin, plus the sort order, as the spill manifest already carries (`type_counts`, `sort`).
> Check: the call above prints e.g. `hidden 29: FormList 20, Perk 6, … · by winner: Skyrim.esm 12, Requiem.esp 9, …
> · order: load-order scan`.

**2. Optional, low priority: `where=` `missing` / `exists` folds a present-empty list into missing** (T1 read side).

> On 2.2.0, over `HC_Eval_animated-carriages_r23.esp` (off-order), a fields read shows `Perks = [list: 0 item(s)]`
> beside `ActorEffect = (absent)` on the same records. But `where=["Perks missing"]` matches all 104, and
> `["Perks exists", "Perks[*count] = 0"]` matches 0. The predicate and the render disagree on what present means.
> Ask: make `exists` / `missing` on a list follow the render (present-empty is present), or state in the
> `where=` description that an empty list counts as missing.
