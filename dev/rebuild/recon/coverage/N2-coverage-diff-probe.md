# N2 coverage-diff probe on houseCARL 2.2.0

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (finding). Probed live on houseCARL **2.2.0** (`7f1d8baa`), ARR instance, profile
`ARR Personal Profile` (3,260 active plugins). Subject: The Rot Below (`CJ03Elroy.esp`, 25,987 records) against
ARR's handmade patch `Authoria - Reqtificated - The Rot Below.esp` (202 records). Read-only; scratch files only.*

## Question

`carried-forward.md` N2: a coverage script would flag every record that isn't patched and has no reason against it,
which an agent can't skip. How much of that do houseCARL reads already give?

## Verdict

**Most of it.** houseCARL gives the unpatched set exactly, in one call. It also gives the mechanical reasons a record
needs no patch, in about six calls. About **45% of the unpatched records** in the patchable types get a reason from
reads alone. Another **13%** get one from a short skill line listing the types Requiem takes no input on. The other
**~42%** need a record read and a judgement. That leftover list is exactly what the eval's controls dismissed unread.

The only thing houseCARL doesn't give in one call is **"nothing in the live order references this record"**,
bounded to a set. That takes two calls plus a join. So a coverage script, if we keep one, shrinks to **joining
houseCARL answers into one disposition list**. It reads no record bodies and decides nothing.

## What was run

Patchable types (28): NPC_, RACE, SPEL, MGEF, CONT, WEAP, ARMO, ENCH, COBJ, DOOR, LVLI, LVLN, AMMO, ALCH, PERK, BOOK,
KEYM, MISC, OTFT, SHOU, PROJ, EXPL, CLAS, CSTY, FACT, SCRL, INGR, SLGM. Placed references, cells, navmesh and
dialogue are out of this probe (locks on placed references are a separate question).

| # | Call | Answer |
|---|---|---|
| 1 | `records` on the patch, `to_file` | 202 records: NPC_ 67, RACE 29, SPEL 27, CONT 25, WEAP 23, ENCH 9, … |
| 2 | `records` on the mod, patchable types, `where formid not in @patch` | **249 unpatched**: MGEF 69, ARMO 42, BOOK 29, SPEL 21, LVLI 15, KEYM 12, OTFT 11, … Every NPC_, WEAP, CONT, DOOR, AMMO, COBJ is patched |
| 3 | `records references=@unpatched`, `to_file` | 254 referrers, each naming the targets it hits. Reverse index built in 23 s on first use |
| 4 | Join (script): unpatched minus targets named in 3 | **54 unreferenced** in the live order |
| 5 | `layer formids=@unreferenced` | 1 SkyPatcher line (a UBE armour-addon add, not distribution); SPID, KID, BOS, FLM 0. None revive a record |
| 6 | `decompile_script provider=` + grep | 156 scripts, 0 `GetFormFromFile` / hard-coded lookups. Script properties are already record links |
| 7 | `records types=[ARMO] where MajorFlags has NonPlayable` | 36 NonPlayable (creature skins, NPC-only copies) |
| 8 | `records types=[BOOK]`, field `Teaches` | 22 teach nothing (notes, journals), 3 skill books, 4 spell tomes |

## The partition (249 unpatched)

| Reason | Count | Source |
|---|---|---|
| NonPlayable armour (build rescales it; Heisen 2026-10-31) | 36 | houseCARL flag read |
| Unreferenced in the live order (dead) | 54 | houseCARL references + join |
| Lore book (teaches nothing) | 22 | houseCARL field read |
| **Mechanical, subtotal** | **112 (45%)** | |
| Type with no Requiem input (KEYM, CSTY, FACT, PROJ, EXPL, CLAS) | 33 | a skill line, not a read |
| **Needs a read and a judgement** | **~104 (42%)** | MGEF 45, SPEL 15, LVLI 15, OTFT 6, ARMO 5 (playable rings), SHOU 5, PERK 4, ENCH 4, skill books 3, ALCH 1, RACE 1 |

Spot checks:
- **The unreferenced ring is a deliberate re-point, not a gap.** `CJ03UndeadBlacksmithsRing` is named by a dialogue
  fragment's property in the mod. The patch re-points that property to vanilla `EnchRingSmithing04`, so the live
  order references the ring nowhere. The reverse index reads winners' links, VMAD properties included. That's the
  right answer for "is it live".
- **The 4 unreferenced spell tomes are won by `Synthesis Gameplay.esp`** (generated output). They're also
  unreferenced, so they count as dead. The winner column shows generator wins for free.
- **The rest of the residual is where judgement lives.** The patch took 27 of 48 spells. The other spells and the
  69 MGEFs are mostly NPC-only creature abilities. Telling player-reachable from NPC-only is the MGEF carrier walk,
  which is a read, not a decision.

## Limits and caveats

- **Liveness is measured against the live winner**, so it already includes the patch's own re-points. In a fresh
  job the patch is the agent's new plugin. Liveness should then be read with that plugin in the order (enabled, or
  folded via `source=`), or a re-pointed record shows as live.
- **"Referenced by nothing" has no bounded one-call predicate.** `references=["!X"]` means "doesn't reference X".
  Only the unbounded orphan sweep answers "nothing references it", and it covers the whole order. A bounded form
  (formids= / plugins= ∩ orphan) would drop the join. Candidate houseCARL request, not filed.
- **Flag predicates are per type.** `MajorFlags has NonPlayable` over a mixed-type set errors, because flag names
  are type-specific. One call per type (ARMO, WEAP).
- Placed references (locks, ownership) and dialogue are outside this probe. Runtime layers and scripts are covered by
  N3–N5 (`N3-N5-housecarl-2.2.0-recheck.md`).
- One subject, one patch. The partition shares will differ on an armour pack (more NonPlayable / AR 0 calls) or a
  quest mod (more dialogue).
- A `fields` read with `format=dense` and a small `max_chars` spilled to houseCARL's install folder (houseCARL#1290,
  known).

## For the spec

- **Keep a coverage step; it can be thin.** "Every record of the patchable types is either patched, has a
  mechanical reason, or is on the decision list" is a capability houseCARL answers. The router states the rule and
  the reasons. The only hard requirement is that the residual list is read record by record.
- **Script or no script.** A script's job would be the join plus the counts: unpatched minus reasons gives the
  residual, rendered as a disposition table. That's about 40 lines, reads no record bodies, and decides nothing. If
  houseCARL ships a bounded unreferenced predicate, the join goes away and a script buys only the guarantee that the
  residual is printed in full. Decide in the spec session (N2 topic) against that.
- **Mechanical reasons to name in the skill** (capability-phrased, no call recipes): NonPlayable; dead in the live
  order; generator-owned; lore-only book; runtime-layer or script reach (from N3–N5).
- **Skill-knowledge reason:** the short list of types Requiem takes no input on.
- **Run it as reconciliation,** after the patch is written and in the order, so re-points count.
