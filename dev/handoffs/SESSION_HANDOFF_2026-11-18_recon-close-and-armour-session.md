# Session handoff — 2026-11-18 (2): recon leftovers closed, armour session done

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (frozen at close). Project: `dev/rebuild/`. Supersedes
`SESSION_HANDOFF_2026-11-18_housecarl-2.2-unblocked.md` as the latest handoff.*

## Where it stands

**Stage: recon, last input in progress.** Everything in recon that needed no input from Aaron landed today (PRs
#61–#64). The **armour patching session (B1–B4, first of two) is done.** Aaron ran it himself on the **Bloodline**
mod. Its transcript hasn't been mined yet; that's the next job.

## Landed today

| PR | What | Where |
|---|---|---|
| #61 | **A6:** the five eval tool traps root-caused on houseCARL 2.2.0. T1/T2 came from our own rules (delete them); T3 is no problem; T4 was a houseCARL gap, now closed; T5 is still a gap (issue drafted, not filed). **N2:** houseCARL reads give the unpatched set in one call and a mechanical reason for ~45% of it; a coverage script would only join the answers | `recon/tools/A6-tool-traps.md`, `recon/coverage/N2-coverage-diff-probe.md` |
| #62 | **Census merge** with a dominance field (91 of 178 conventions matched; 16 `house` conventions rest on one plugin, mostly Bruma). **Suspected-bugs recheck:** 28 confirmed, filed in arr-release `BUGS.md` (entry dated 2026-11-18) | `recon/census/merged.md`, `conventions.merged.json`, `recon/suspected-bugs-recheck-2026-11-18.md` |
| #63 | **A8 / A9 live pass:** one repo installs on Claude Code and Codex with the existing `.claude-plugin/` manifests; both hosts name skills `plugin:skill`. On a real task GPT made two stance errors: it treated a handmade patch as generated, and took RfI's baked damage as the target. Docs recheck: ~29 of 46 claims confirmed, 6 changed | `recon/hosts/A8-A9-live-pass.md`, `A8-A9-docs-recheck.md` |
| #64 | **B1–B4 protocol.** Goal: a correct patch, Aaron working as normal. Let the agent go first on each call. Don't tell it it's a test, and don't have it keep a log. A fresh agent mines the transcript afterwards. Also recorded: the rebuild runs **alongside** `authoria-design` `aspects/requiem-patching/` wave 2, with the build-boundary facts kept in one swappable place | `recon/sessions/README.md`, `decisions.md` 2026-11-18, `carried-forward.md` X1/X2 |

State left behind:
- The 1.x pack is **uninstalled** on both hosts. The GitHub marketplace entries are still registered, with nothing
  installed.
- The `claude` CLI login has expired, which blocks headless trigger runs. Aaron re-logs (`claude`, then `/login`)
  when the trigger evals run.
- CLAUDE.md step 0 is still accurate (no install).

## Next (pick up here)

1. **Mine the armour session.**
   - Source: Claude Code session `fbf096a4-8517-4109-9b56-9deb948d4d0c`, opened in `Projects/arr-personal`
     (2026-11-18, ~14 MB). The transcript lives in the Claude projects folder for arr-personal under `<home>`.
   - Use a **fresh-context subagent.** It reads the whole transcript and writes
     `recon/sessions/B-armour-bloodline.md` in the README's entry format. At the top: recurring calls, what Aaron
     had to supply, what the dissection caught or missed, and house conventions decided.
   - Aaron checks it. No local paths or private transcript pastes go in the public doc; the raw transcript stays
     local.
2. **Note the context gap.** The session ran in **arr-personal**, for Aaron's **personal playthrough**: its opening
   line says so, and the profile was presumably his personal one, not the list profile the protocol asked for. It
   still serves B1–B4, since Aaron's judgement calls are the data. But:
   - **don't log it in arr-release**: personal work is never list work (Documents/Claude CLAUDE.md);
   - say in the mined doc which profile it used. Whether the Bloodline patch also becomes list work is Aaron's call.
3. **Quest session** (the second B session): same protocol, Aaron's pick of mod.
4. **Then the spec session.** Open with the N1–N5 topics in `carried-forward.md` (write-gate hook, coverage script,
   scripts / assets / runtime layers) and X1 / X2. Then go through the 16 single-plugin `house` conventions from
   `merged.md`.

## Lessons

- **The latest handoff can miss sibling-repo work.** The 2026-11-17 authoria-design requiem-patching study (Heisen's
  Reqtificator study and the replace-the-Reqtificator hypothesis) wasn't in the previous handoff. Check
  `authoria-design` `aspects/requiem-patching/` and `authoria-domain-knowledge` when orienting.
- **Codex CLI ships inside the Codex desktop app** (`%LOCALAPPDATA%/OpenAI/Codex/bin/<hash>/codex.exe`), not on PATH.
  `config.toml`'s model `gpt-5.5` is refused for a ChatGPT-account login, so pass `-m gpt-6-luna`.
- **Don't merge subagent verdicts unread.** Three confirmed rows were re-read live before filing (MG3, MG4, W1); a
  confirmed C1 turned out INTENDED on reading the row.
