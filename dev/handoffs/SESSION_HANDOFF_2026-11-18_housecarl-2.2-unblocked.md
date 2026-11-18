# Session handoff — 2026-11-18 houseCARL 2.2.0 unblocks the rebuild

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (frozen at close). Project: `dev/rebuild/`. Supersedes
`SESSION_HANDOFF_2026-10-31_calls-and-codex.md` as the latest handoff.*

> **For the next session: re-orient Aaron first.** About three weeks passed since the last real work (2026-10-31),
> spent waiting for houseCARL. Aaron has said he can't remember the details. Open with the plain-words picture
> below, then the stage and next steps. Explain from the ground up, without IDs, and say what each choice means.
> Don't start work until he has the picture back.

## The project in plain words

- **What:** rebuild the `authoria-requiem` skill pack. Its 11 skills help Claude patch new Skyrim mods to fit
  Requiem for the ARR list, by comparing against Requiem's own records through houseCARL.
- **Why a rebuild:** a 42-run control eval (October) showed the 1.x skills still beat a bare model on 5 of 6 jobs,
  but:
  - they cost about 4× as much;
  - about 86% of their 12,660 lines did nothing;
  - five of their "facts" are false;
  - they teach the wrong stance for ARR;
  - they don't support how Aaron actually patches: understand the whole mod first, agree the judgement calls,
    then execute.
- **Target:** about 1,500 lines, mostly one agent, keeping the measured wins:
  - the coverage procedure: list everything, read each record, decide, reconcile;
  - the facts about where the Reqtificator stops;
  - the domain comparison methods;
  - the house values.

  Everything else goes. It must work in Claude Code **and** OpenAI Codex, and ship as an installable release.
- **Method:** staged project: intent → recon → spec → plan → build. Aaron agrees each stage before the next starts.
  Router: [`../rebuild/INDEX.md`](../rebuild/INDEX.md). Every decision so far: [`../rebuild/decisions.md`](../rebuild/decisions.md).

## Where it stands

- **Stage: recon (research), nearly done.** Intent agreed 2026-10-30. Recon done so far:
  - **The control eval and its distillation:** what helped, what hurt and what was dead weight, per skill
    (`eval-2026-10/distillation/`).
  - **A census of ARR's 250 handmade Requiem patches,** with 14 deep dives (the "split hunts") into where they
    disagree. This is the evidence for the house conventions (`recon/census/`, `recon/splits/`).
  - **Heisen's answers** to the questions the records couldn't settle, recorded 2026-10-31. Key rulings:
    - Requiem and its addons are the reference first;
    - NPC doctrine;
    - each split's fate.
  - **Anthropic's skill-authoring guidance** (A1–A5) and the install / hooks question (A7).
  - **A desk pass on Codex support and distribution** (A8 / A9).
  - **Scripts, assets and runtime layers** (N3–N5): first on houseCARL 2.1.2, re-checked on 2.2.0 today.
- **Aaron's calls on 2026-10-31,** in `decisions.md`:
  - new skills are graded against the spec, not against 1.x;
  - there's no frozen checklist metric;
  - no separate validation run;
  - build the router first;
  - trigger evals load the real houseCARL;
  - Ancient Falmer arrows are about 100;
  - Codex is a target, the pack ships as a release, and each skill gets a review against both vendors' docs.

## What happened since 2026-10-31

1. **2026-10-31:** the first live test of houseCARL's asset tools on The Rot Below turned up gaps: no SPID / KID
   reader, one-at-a-time decompile, and others. houseCARL redesigned its whole asset and runtime layer as its own
   project, and Aaron ruled that **this project waits for it**. Holds were set on graded runs and on Aaron's own
   patching sessions (B1–B4).
