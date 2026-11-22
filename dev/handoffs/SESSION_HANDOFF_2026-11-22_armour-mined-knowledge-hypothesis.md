# Session handoff — 2026-11-22: armour session mined, domain-knowledge hypothesis

*Author: Aaron (+ Claude session) · 2026-11-22*

*Class: ARCHIVE (frozen at close). Project: `dev/rebuild/`. Supersedes
`SESSION_HANDOFF_2026-11-18_recon-close-and-armour-session.md` as the latest handoff.*

## Where it stands

**Stage: recon, last input pending (the quest session).** The armour session is mined. It raised a hypothesis that may
change the project's premise: **the deliverable may be a public ARR domain-knowledge library, not a skill pack**
(`rebuild/decisions.md` 2026-11-22, recorded as under test, not decided). Spec work waits on the quest session.

## Done this session

- **Mined** `rebuild/recon/sessions/B-armour-bloodline.md`: 30 decisions (D1–D30) plus a `houseCARL tool use` audit
  (89 houseCARL calls, 4 errors, all agent-side; gaps G1–G7). Run on `ARR Personal Profile`, not the list profile.
- **Method that worked:** the raw JSONL was 14.6 MB but mostly payload. A first condensed pass (inputs capped 1,200,
  results 2,500 chars) cut 30 of 65 `records` results and flagged no errors. That is unfit for a tool-use audit. The
  rebuilt pass kept every tool input whole, every houseCARL / Outfit Studio result whole and every error result whole,
  and capped the rest at 5,000 (~760 KB). Two fresh agents ran: one for the decision log, one for the houseCARL
  audit on a houseCARL-only extract (~600 KB). Their claims were spot-checked against the uncut text and live.
- **Verified live:**
  - The Ancient Falmer comparable was read from RFI, but `Requiem.esp` holds the same AR (100 / 75 / 250). The
    numbers are right; the source was wrong.
  - The temper ops `ReplaceAll` the conditions with one HasPerk, which drops the `EPTemperingItemIsEnchanted`
    OR-condition on the 18 core-piece tempers. This is a confirmed defect in Aaron's **personal** patch: fix it in
    arr-personal, not arr-release. The in-game effect was not checked.
- Updated `recon.md` findings index, `recon/sessions/README.md` table, `rebuild/INDEX.md` status.

## Next (pick up here)

1. **Quest session** (Aaron runs it). This time use the list profile and an `arr-release` task, per
   `recon/sessions/README.md`. Run it as a baseline: no skills and no new knowledge docs.
2. **Mine it the same way:**
   - Build a full-fidelity transcript and a houseCARL audit, as described above.
   - Sort every item Aaron supplied into **knowledge / taste / tool habit**.
   - Check the precedent effect: did the agent find and copy earlier task notes or list files? The armour session
     leaned on Aaron's Sherwood task notes (`auri-replacer`).
3. **Then decide the hypothesis.** If it holds, the open questions are:
   - where the library lives (`authoria-domain-knowledge` is private and team-shared; a public repo needs Heisen's
     say);
   - what this repo becomes;
   - which recon outputs (census, split hunts, the Reqtificator rulebook) convert into knowledge docs;
   - how recall gets tested (the knowledge repo has a recall test).
4. **Separate follow-ups, not done:**
   - The candidate houseCARL issues G1–G7 aren't checked against the tracker or filed.
   - The personal-patch temper fix goes in arr-personal.

## Lessons

- **Size before you condense, and audit what the condensing cut.** A cap that keeps a narrative readable can delete
  exactly the evidence a tool-use question needs. Count per tool which results were cut before handing the file on.
- **A subagent's "misuse" finding needs a live check of its consequence.** The RFI-source finding was real, but it
  did no harm here. Record the process flaw and the actual outcome separately.
