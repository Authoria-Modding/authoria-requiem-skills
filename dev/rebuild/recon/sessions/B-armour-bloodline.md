# Recon B session: armour — Bloodline

*Author: Aaron (+ Claude session) · 2026-11-19*

*Class: ARCHIVE (frozen once Aaron checks it).*

Mined from the transcript by a fresh-context agent. Every claim below is traceable to the transcript; where this log
infers, it says so. "No reason given" means Aaron gave none.

## Context

- **Mod:** Amsedillir - BloodLine - 3BA UBE (Nexus 184582, v1.0.0, FOMOD 3BA + UBE). Two ESL plugins:
  `Amsedillir-BloodLine.esp` (243 records) and `Amsedillir-BloodLine UBE patch.esp` (110 records). 9 pieces × 6
  colourways = 54 light ARMO, 108 ARMA, 109 COBJ, 20 TXST, 1 MISC (a recipe book). BodySlide projects for 3BA and UBE,
  SMP physics on three pieces, an inert Material Swapper Framework config.
- **Date:** 2026-11-18, about 18:00–22:16 (active work 18:00–19:54).
- **Project and profile:** run in the `arr-personal` project, task folder `tasks/bloodline-armor/` (TASK.md,
  `build/`), ledger in arr-personal's `LOG.md`. **MO2 profile used: `ARR Personal Profile`**: every houseCARL read
  reports `profile 'ARR Personal Profile'`, and the shell reads are of that profile's `modlist.txt` / `plugins.txt`. The
  list profile was not used.
- **Skills state:** no Requiem skills loaded. houseCARL MCP 2.2.0 connected. No skill of any kind was loaded during the
  session (the houseCARL `kid-authoring` skill was available and not loaded before the KID line was written). The
  Outfit Studio 6.1.0 MCP was added mid-session (D12).
- **Protocol deviations** (they change how B2 reads):
  - Personal playthrough, personal profile, personal task folder; no `arr-release` task, no `CHANGES.md` ledger line.
    The patch carries the personal ` AL Custom` naming, not list naming.
  - Aaron's opening front-loaded instructions: check for errors first; work out whether it needs BodySlide built;
    "plan where it should go in the load order so that the patch we make is either pre-reqtificator or post
    reqtificator", with the hint that the answer "depends on where other armour mods of this kind sit". So D3 and D5
    are **pre-supplied questions**: they show Aaron knew to ask, not whether Claude would have.
  - Claude read Aaron's earlier personal task `auri-replacer` (the Sherwood Huntress patch) at its second step. That
    file carried the house pattern (an `Authoria - Reqtificated - … AL Custom` ESL patch, the `AuthoriaCC_ExoticArmour`
    KID line, the RFTI-exclusion keyword, the apply-ops syntax). Several house conventions below came from that
    precedent, not from Claude's own knowledge (D5, D23, D24). The arr-personal `CLAUDE.md` was also in context
    (inferred from Claude citing its naming rule); this log did not see its text.
  - The opening asked for no Requiem recommendation list; the Requiem calls (tier, stats, recipes) came late, after a
    long mesh and slot phase.
- **What it produced** (state at session end):
  - New mod `houseCARL - Authoria - Reqtificated - BloodLine AL Custom`, **enabled** by Aaron (MO2 priority 2), holding
    `Authoria - Reqtificated - BloodLine AL Custom.esp` (ESL, override-only, 198 records: 54 ARMO, 36 ARMA, 108 COBJ;
    sorted by Aaron at plugin 3003, before RFTI at 3207), `BloodLine AL Custom_KID.ini`, and the BodySlide project
    files for 6 re-slotted variants.
  - Built meshes (16 NIF + 8 TRI per body) in `Authoria - Bodyslide Output - 3BA AL Custom` and `… UBE AL Custom`.
  - Aaron sorted the mod's own plugins into the armour block (496) and the UBE-patch block (1049).
  - Verified in houseCARL: patch wins 198 / 198, 0 dangling refs or missing masters, 109 / 109 walked asset files
    present, KID reaches 18 LIGHT + 36 CLOTHING armours. **Not checked in game.** Nothing committed.

## What it shows

**B1, recurring calls.**
- Where the patch sits relative to the Reqtificator, and so whether to patch by hand (D5).
- Which Requiem tier, and the per-piece stats from it (D20, D21).
- Which pieces count as armour; what happens to cosmetic pieces (AR, type, keywords, weight) (D14, D17, D22).
- Recipe gating: perk, materials, the mod's own gates (book), tempering (D23, D24).
- Crafting-menu routing via KID (D25), and the RFTI exclusion keyword (D26).
- Slot conflicts with the rest of the order, and re-slotting (D9, D18).
- Merge or keep multi-piece sets (D10, D11, D15–D17).
- Whether BodySlide must build, into which output mod, with which preset (D3, D19).

**B2, what Aaron had to supply.**
- **No tempering on AR-0 pieces** (D24). Claude kept temper recipes for six 0-armour pieces; Aaron corrected it.
  Claude then found Requiem's own disabling method (`REQ_DisableRecipe`) by reading Requiem, unprompted.