2. **2026-11-18:** houseCARL **2.2.0** was released and installed. It ships the whole redesign. The live recheck
   ([`recon/coverage/N3-N5-housecarl-2.2.0-recheck.md`](../rebuild/recon/coverage/N3-N5-housecarl-2.2.0-recheck.md))
   showed the job now takes five calls with no shell step:
   - every script decompiled in one call;
   - one call lists which SkyPatcher, SPID, KID, BOS and FLM lines name a mod's records;
   - one call lists the files a mod ships that nothing uses.

   **The holds are met** (`decisions.md`, 2026-11-18). PR #59.
3. Leftover houseCARL items don't block us:
   - the notice repeated on every answer (#1288);
   - no elapsed time (#1289);
   - spill cleanup (#1290);
   - verbose `links=` (#1291);
   - the whole-mod walk still takes about 4 min on ARR, and its 2,000-node default cuts it short.

## Things that changed around the project (check before relying on old docs)

- **The repo moved** to the `Authoria-Modding` GitHub org (`Authoria-Modding/authoria-requiem-skills`). Old
  `Avick3110/…` links redirect.
- **Team repos opened 2026-11-14:**
  - `arr-dev` was renamed `authoria-domain-knowledge` (knowledge only);
  - plans and list decisions now live in `authoria-design`;
  - how the team works lives in `authoria-handbook`.

  This repo's live docs don't name `arr-dev`. Heisen answered the questions doc on 2026-10-31 and has the final say
  in `authoria-design`. The intent's line that "Heisen is out of action, so Aaron holds every gate" may be stale:
  ask Aaron.
- **MO2's selected profile is `ARR Personal Profile`,** not `arr-skill-eval-profile`. Graded or eval runs need the
  eval profile selected (Aaron's step), or must say which profile they read.
- **houseCARL's own skills now hold framework knowledge only,** and tool descriptions say how to call. That's a
  design input for how our skills refer to houseCARL. Parameters were renamed (`paths=`; `housecarl_layer`); none of
  our live docs use the old names.
- **Still no live install of our pack** (CLAUDE.md step 0). The missing `~/.claude/skills/authoria-requiem` is on
  purpose.

## Next (pick up here)

1. **Re-orient Aaron** (above). Point him at `INDEX.md`, `intent.md` "Proposed outcome", and `decisions.md`.
2. **Remaining recon that needs no input:**
   - **N2:** the coverage-diff probe. How much of "every record not patched, with no reason against it" do houseCARL
     reads already give? Now easier with 2.2.0's `@file` / `exclude=`.
   - **A6:** root-cause the five tool traps from the eval. Recheck them against 2.2.0, since some may be gone.
   - Merge the census `conventions.json` files, with a dominance field.
   - Re-verify `recon/suspected-bugs.md`, then file the confirmed ones in `arr-release/BUGS.md`. Add the Rot Below
     leads: 9 human NPCs with no FaceGen, and two attached scripts nothing ships.
3. **A8 / A9 live pass:** check the docs live, do a fresh install on each host, and a Codex / GPT smoke test.
4. **B1–B4: Aaron's own patching sessions** (an armour mod and a quest mod) with decision logs. They're now
   unblocked, and they need Aaron.
5. **Then the spec session.** Open with the hook and coverage-script topics (`carried-forward.md` N1–N5); spec
   against 2.2.0's real calls. Open spec questions: does grading also use a GPT model, and mocks for full graded
   runs.

## Lessons

- **Tool calls sent in one message can run at the same time.** A `date` stamp beside a call doesn't time it. Time a
  call with stamps in separate messages.
- **Project output goes in the project's folder** (Aaron, 2026-11-04). A doc for another project's agent goes in
  that project or here, not in the Claude Output vault.
- **The auto-mode classifier still needs an explicit merge go.** "Merge when green" works. GitHub auto-merge is off
  for this repo, so wait on `gh pr checks --watch`, then `gh pr merge --rebase`.
- **On Windows, `git worktree remove` fails while the shell sits in the folder.** Unregister, then delete the folder
  from another cwd.
