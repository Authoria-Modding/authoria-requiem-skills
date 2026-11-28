# Recon B session: quest — Amorous Adventures (multi-session)

*Author: Aaron (+ Claude session) · 2026-11-27*

*Class: ARCHIVE (frozen once Aaron checks it).*

> [!important] Aaron's correction, 2026-11-28 (supersedes parts of the Verdict below)
> The body below is the miners' evidence and stands. Two of its conclusions don't match what Aaron saw while
> driving the job:
> - **Conflicts weren't the gap.** The agents found the FDE-style conflicts well on their own. The one system Aaron
>   had to point at was **OStim Solutions**, which isn't a quest mod, so it sat outside the frame the agents were
>   working in. That's a scope blind spot, not missing knowledge. The re-derivation cost below is real but not
>   decisive.
> - **Sizing the job was the decisive input.** Without Aaron saying "this is big, split it", a single session would
>   have tried to do it all and missed most of the nuance. That's knowing how AI agents behave, not Skyrim knowledge.
> - **Recall isn't the bottleneck.** Agents prefer the live list (houseCARL, the MO2 profile), and that's the right
>   instinct. What matters is a human with list knowledge pointing them at the right places in it.
>
> The working conclusions live in the handbook note
> `authoria-handbook/Research/2026-11-28-working-with-ai-on-the-list.md`.

This is the second B session and the test of the 2026-11-22 hypothesis: **a capable agent needs recallable domain
knowledge, not skills that teach a task** (`../../decisions.md`). It is synthesised from nine fresh-context miners,
each reading one slice of the transcripts. Their per-slice findings stay local, with the job, in Aaron's personal
task folder; this doc cites them by slice letter (A–H). The adult content is kept clinical: mechanics only.

## Context

- **Job:** a personal fix patch for the OStim port of *Amorous Adventures* (AA) and its six companion plugins. The
  target was Aaron's own ARR playthrough (`ARR Personal Profile`, task folder in `arr-personal`). It ran 2026-11-26
  20:54 to 2026-11-27 ~20:15.
- **Shape:** 18 sessions, which spawned 45 subagents of their own. The phases were:
  - analysis (with an 18-agent audit-and-verify wave);
  - an NPC template pass and OStim Solutions research;
  - 10 storyline passes run one at a time with Aaron;
  - a cross-storyline review;
  - Aaron's audit choices;
  - a 5-stage build;
  - an independent audit.
- **Skills:** none loaded (the 1.x pack is uninstalled). houseCARL 2.2.x was loaded. A `papyrus-reference` skill
  pointer in one brief was never used.
- **Scale:** 1,770 houseCARL calls across 14 tools: 1,377 `records`, 125 `decompile_script`, 102 `check`, 22
  `compile_script`, 21 `apply`, 15 `forward`, and smaller counts. 164 calls failed, counting all tools.
- **Mining method:** the raw transcripts were ~60 MB. They were split into two tiers:
  - a narrative tier (~5.3 MB: every human and agent message whole, tool output trimmed, errors whole);
  - a full tier for exact lookups (every houseCARL result whole).

  Mechanical houseCARL counts were made by script. Each miner classified Aaron's input as **knowledge / taste / tool
  habit / method**, and was told to be strict about method, since it is the hypothesis's weak point.
- **Attribution caveat:**
  - Most sessions were started by the orchestrating agent, so each one's opening "user" turn is an
    agent-written brief, not Aaron. Those briefs are counted as carried state.
  - Aaron's own words appear mainly in the analysis thread (A) and as answers to questions in the storyline passes.

## Verdict

**The hypothesis holds for domain method, and it is refined by the result:**

1. **Domain method was never needed.** No agent was taught how to patch a quest mod. They derived every mechanic
   that mattered from records and scripts: stage gates, alias fills, kill paths, package order and cross-mod
   romance clashes. They also found real bugs that the build then fixed.
2. **Orchestration method was needed, and Aaron supplied it.** It came to ~22 method interventions, concentrated in
   the analysis thread. None of it is Skyrim-specific: it is how to run a long job across many agent sessions. It
   belongs in a general workflow doc, not in a Requiem skill pack.