- **The UBE revealing-slot issue** (D8). Aaron named it ("UBE … changes cuirass slots depending on if the armour is
  revealing the crotch"); Claude had not checked slots against UBE at all. Once pointed, Claude derived the convention
  from the list correctly and found the shipped setup right.
- **Slot conflicts as a check** (D9): only looked at because Aaron asked.
- **Piece-count / merge preference** (D10–D17): Aaron's taste, iterated four times and ending in "no merging, strip
  the extras of armour". The 0-AR-head rule and spreading the head's share over body / hands / feet were Aaron's (D14).
- **Tooling Aaron supplied:** that an Outfit Studio MCP exists and is installed (D11); that restarting the app would
  load it (D12); where the BodySlide project files should live (D28).
- **Pre-supplied by the opening, so not evidence of a gap:** error check first, the BodySlide question, the
  pre/post-Reqtificator question (D3, D5).
- **Aaron's preference, not knowledge:** tier "higher than Elven", then Ancient Falmer (D20); keep 6 colourways (D13);
  Coat/Ribbon either-or (D16); move the clashing pieces (D18).

**B3, did the dissection catch what matters?**
- **Caught:** plugin health; no distribution (crafting only); unbuilt meshes (16 projects) and the right output mods;
  Material Swapper config inert and PBR absent; male model is a placeholder; slots for every piece; the book gate
  is trivial; the list pattern for 3BA + UBE armour patches (D2–D7). The first report was broad and accurate.
- **Missed until Aaron asked:** UBE slot convention and slot clashes with survival / cloak / lantern gear (D8, D9);
  that cosmetic pieces should not temper (D24).
- **Missed or not done, found by this log:** the temper recipes Claude rewrote drop the `EPTemperingItemIsEnchanted`
  OR-condition that the originals and the list comparable carry (D23; confirmed in the ops script, effect not checked
  in game). Claude also chose the Trousers slot (57) itself and dropped the book gate without an answer from Aaron
  (D18, D23). Self-caught: a wrong keyword FormID (`ClothingBody` used as `ArmorClothing`), fixed before enabling (D22).
- **What a "patch this mod" job actually involved:** most of the session was not Requiem work. Of ~2 hours, about
  1h20 went on slots, merging, Outfit Studio and BodySlide; the Requiem patch itself took about 20 minutes (D19–D26).

**B4, house conventions that came up.**
- Hand patch `Authoria - Reqtificated - <Mod>` ESL, loaded before RFTI, no Reqtificator rerun; forwards the UBE
  patch's armatures (D5, accepted by Aaron by sorting it there).
- The mod's main esp in the armour block, its UBE patch in the UBE-patch block (D6, Aaron sorted).
- 3BA / UBE meshes built into the `Authoria - Bodyslide Output - … AL Custom` mods (D3, D19).
- `AuthoriaCC_ExoticArmour` KID line for the forge menu (D25); RFTI exclusion keyword on every piece (D26).
- Personal ` AL Custom` suffix on new mods and files (D7, D19).
- Disable a recipe with `REQ_DisableRecipe` (D24, derived from Requiem, approved by Aaron's ask).
- Aaron's call, possibly a house rule for cosmetic armour pieces: 0 AR, no tempering, head share spread (D14, D17, D24).
  Whether this is a general rule or one-off taste was not stated.

**houseCARL navigation, with no skills** (full audit in [houseCARL tool use](#housecarl-tool-use)):
- Good overall: right tool nearly every time, correct FormIDs throughout, a safe write lane (dry run, new patch,
  `into=`, off-order read-back, enable step, re-verify). 4 errors, all the agent's own, each fixed in under 15 s.
- What a skill must teach: read comparables below the Reqtificator layer (it read RFI, D21); look up FormID constants
  before writing (D22); scope "nothing uses X" claims to what was queried (it generalised from 5 of 54 armours); ask
  before any consent-gated in-place write; settle "tell Aaron to sort a pre-RFTI patch" against the never-sort rule.
- Seven candidate houseCARL gaps (G1–G7), none checked against the tracker yet.

## Decision log

### D1: Where does the work live, and on which profile?

- **Records:** whole mod
- **Options:** list profile + `arr-release` task / personal profile + `arr-personal` task
- **Claude recommended:** `ARR Personal Profile`, new task `arr-personal/tasks/bloodline-armor`, because Aaron's
  opening said "for my personal playthrough"
- **Aaron chose:** the same (implicit; his opening set it)
- **Claude missed:** nothing
- **Kind:** other

### D2: Is the mod clean enough to work on?

- **Records:** both BloodLine plugins
- **Options:** clean / needs fixes first
- **Claude recommended:** clean: `housecarl_check` errors + scripts found 0 dangling refs, 0 missing masters, 0
  scripts; no cells, refs, NPCs or leveled lists; only conflict is the UBE patch over its own 54 ARMO; textures all
  shipped and winning. Noted `ksws03_quest.esp` already fails to parse (unrelated)
- **Aaron chose:** proceed (implicit), because no reason given
- **Claude missed:** nothing (Aaron pre-supplied the "check first" step)
- **Kind:** coverage

### D3: Does it need BodySlide built, and where do the meshes go?

- **Records:** all ARMA (54 base + 54 UBE)
- **Options:** ships pre-built / build in BodySlide; output into the shared outputs / the `AL Custom` outputs
- **Claude recommended:** build: only the Cap ships pre-built, the other 8 pieces × 2 bodies are absent (asset walk);
  3BA group into `Authoria - Bodyslide Output - 3BA AL Custom`, UBE into `… UBE AL Custom` (Sherwood precedent)
- **Aaron chose:** accepted; Claude later built them itself (D19)
- **Claude missed:** nothing (question pre-supplied by Aaron's opening)
- **Kind:** coverage

### D4: Does it need Material Swapper Framework or PGPatcher?

- **Records:** `SKSE/Plugins/MaterialSwapperFramework/…` config; PBR note on the Nexus page
- **Options:** install MSF / PGPatcher / skip
- **Claude recommended:** skip: the MSF DLL is not in the order so its config is inert, each colourway is already its
  own ARMO + ARMA; no PBR package installed, so PGPatcher has nothing to do
- **Aaron chose:** no comment; skipped
- **Claude missed:** nothing
- **Kind:** coverage

### D5: Pre- or post-Reqtificator, by hand or by rerun?

- **Records:** whole mod
- **Options:** pre-RFTI hand patch, no rerun / post-RFTI patch / include in a Reqtificator rerun
- **Claude recommended:** pre-RFTI hand patch, no rerun, because the list's 3BA + UBE armours (Hedge Knight, Abyss,
  Zamorian Thief, Lastriem, Rogue Stalker) each have an `Authoria - Reqtificated - <Mod>.esp` in `Authoria - Requiem
  Patches` before RFTI that forwards the UBE armatures, carries the RFTI exclusion and wins all its records (Hedge
  Knight 11 / 11); Sherwood AL Custom did the same without a rerun
- **Aaron chose:** the same (sorted the finished patch to 3003, before RFTI 3207); no reason given
- **Claude missed:** nothing; Aaron pre-supplied the question and the hint to look at comparable armours. The Sherwood
  task notes Claude read at boot already held this pattern
- **Kind:** stance (upstream / bake) + house convention

### D6: Where do the mod's own two plugins sort?

- **Records:** `Amsedillir-BloodLine.esp`, `Amsedillir-BloodLine UBE patch.esp`
- **Options:** leave at the end (after RFTI) / main esp in the armour block, UBE patch in the UBE-patch block
- **Claude recommended:** move them into their blocks (~415–493 and ~1022–1047), from the comparables; said leaving
  them after RFTI is harmless because RFTI does not include them
- **Aaron chose:** sorted them himself to 496 and 1049
- **Claude missed:** nothing. Observation: Claude told Aaron to sort plugins, which the workspace router forbids for
  ARR ("never tell Aaron to sort"). Aaron did not react; that rule may not apply to his personal profile
- **Kind:** house convention

### D7: Rename the mod folder to the personal naming?

- **Records:** mod folder `Amsedillir - BloodLine - 3BA UBE`
- **Options:** rename to `… AL Custom` and move below the 3BA output / leave as installed
- **Claude recommended:** rename (citing the naming rule) and move below the 3BA AL Custom output
- **Aaron chose:** never answered; the folder kept its name. For the patch mod, Claude suggested dropping the
  `houseCARL - ` prefix; Aaron kept it (no reason given)
- **Claude missed:** nothing
- **Kind:** house convention

### D8: Are the UBE torso slots right for a revealing armour?

- **Records:** `000835:Amsedillir-BloodLine UBE patch.esp` (0_A7dlr_BloodLine_Torso_UBE) and the other UBE ARMA
- **Options:** as shipped (32 + 53) / change to 32 only / add TNG revealing keywords
- **Claude recommended:** as shipped. Read the list: UBE naked torso = 32 34 35 36 38 53; slot 52 = underwear / TNG;
  in `Authoria - UBE Master Patch`, 400 covering cuirasses use 32 without 53 and 251 revealing ones use 32 + 53, as
  does every armour UBE patch. BloodLine's UBE torso mesh carries the UBE body with partitions 32 + 53 and its ARMA is
  32 + 53, the revealing kind. No list armour uses `TNG_Revealing`, so nothing to add
- **Aaron chose:** accepted (moved on); no reason given
- **Claude missed:** **Aaron supplied the question.** Claude's first pass did not compare slots against UBE's convention
  at all; it only listed slot overlaps inside the mod. Once pointed, the derivation was Claude's own and correct
- **Kind:** coverage

### D9: Do any pieces clash with other gear in the order?

- **Records:** Trousers (slot 46), Coat and Ribbon (49), Cap and Barrette (42), Cape (34)
- **Options:** report / ignore
- **Claude recommended:** report: Trousers 46 clash with 234 cloak items (Wet and Cold, Campfire, Frostfall, FurSet,
  BlanketScarf); Coat / Ribbon 49 with 58 items (SunHelm waterskins, wearable lanterns, a Haberdashery item); Cap /
  Barrette exclude each other; Cape 34 hides the UBE skin's forearms when worn without the torso
- **Aaron chose:** acted on it later (D18)
- **Claude missed:** Aaron prompted the check ("check slot conflicts"); the first report had listed only the
  in-mod overlaps and that 46 is "often used by cloak mods"
- **Kind:** coverage

### D10: Too many pieces: merge into vanilla slots?

- **Records:** all 54 ARMO
- **Options:** keep 9 pieces / merge to 4 (Cuirass = Torso + Trousers + Cape + Coat or Ribbon; Gloves; Boots; Head);
  route A records-only (extra ARMA under the Torso ARMO) / route B Outfit Studio merge
- **Claude recommended:** the 4-piece merge; flagged route A as unverified (would the engine draw a mesh whose
  partition is not on its ARMA) and route B as sure but more work. Confirmed no jewellery or earrings in the set
- **Aaron chose:** wanted fewer pieces ("it has too many pieces in my opinion"); route chosen in D11
- **Claude missed:** nothing; the merge wish is Aaron's taste
- **Kind:** other

### D11: How to merge, and what stays out of the body?

- **Records:** all ARMO / meshes
- **Options:** route A / route B; Cape in or out of the body; follow list precedent
- **Claude recommended:** after Aaron's steer, searched the list for multi-piece merges: found Asura's Guard (combined
  by its author, Heisen only converted it to UBE): everything in the body except head, hands, feet. Twilight Princess,
  FVO Cloth and Armors of the Velothi were left multi-piece. Could not find a merge Heisen made himself
- **Aaron chose:** Outfit Studio, Cape kept separate, model on Heisen's merges; then "maybe he didn't merge any … your
  plan is solid"
- **Claude missed:** **Aaron supplied** that Outfit Studio has a new MCP and that it is installed in the instance.
  Aaron's belief that Heisen had merged sets turned out unsupported by what Claude found
- **Kind:** tooling

### D12: Connect the Outfit Studio MCP

- **Records:** none (Claude config)
- **Options:** register now / ask first; new session / restart the app
- **Claude recommended:** said it would register only with Aaron's OK; after Aaron said "I added the argument and am
  booting outfit studio", registered `outfit-studio` (local config, arr-personal only). Tools did not load mid-session;
  Claude proposed a new session
- **Aaron chose:** "I could just quit and reload the claude app"; that worked
- **Claude missed:** that an app restart would do (Aaron's simpler route). Reading Aaron's message as consent to the
  config change is an inference Claude made; Aaron did not object
- **Kind:** tooling

### D13: Keep all 6 colourways?

- **Records:** 54 ARMO (9 × 6)
- **Options:** keep all 6 / fewer
- **Claude recommended:** asked, no recommendation
- **Aaron chose:** keep all 6; no reason given
- **Claude missed:** nothing
- **Kind:** other

### D14: Head pieces: which, and do they carry armour?

- **Records:** Cap and Barrette ARMO (12)
- **Options:** Cap / Barrette / both; AR as shipped / AR 0
- **Claude recommended:** rendered both in Outfit Studio for Aaron to choose
- **Aaron chose:** both stay, exclusive, **no armour value**; "the extra armour that the head normally provides should
  be divided between the other pieces like body feet and hands"
- **Claude missed:** nothing (preference). Claude turned it into numbers: Requiem's split body 1 : hands 0.3 : feet 0.3
  : head 0.4, spread pro rata = body ×1.25, hands / feet ×0.375 of the tier cuirass. The ratio matches the Ancient
  Falmer set read later (250 / 75 / 75 / 100)
- **Kind:** value

### D15: Coat: merged or optional, and on which slot?

- **Records:** Coat ARMO / ARMA
- **Options:** merge into body / optional extra; stay on 49 / move to a spare slot
- **Claude recommended:** after Aaron's call, slot 58 for the optional Coat (only Dismemberment Framework parts, OCum
  and a few arm accessories use it); listed 48, 55, 57, 59, 60 as busier
- **Aaron chose:** "The wing things I don't think should be merged, we should make them an extra piece so they are
  optional." Claude read "wing things" as the Coat's side panels; Aaron did not correct that
- **Claude missed:** nothing
- **Kind:** other

### D16: Coat and Ribbon: one piece, or either-or?

- **Records:** Coat and Ribbon ARMO, ARMA, meshes
- **Options:** merge Ribbon into body / drop it / merge Coat + Ribbon into one piece / keep either-or
- **Claude recommended:** first asked body-or-drop; after Aaron proposed merging the two, rendered them together and
  showed the back straps double. When Aaron asked if they were meant to be either-or, Claude confirmed from evidence:
  same slot 49 in ARMO, ARMA and mesh partition; the Ribbon hangs off the Coat's own physics bones
- **Aaron chose:** "keep them either-or like the author intended"
- **Claude missed:** nothing; here Claude's evidence corrected Aaron's idea
- **Kind:** other

### D17: Merge anything at all?

- **Records:** all ARMO / meshes
- **Options:** Body = Torso + Trousers merged in Outfit Studio / no merging, strip extras of armour
- **Claude recommended:** the Torso + Trousers merge (as the then-agreed plan)
- **Aaron chose:** "don't merge them into the body. It seems like this outfit shouldn't be merged, rather we should
  just strip the extra pieces of armour value." Only Torso, Gloves, Boots carry AR. (Sent one second after Claude's
  message, so probably typed before reading it.)
- **Claude missed:** nothing (preference); it reversed ~1 hour of merge planning
- **Kind:** value

### D18: Leave the slot clashes, or re-slot the pieces?

- **Records:** Trousers ARMO + 12 ARMA; Coat / Ribbon ARMO + 24 ARMA; their meshes
- **Options:** leave / move Trousers and Coat / Ribbon to spare slots (record change + mesh partition edit)
- **Claude recommended:** offered both, noted 58 as the best spare
- **Aaron chose:** "Move them"
- **Claude missed:** nothing supplied by Aaron. **Claude then picked slot 57 for the Trousers itself, without asking**,
  rejecting 59 (HDT softbody breast item), 54 (UBE hide-underwear), 44 (Wet and Cold). Slot 57 is shared with
  pauldrons, a Serana neck corset, the Magecore choker and the Falmer Slayer belt (its own read); Aaron was told
  afterwards and did not object
- **Kind:** coverage

### D19: How to make the re-slotted meshes, and how to build

- **Records:** BodySlide projects `[A7dlr]_BloodLine_3BA.osp` / `_UBE.osp`
- **Options:** edit the source projects / derived variants; build by Aaron in BodySlide / headless via the MCP; preset
- **Claude recommended:** 6 Outfit Studio variants (`create_derived_project`, kind variant) with only the piece shape's
  partition changed (collision and placeholder shapes left on 32), new output names `…_ALC` so they cannot clash with
  the source outputs; test-built to scratch and checked partitions with `nif_inspect`; then built all 8 sets per body
  headless into the AL Custom outputs with the zeroed presets and TRI morphs (inference: zeroed + TRI suits OBody
  morphing, the transcript gives no reason)
- **Aaron chose:** no objection; the earlier plan had Aaron building, Claude did it
- **Claude missed:** that Outfit Studio launched through MO2 saves new project files into MO2 overwrite (D28). A
  group file Claude wrote outside the VFS was not visible to BodySlide, so it built by outfit names
- **Kind:** tooling

### D20: Which Requiem tier?

- **Records:** Torso, Gloves, Boots ARMO (18)
- **Options:** first offered Elven / keep Scale; then Glass (275) / Ancient Falmer (250) / Dragonscale (300)
- **Claude recommended:** no pick; noted Ancient Falmer has no Requiem forge recipe to copy (quest gear), so materials
  would be borrowed
- **Aaron chose:** "something higher than elven", then Ancient Falmer; no reason given
- **Claude missed:** nothing
- **Kind:** value

### D21: Core-piece stats and keywords

- **Records:** Torso, Gloves, Boots ARMO (18)
- **Options:** derived from the tier comparable
- **Claude recommended:** from Requiem's Ancient Falmer set (read live, winner RFTI): Torso AR 313 (250 × 1.25), weight
  10, value 2500; Gloves / Boots AR 94 (≈ 250 × 0.375), weight 3, value 750. Keywords: ArmorLight, part keyword,
  VendorItemArmor, `REQ_ArmorSet_AncientFalmer`, `Survival_ArmorCold`, `REQ_Tempering_ElvenSmithing`, RFTI exclusion;
  `REQ_Armor_Resistance_Ranged_Tier3` on the Torso. Weight and value copied unscaled (the head's share went to AR only)
- **Aaron chose:** accepted; no comment
- **Claude missed:** nothing Aaron flagged. Its comparable was read from the winner, `Requiem for the Indifferent.esp`
  (generated output), not `Requiem.esp` (see houseCARL tool use §3). Re-read 2026-11-19: `Requiem.esp` holds the same
  AR on all three pieces (100 / 75 / 250), so the numbers are right; the source was wrong
- **Kind:** value

### D22: What are the cosmetic pieces, record-wise?

- **Records:** Trousers, Cape, Coat, Ribbon, Cap, Barrette ARMO (36)
- **Options:** light armour with AR 0 / clothing; weight; keywords
- **Claude recommended:** ArmorType Clothing, AR 0, weight 0.5, value as shipped; keywords ArmorClothing,
  VendorItemClothing, RFTI exclusion, plus ClothingHead on Cap / Barrette. No source cited for 0.5 or for making them
  Clothing
- **Aaron chose:** no comment
- **Claude missed:** self-caught bug: the first write used `0A8657:Skyrim.esm` (ClothingBody) as "ArmorClothing";
  Claude caught it on read-back and re-applied 36 keyword ops with `06BBE8` before Aaron enabled the patch
- **Kind:** value

### D23: Forge and temper recipes

- **Records:** 54 forge + 54 temper COBJ; book recipe `00046F:Amsedillir-BloodLine.esp`
- **Options:** keep the mod's gates (book + Advanced Light Armors) / tier perk only; materials; keep the book
- **Claude recommended:** gate every recipe on `REQ_Smithing_ElvenSmithing` only (the Ancient Falmer tempering
  perk); materials Torso 4 moonstone + 2 malachite + 3 strips, Gloves / Boots 2 + 1 + 2, cosmetic 1 leather + 2 strips;
  temper 1 moonstone (core) / 1 strip; book gate dropped, book recipe left as shipped. Materials are borrowed
  (moonstone from Elven, malachite from Glass, by Claude's own account) since no Requiem AF forge recipe exists
- **Aaron chose:** the book question ("keep the book requirement?") was asked twice and never answered; Claude
  dropped it on its own. No comment on materials
- **Claude missed:** found by this log, **confirmed in the ops script** (`Conditions` `ReplaceAll` with one HasPerk
  condition): the `EPTemperingItemIsEnchanted` OR-condition that the originals and the list comparable (Snow Elven
  Arsenal patch) carry is gone from the 18 core-piece tempers (the 36 cosmetic ones are disabled anyway, D24).
  Inference: an enchanted piece may now temper without the enchanted-item perk gate. Not raised in the session, not
  checked in game
- **Kind:** value

### D24: Should 0-armour pieces be temperable?

- **Records:** 36 temper COBJ of the cosmetic pieces
- **Options:** keep / delete / disable
- **Claude recommended:** originally kept them (1 strip each)
- **Aaron chose:** "there should not be tempering recipes for armour pieces we stripped of armour rating". Claude
  disabled them the Requiem way: read Requiem's `REQ_NULL_…` recipes, found they move to workbench keyword
  `REQ_DisableRecipe` (AD3B01), and did the same for the 36
- **Claude missed:** **Aaron supplied the rule.** The disabling method was Claude's own find
- **Kind:** house convention

### D25: Route the set into the forge menu with KID

- **Records:** 54 ARMO (runtime keyword)
- **Options:** KID line / leave in generic forge sections
- **Claude recommended:** `AuthoriaCC_ExoticArmour|Armor|Amsedillir-BloodLine.esp|LIGHT` and `|CLOTHING`, in the patch
  mod, matching the list's crafting-categories KID file and the Sherwood precedent. Verified reach with houseCARL (18
  LIGHT + 36 CLOTHING). Flagged that clothing pieces carry no material keyword and may sit loose under `$Exotic Armour`
- **Aaron chose:** asked "what is the KID file you made doing?", then accepted the explanation
- **Claude missed:** nothing; but it wrote the line without loading the `kid-authoring` skill
- **Kind:** house convention

### D26: RFTI exclusion keyword on every piece

- **Records:** 54 ARMO
- **Options:** add `AD3B2B:Requiem.esp` / leave RFTI to rescale
- **Claude recommended:** add it to all 54, as the list's Reqtificated armour patches and Sherwood do
- **Aaron chose:** no comment
- **Claude missed:** nothing Aaron flagged. Note: split hunt 10 found this keyword load-bearing only below the rescale
  threshold, habit elsewhere; here it rode the precedent, not a derivation
- **Kind:** house convention

### D27: ESL and patch packaging

- **Records:** the patch plugin
- **Options:** leave as written / compact in place
- **Claude recommended:** compact in place (override-only, nothing renumbered), check the ESL flag survived each later
  apply by reading the header bytes
- **Aaron chose:** no comment
- **Claude missed:** nothing
- **Kind:** tooling

### D28: Where do the BodySlide project files live?

- **Records:** 2 `.osp`, 6 ShapeData NIFs, 1 group XML
- **Options:** new `Amsedillir - BloodLine - BodySlide Projects AL Custom` mod / Aaron moves them / the patch mod
- **Claude recommended:** a new mod, Claude to move them
- **Aaron chose:** first "I am confused why there are files in overwrite, that makes no sense"; after Claude's
  explanation (MO2 VFS sends new files to overwrite), "move them into houseCARL - Authoria - Reqtificated - BloodLine AL
  Custom"
- **Claude missed:** did not warn up front that saves would land in overwrite, or plan a home for them
- **Kind:** tooling

### D29: Getting textures to show in Outfit Studio renders

- **Records:** none (Outfit Studio setting)
- **Options:** add the mod folder as an extra data folder / launch Outfit Studio from BodySlide
- **Claude recommended:** added the mod folder, removed it again at the end
- **Aaron chose:** suggested launching from BodySlide might avoid it; Claude said it could not tell
- **Claude missed:** unresolved
- **Kind:** tooling

### D30: Male model placeholder

- **Records:** all base ARMA (male model = vanilla Blades armour)
- **Options:** accept / give men a real mesh / hide
- **Claude recommended:** asked ("Is the men's placeholder fine?")
- **Aaron chose:** never answered; left as shipped
- **Claude missed:** nothing
- **Kind:** coverage

## houseCARL tool use

*Session: Amsedillir BloodLine (3BA + UBE) setup, 2026-11-18, no Requiem skills loaded. houseCARL server 2.2.0. 89 houseCARL calls of 270 total. TOOL# numbers are the transcript's call numbers.*

**Verdict (5 lines)**
1. Navigation was good with no skills: it chose the right tool almost every time (check, conflicts_only, delta, tree, references, asset walk, nif partitions, the `kid reaches` predicate) and used the `XXXXXX:Plugin.esp` form correctly in every call.
2. Writes followed the safe lane: a dry run (#223), a NEW patch (#224), `into=` for both extensions (#235, #247), off-order read-backs (#229, #230, #232), and a post-enable verify (#252–#259). It told Aaron to enable the mod.
3. 3 hard errors and 1 soft error, all its own mistakes, each fixed in 5–14 s, usually by doing what the error message said (#48, #51, #191, #257).
4. Main misuses: it took the Ancient Falmer reference stats from the **RFTI winner** (generated output) rather than `Requiem.esp` (#213). It passed the in-place compaction consent gate itself (#228). Twice it made a whole-set claim from a partial query (#50, #53). It read the ESL flag from raw plugin bytes twice (#238, #248).
5. Efficiency was middling: several over-broad dense dumps, a one-call-per-slot census, and mixed-type field lists that buried results in "not on <type>" notes (#15, #230).

### 1. Inventory

| Tool | Calls | Used for |
|---|---|---|
| `records` | 65 | Health and contents (#11, #12, #14, #15, #18, #19, #23, #39, #40); comparables: Hedge Knight patch, UBE patches, UBE master patch, Asura's Guard, Haberdashery, Twilight Princess, FVO (#27–#28, #41–#44, #49, #52, #54, #55, #73, #75–#78, #81); TNG / revealing keywords (#46–#48, #50); references to the armour (#51, #53); slot census (#56–#59, #132–#138, #155–#159); book recipe (#60, #61); tier reference (#213–#215); a to_file dump that fed op generation (#217); read-backs (#230–#232); REQ_DisableRecipe lookup (#243–#245); live verify (#253, #255, #256, #258) |
| `load_order_status` | 5 | The two BloodLine plugins (#7, #8), a comparable patch (#26), the new patch off-order (#236) and after enabling (#252) |
| `asset_status` | 5 | Shipped meshes (#20), asset walk before the build (#21), built-mesh census (#237), asset walk after enabling (#257 error, #259) |
| `nif_inspect` | 4 | UBE ShapeData partitions (#45); partitions of the re-slotted built meshes (#169, #191 soft error, #193) |
| `apply` | 4 | Dry run (#223), new patch (#224), keyword fix (#235), disabling the temper recipes (#247) |
| `check` | 3 | Source plugins errors + scripts (#9), the patch off-order (#229), all three after enabling (#254) |
| `skse` | 2 | Material Swapper inventory (#10) and config audit (#13) |
| `compact_plugin` | 1 | Set the ESL flag on the new patch, in place (#228) |

Tools loaded through ToolSearch (#5, #216, #225, #242). `remove` was loaded but never used: it disabled the recipes rather than deleting them (#247). `create_plugin` and `forward` were loaded and not needed. `housecarl_layer` and the Nexus tools were never loaded.

### 2. Right tool for the job?

| Case | What it did | Should have been | Severity |
|---|---|---|---|
| ESL flag after a write | Python `struct` read of the plugin header bytes (#238, #248) | `load_order_status` once the patch is active (#252 shows `ESL flag YES`). Off-order it showed nothing (#236), so this is partly a tool gap (§7) | Medium: breaks "never regex over bytes" |
| Load-order positions | grep of `plugins.txt` (#6, #24, #25, #251) | No houseCARL output seen here gives a plugin's index, so Bash was the only route (§7). Allowed under ARR's "read the live instance" rule | Low |
| Plugin set for a scan | grep of `plugins.txt` into a list, passed as `plugins.names=@file` (#74 → #75, #76) | Works. A name-prefix filter would remove the step (inference: none seen in the schema) | Low |
| Distribution claim | Said "no SPID/KID/SkyPatcher files" from the mod's own file listing (#3); never called `housecarl_layer` | `housecarl_layer` (other mods' lines can target the plugin) or a `kid reaches`-style predicate | Medium (scope not stated) |
| Spill files | grep/python over the JSONL spill files (#22, #194, #218, #246) | Sanctioned: the spill manifest invites own-tool reads | OK |
| `.osp` / BodySlide XML | grep (#17, #71, #72, #79, #80, #260) | Outside houseCARL; the Outfit Studio MCP covers it | OK |
| KID line | Wrote `_KID.ini` by hand (#227); no `kid-authoring` skill load | Load the bundled `housecarl:kid-authoring` first (inference: available in that session). The `kid reaches` verify (#255, #256) did confirm 18 + 36 | Low |

It never fell back to Bash for record content: every record question went through `records`.

### 3. Correct use and misreads

**Good:** `conflicts_only` (#12) to prove the only overrides were the UBE patch's own; `delta` with `source`/`versus` (#39); `tree` for an override stack (#27, #43); `[*count]` once it hit a 24-row race list (#18 → #19); `fields_source="winner"` where it mattered (#44, #73, #217); `source=` reads of the off-order patch (#230, #232, which confirms the T4 fix in 2.2.0); `to_file=` and re-entry by `@file` (#217, #258 → #259); `resolve_names` to catch its own wrong FormID (#230).

**Wrong layer read:** #213 read `REQ_Light_SnowElf_*` with the default winner source, and every row came `from Requiem for the Indifferent.esp`. Torso AR 313 = 250 × 1.25, and the core-piece keyword set (including `Survival_ArmorCold`) were taken from that generated layer, not from `Requiem.esp` (`source="Requiem.esp"` or a `tree`). A `tree` re-read on 2026-11-19 showed `Requiem.esp` holds the same AR on all three (100 / 75 / 250), so the numbers came out right by luck of the layer, but the server rule is "never build on generated output". A skill must cover this, because the default winner read hides it.

**Misreads and over-claims:**

| # | Claim to Aaron | What the result supports |
|---|---|---|
| M1 | "no list armour uses `TNG_Revealing`" (after #50) | #50 checked only `TheNewGentleman.esp`'s two FormIDs. #46 had listed two more `TNG_Revealing` keywords (Magecore, HDT SMP Object Simple) and two `SOS_Revealing`, never queried. Over-claim (whether TNG reads them is inference) |
| M2 | "The only things that reference the armour are its own 109 recipes" | #53 asked about 5 FormIDs (4 armours + the book) out of 54 armours. It generalised from a sample, which is the same class as the A6 T5 trap |
| M3 | "no SPID/KID/SkyPatcher files" | Only the mod folder's listing was checked (#3); no layer read (see §2) |
| M4 | "RFTI doesn't include them" (BloodLine sitting after RFTI) | No houseCARL read checked RFTI's masters or overrides (from #24/#25 grep only). Unverified |
| M5 | `ArmorClothing = 0A8657:Skyrim.esm` (in its own op generator) | A constant from memory, never resolved. #230 showed it as `ClothingBody`; it was fixed via #231 → #235. Not a result misread, but a write-time constant never looked up |

Interpretation was otherwise accurate: the slot bit maths (`has_any 268435456` = slot 58, and so on) and the 18 + 36 KID reach, 198 winners and 109 present assets all match the results (#253, #255, #256, #259).

### 4. Errors and recovery

| # | Error | Cause | Recovery |
|---|---|---|---|
| #48 | `has_any` on a list (`Keywords`) | Agent: flag operator on a list | 8 s: #50 used `references=`, as the error suggested |
| #51 | `where=` with `references=` and no `types=`/`plugins=` refused as unbounded | Agent | 6 s: #53 dropped `where` (adding `types=` would have kept the filter) |
| #191 | `under=` with a drive-rooted glob returned 0 meshes, only a note | Agent, plus a tool gap (`under` is Data-relative only; no on-disk glob) | 14 s: listed the files in Bash (#192), then used `paths=` (#193) |
| #257 | `@file` artifact refused: epoch changed after Aaron enabled the mod | Agent reused a stale artifact; the refusal is correct by design | 5 s: re-materialised with `to_file` (#258), then #259 |

By cause: 4 agent mistakes (one also exposes a tool gap), 0 environment, 0 tool bugs. The excluded `ksws03_quest.esp` (an unparseable record) was reported in the first message as unrelated, which is right, and it did not distract the session.

### 5. Efficiency

- **Over-broad dumps:** #76 (602 matches, 80 dense rows, about 1,500 transcript lines, to look for merged sets); #23 (54 ARMA rows of mesh paths, which the #21 walk already covered); #54 and #55 (about 450 lines each); #155–#158 (about 1,900 lines to choose a spare slot); #59.
- **One call per slot:** #132–#137, then #155–#159. Two rounds totalling 11 calls, where a slot histogram would have taken one (§7). #156 and #157 re-asked slots 59 and 57 already counted in #136 and #134.
- **Mixed-type field lists:** #15 (MISC + COBJ, cut off at 7 of 15 rows) and #230 (ARMO + ARMA + COBJ, 11 "not on <type>" notes, and the recipe rows truncated, so it needed #232).
- **Redundant:** #244 repeats #243's scan (same filter, grouped by type instead of winner); #7 and #8 could have been one call (inference: `filter` may take only one value).
- **Unused:** #42 and #52 gave context only. Most results did feed a claim.
- **Efficient:** the `to_file` dump in #217 drove offline op generation, giving 594 ops in one apply. `counts_only` in #237, #254, #255 and #256.

### 6. Writes

| # | Call | Lane | Result |
|---|---|---|---|
| #223 | `apply` dry run | new patch | 594 ops validated; masters previewed |
| #224 | `apply patch="Authoria - Reqtificated - BloodLine AL Custom"` | **new plugin** in new mod `houseCARL - …` | 594 edits on 198 records (54 ARMO, 36 ARMA, 108 COBJ); lean masters Skyrim, Update, UBE_AllRace, Requiem and both BloodLine plugins |
| #228 | `compact_plugin in_place=true acknowledge=true` | **in place** on the just-written, not-yet-enabled patch | ESL set, nothing renumbered (override-only) |
| #235 | `apply into=` | extend own patch | 36 keyword ReplaceAll (the M5 fix) |
| #247 | `apply into=` | extend own patch | 36 temper COBJ moved to `REQ_DisableRecipe` (AD3B01, read in #245) |

- **New-plugin default kept:** no source plugin was edited in place.
- **Consent gate:** #228 set `acknowledge=true` without asking Aaron. The risk was low, because the target was houseCARL's own new file and off-order. But the server calls in-place writes consent-gated, and the agent decided this itself. Nothing in the session explains why a new patch needs an in-place pass to get ESL (§7).
- **Read-back:** after #224 it ran `check` (#229) and field reads (#230, #232) on the off-order file, which caught M5. After #247 it read only the raw ESL byte (#248), with no field read-back of WorkbenchKeyword until the post-enable count of winners (#253).
- **Enable step:** told to Aaron in the 19:35 message, with the patch mod and the ESL kept; verified after he enabled it (#252: active, ESL, 6 masters). It also told him to sort the patch before RFTI. That is functionally needed for a pre-RFTI patch, but it conflicts with the ARR rule "never tell Aaron to sort". A skill should settle that tension.
- **Outside houseCARL:** the KID ini (#227) and the BodySlide project files (#264) went into the houseCARL mod folder by hand.

### 7. Gaps

**Candidate houseCARL issues** (none checked against the issue tracker; "likely known" is inference):

| Gap | Evidence | Note |
|---|---|---|
| G1: `apply` (and `into=`) results don't report the header flags (ESL) or whether they survived | #235 and #247 say nothing about ESL, so it read bytes (#238, #248) | New candidate |
| G2: `load_order_status` says nothing about an off-order on-disk plugin's header | #236: "not in the load order", with no header, though `records`/`check` read the same file off-order | Fits the T4 off-order work; possibly known |
| G3: No way to write a new patch as ESL; that took an in-place `compact_plugin` behind a consent gate | #224 → #228 | Inference: no `esl` option seen in use. Candidate: `esl` on new-patch writes, or no in-place gate for houseCARL's own unregistered output |
| G4: `nif_inspect under=` can't glob an on-disk folder outside Data (a build temp dir) | #191 | Small. The note was clear, but the call returned 0 rows, not an error |
| G5: No slot-occupancy histogram (aggregate by BodyTemplate bit) | #132–#137, #155–#159 | Candidate "group_by slot" |
| G6: No load-order index in `load_order_status` | #24, #25, #251 grep `plugins.txt` for positions | Possibly by design (reads the files) |
| G7: A long `fields` read over mixed types floods "not on <type>" notes | #15, #230 | Polish: one summary line |

**houseCARL could have done it, but the agent didn't find it:** `source="Requiem.esp"` or `tree` for pre-Reqtificator comparables (#213); `housecarl_layer` for the distribution claim (M3); `references=` over all 54 armours via a `formids=@file` set (M2); adding `types=` to keep the `where` in #53; the bundled `kid-authoring` and `mutagen-reference` skills (inference that they were available).

### 8. What a skill would need to teach about houseCARL

1. **Read comparables below the Reqtificator layer.** A default winner read of a Requiem record often comes from `Requiem for the Indifferent.esp`. Derive stats and keywords with `source="Requiem.esp"` (or `tree`), and say which layer every number came from (#213).
2. **Resolve every FormID constant by EditorID before writing** (one `records` KYWD call), and read back with `resolve_names` (M5: #230 caught it only because the read-back resolved names).
3. **Scope absence claims to what was queried.** `references=` over the full set (`formids=@file`), every same-EDID keyword plugin, and `housecarl_layer` for runtime layers, before "nothing references / distributes / uses X" (M1–M3; the same family as T5).
4. **The write lane, end to end:** dry run → new patch → `into=` for later edits → off-order `check` + `source=` read-back → tell Aaron to enable → re-verify against the new epoch (re-materialise any `@file` artifacts, #257). Ask Aaron before any `acknowledge=true` (#228). How ESL gets set, and how to confirm it without reading bytes.
5. **Query hygiene:** one record type per `fields` read; `[*count]` for big lists; `counts_only`/`aggregate` before `dense`; slot bits (`1 << (slot − 30)`); `has_any` is for flags only, and lists take `[*any]` or `references=`; `where=` needs `types=`/`plugins=`/`formids=` to bound the scan.
6. **Pre- vs post-RFTI placement** (a load-order fact houseCARL shows only partly) and how to tell Aaron about it under the ARR "never tell Aaron to sort" rule.

## Open ends

- Nothing checked in game: stats (313 / 94 / 94, others 0), cloak or lantern worn with Trousers or Coat / Ribbon,
  SMP physics on Coat, Ribbon, Barrette, both bodies, forge menu placement and tempering.
- The 18 core-piece temper recipes lost the `EPTemperingItemIsEnchanted` OR-condition (D23): confirmed in the ops
  script, a live defect in the personal patch until fixed; in-game effect not checked.
- Trousers on slot 57 was Claude's own pick (D18); it shares 57 with pauldrons, a neck corset, a choker and a belt.
- Book gate dropped without Aaron's answer; the book recipe still exists and now does nothing (D23).
- Clothing pieces have no material keyword; their forge-menu subsection is unverified (D25).
- The UBE Trousers' first-person model points at the 3BA mesh (as shipped; Claude noted and left it).
- Male placeholder unanswered (D30). Mod-folder rename never done (D7).
- Whether "cosmetic pieces get 0 AR, no tempering, head share spread over the core three" is a house rule or a
  one-off for this set was not stated (D14, D17, D24).
- arr-personal `TASK.md` / `LOG.md` changes were not committed (the app offered no commit).