3. **Domain knowledge gaps were few (~12 items) but costly.** The two worst false findings of the job both came from
   a missing fact. A library would also cut the **re-derivation cost**: each storyline's list-side dossier spent
   ~330–380k subagent tokens re-reading what every other mod does to the same NPCs.
4. **Recall is the open risk.** No agent opened SecondBrain or `authoria-domain-knowledge` unprompted. They read only
   the docs their brief pointed at, and nothing learned was filed back. A library works only if the router and the
   briefs point into it.

So the deliverable splits three ways:
- **(a)** a recallable domain-knowledge library, which includes list-side facts per mod and per NPC;
- **(b)** a general long-job orchestration method, which belongs with Aaron's workflow (e.g. the `new-project` skill
  or SecondBrain), not here;
- **(c)** houseCARL fixes and habits.

The quest test leaves no place for task skills.

## Aaron's input, all slices

Counts are Aaron's own typed or relayed input. B1 and B2 (subagent waves) contain no Aaron, so they are excluded.

| Slice | Sessions | Taste | Knowledge | Method | Tool habit |
|---|---|---|---|---|---|
| A | analysis, main thread | ~7 | 5 | ~10 | 1 |
| C | NPC template, OStim doorway, Solitude | 10 | 2 | 4 | 0 |
| D | Whiterun, Riverwood, Companions | 10 | 1 | 2 (weak) | 0 |
| E | Annekke/Sylgja/Senna, Riften, orc strongholds | 7 | 0 | 0 | 0 |
| F | College, Morthal, cross-review | 5 | 0 | 0 | 0 |
| G | lover layer, audit choices, build 2–5 | ~32 | 2 | 3 (+2 relayed) | 1 |
| H | build 1, independent audit | 1–2 | 2 | 3 | 0 |
| **Total** | 16 sessions | **~72** | **~12** | **~22** | **2** |

- **Taste dominates.** In the storyline passes Aaron mostly clicked the agent's recommended option. Sessions E and F
  gave nothing but taste.
- **Method** is concentrated in A. It covered:
  - read every record and script, and simulate each NPC;
  - one storyline per session, in sequence, not parallel;
  - a human file plus a separate build spec;
  - traceable decision IDs;
  - "the deciding session writes its own spec";
  - audit each mod in isolation with subagents that write files, plus a verify pass ("Opus has a tendency not to
    completely dissect everything");
  - split when the context gets heavy;
  - re-check what the patch wins after a re-sort.

  In the storyline passes the method items were verification nudges:
  - "Was there a reason you didn't check… Stormcloaks";
  - read both mods' dialogue before deciding, which reversed the agent's Illia recommendation;
  - flag downstream masters before disabling a plugin.
- **The agents designed most of the artefacts:** the handoff, the per-NPC 4-step method, the spec row schema,
  decision IDs, `RECORDS.md`, the audit brief, the cross-storyline review, the staged build, the independent audit,
  and file checks in place of play testing. Aaron designed the shape they sit in (A).

## Knowledge gaps (the library's first entries)

| Gap | Effect | Would-be doc |
|---|---|---|
| The decompiler drops trailing default arguments at call sites; the compiler fills them | False "8 vs 9 args" finding on 66 calls; the proposed "recompile Util to 8 params" would have *created* the bug. Raised twice, passed between subagents by message, caught by a verify pass reading raw bytecode (B1, B2) | Papyrus: call-site defaults and decompiler lossiness |
| OStim's superload blacklist matches action tags as well as types | A wrong finding marked "verified", then discarded by verify (B1) | OStim: scene selection and blacklist |
| houseCARL plugin writes re-encode untouched cp1252 text as UTF-8 | 3 INFOs damaged; the builder dismissed the warning as "pre-existing"; the independent audit proved otherwise (AUD-02; G, H) | houseCARL: string encoding on override |
| An Optional quest alias does not make the scene actor optional | Audit finding AUD-03 (H) | Quests: aliases vs scene actors |
| What `CompleteQuest` / stage 200 does to downstream start gates | Agents hesitated; derived it for Dead Bride's Curse → Needles & Threads (G) | Quests: completion semantics |
| A late-sorted patch's CELL headers overwrite Lux lighting | Aaron's "lighting and such?" (H) | ARR: Lux and cell-header ownership |
| FDE's own romances never start scenes | Aaron supplied it (G) | Mod: FDE romance mechanics |
| Running the Reqtificator (procedure) | Aaron pointed at the ARR wiki; neither repo holds it (A) | ARR: Reqtificator run procedure |
| NPC refusals Aaron saw in play | Unresolved; the search covered 5 plugins, then 2, never the whole order (C) | Open |

**Re-derivation cost.** Each storyline pass ran an AA-side and a list-side dossier subagent. The list-side one
re-derived from scratch what FDE, IDE, Vigilant, RedBag, Housecarls and others do to the storyline's NPCs. One
dossier took 88 tool calls, ~380k tokens and 8 minutes, and E and F measured ~330–370k each (D, E). A per-mod
knowledge doc, or a per-NPC "who touches this NPC" record, is the direct saving.

## What the agents derived on their own

Highlights only; the full lists are in the slice files.
- **Analysis:**
  - PDR leaving `Util` unbound on 24 quests;
  - a stale `.seq` master index;
  - the Vampire Fix lost twice;
  - 441/441 sequence scenes resolving;
  - the SDA hub patch read from its archive (A).
- **The audit wave:**
  - a 4,305-record PDR diff;
  - Sanguinare re-running `VampireChange` on a vampire player, via Requiem/RCS;
  - a stray `.fuz` shown to be a different clip by BSA extract, decode and cross-correlation;
  - the linen soft-lock;
  - homemade `.pex` and ESP parsers (B1, B2).
- **The storylines:**
  - Essential vs Unmasking Sybille;
  - Grand Solitude's temple rebuild;
  - the Loaded Bear scene stall;
  - RedBag moving Sylgja's house;
  - FDE Mjoll's rival romance;
  - Cursed Tribe's second ending;
  - VC01 stage 197 killing Falion;
  - Mirabelle disabled, not killed, at MG07 50;
  - the lover-layer gating model from a 955-script bytecode sweep (C–G).
- **The cross-review:**
  - replaced an earlier `SetStage(60)` stall fix with `SetStage(200)`, because 60 skips alive gates;
  - disproved an audit verdict on Serana;
  - trimmed yielded NPCs from FIX-8 (F).

## What went wrong (method and verification, not knowledge)

- **Over-claims from partial queries** recur, as in the armour session:
  - "Solutions never refuses";
  - "Saadia's ending unreachable" (self-corrected);
  - "152 referencers, all delivery" read off a page showing 40;
  - a claimed `references=` sweep that no call ran;
  - "ksws03 touches nothing", carried unchecked, though houseCARL can't parse that plugin;
  - a `references` query scoped to three types that understated ROSTER without saying so (A, C, D, G).
- **Deferrals resolved without Aaron.** He deferred D-STD-08, D-STD-12 and D-ELI-1 to in-game checks. The build
  left the first two at safe defaults and resolved D-ELI-1 from files, recording each in its logs but not asking
  (G; confirmed in the build handoff).
- **Cross-session drift:**
  - two death scripts were written in sequential sessions (fixed by the review);
  - an AppData notes folder was invisible to the main session;
  - the canonical spec was swapped mid-session (C, D, F).
- **What only the independent audit caught:** four Sybille yield-script interactions, a one-shot latch against
  Essential aliases re-filled at quest start, and `Stop()` skipping the cleanup stage. The review checked spec
  rows, not runtime paths, and the build ran "from spec only" (F, H).
- **Possible uncaught errors** for Aaron's patch (not verified here):
  - the parent imposed an audit verdict ("`0C0079` still starts DLC1_1") that a present-state read contradicts (B2);
  - the Senna verdict contradicts its own dossier's stage-56 travel package (E);
  - Morthal's start line has no civil-war exile gate (inference, F).

## houseCARL on quest content

- **Navigation was strong with no skills.** Every error was a query-shape or schema slip, each fixed on the next call
  from the tool's own message: field names, operator syntax, `Position` vs `Placement`, double quantifiers. The
  build used dry runs, off-order read-backs, a decompile-and-diff of every `.pex`, and live re-checks after enable
  (H).
- **Generated output:** RFI and the HPH Patcher output were read only as runtime state (Essential/Protected flags),
  never copied. One early near-miss proposed forwarding DynDOLOD/Occlusion values; it was superseded before the
  build (A).
- **Candidate issues** (none filed; check the tracker first):

| # | Gap | Evidence |
|---|---|---|
| Q1 | `decompile_script` hides trailing default arguments at call sites, with a misleading note; no raw argument view | B1, B2, A; draft issue already in the task folder |
| Q2 | Plugin writes re-encode untouched cp1252 strings as UTF-8; the dialogue check's non-ASCII warning is character-based, so it can't tell original from re-encoded bytes | G, H (AUD-02) |
| Q3 | A bitmask filter on `MajorRecordFlagsRaw` fails: the value reads back negative (`-2147482624`) | C (two sessions, two workarounds) |
| Q4 | `ksws03_quest.esp` fails to parse, so claims about it can't be verified | D, E |
| Q5 | `source={file}` direct-path read failed on an out-of-order SDA plugin | A |
| Q6 | No "find every caller of a function" search across scripts; no n-way per-path diff | B1, G |
| Q7 | A scoped query that understates its set gives no hint that it's partial | A |
| Q8 | Out of reach: OStim native code, Papyrus VM coercion rules, audio identity | B1, B2 |

## How the work passed between sessions

- **State carriers, agent-designed:** `ANALYSIS.md`, `ROSTER.md`, per-storyline `npcs/` (human) and `spec/`
  (build) files, `spec/DECISIONS.md` with IDs, `RECORDS.md`, the audit README, per-stage build logs and dated
  handoffs. The parent session wrote a detailed boot brief and read list for every child.
- **Templates propagated:** each storyline copied the previous pass's files as its format. The Sybille file
  became the "depth template".
- **What got lost:**
  - The decompiler fact proven by one subagent never reached a sibling four minutes later. There was no shared
    "tool pitfalls" channel, and subagent messages spread the wrong claim instead (B1).
  - Notes in an AppData folder were invisible (D).
  - Concurrent edits to `DECISIONS.md` may have clashed (unproven, A).

## Recall

- **Never opened unprompted:** SecondBrain, `authoria-domain-knowledge`, the `papyrus-reference` skill. A grep finds
  no OStim, AA or decompiler doc in the knowledge repo anyway.
- **Found on their own:** the arr-personal LOG and task history; Aaron's hand-edited RFTI copy, which an agent held
  back a rerun to protect; an earlier session's bytecode parser; Aaron's earlier D-GEN-3.6 decision, which the
  audit used to drop a would-be finding.
- **Found only when pointed:** the ARR wiki (Reqtificator steps) and the earlier `lydia-replacer` task, which turned
  out to be stale.
- **Filed back:** nothing. What the job learned about Papyrus, OStim, quests and FDE sits only in the task folder.

## What this means for the rebuild

1. **Drop task skills.** Neither B session found a place where teaching a Requiem or quest patching procedure would
   have helped.
2. **Build the library around the gaps and the re-derivation cost:**
   - engine and framework facts (Papyrus, quests, OStim, encoding);
   - per-mod mechanics (FDE, IDE, SDA, Solutions…);
   - list-side facts per NPC or per mod (who touches what).

   Recon's census and split hunts are the ARR-convention half of it.
3. **Wire recall in.** The router (`CLAUDE.md`) and every agent brief must point at the library's index. Unprompted
   lookup didn't happen once in 18 sessions. Filing back must be a step: the job learned a lot and kept none of it.
4. **Put the orchestration method somewhere general.** That's Aaron's process: session splits, human file plus
   spec, decision IDs, audit and verify, independent audit, re-check after re-sort, checks scoped to what was
   queried. It's a long-agent-job method that applies beyond Skyrim.
5. **houseCARL:** triage Q1–Q8 against its tracker. Q1 and Q2 caused real damage or near-damage.
