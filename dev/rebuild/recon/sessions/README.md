# Recon B1–B4: Aaron's own patching sessions

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: LIVING (until both sessions are logged). Targets B1–B4 in [`../../recon.md`](../../recon.md).*

Aaron patches two real mods for ARR with Claude, the normal interactive way, **with no Requiem skills loaded**:
first an armour mod, then a quest mod. Each session keeps a decision log, which is the evidence for:
- B1, the judgement calls that recur;
- B2, what Aaron had to supply;
- B3, whether understanding the whole mod first catches what matters;
- B4, the house conventions that came up.

## Before each session

- [ ] **No Requiem skills installed** on the host used (`claude plugin list` shows no `authoria-requiem`). houseCARL
      2.2.0 loaded as normal.
- [ ] **MO2 profile:** the list profile `Authoria - Requiem Reforged` is selected (it's real list work), not
      `ARR Personal Profile`.
- [ ] **A home for the work:** an `arr-release` task folder (`tasks/<slug>/`, from its template). The patch is a list
      change, so it also gets a ledger line in the open release's `CHANGES.md`.
- [ ] **The mod:** new to the list, not yet patched, enabled in the list profile.

## How to run it (Aaron, 2026-11-18)

- **The goal is a correct patch, made the way Aaron normally works.** Guide the agent as much as the patch needs.
  The guidance is the data.
- **Let the agent go first on each call, then correct it.** Don't front-load house rules at the start, or the log
  can't show what the agent lacked.
- **Don't tell the agent it's a test, and don't ask it to keep a log.** Being told it's a test changes how it
  behaves. Its own log would be self-grading (intent C9).
- Afterwards, Aaron names the session. A fresh-context agent reads the transcript and writes the decision log in the
  format below, and Aaron checks it. Aaron's own one-line notes on calls that mattered are optional.

Suggested opening (adjust to how Aaron would really start):

> Patch `<mod>` for Requiem for the ARR list, through houseCARL. First understand the whole mod (records, scripts,
> assets, runtime-layer lines) and tell me what needs a Requiem decision, with your recommendation for each. Then
> we agree the calls, then you write the patch into a new plugin.

## Decision log entry format (written from the transcript)

```markdown
### D<n>: <short question>

- **Records:** <FormID:Plugin, EditorID>, or "whole mod"
- **Options:** <a> / <b> / …
- **Claude recommended:** <option>, because <evidence: what was read, which comparable>
- **Aaron chose:** <option>, because <reason>
- **Claude missed:** <knowledge Aaron had to supply, or "nothing">
- **Kind:** value | stance (upstream / bake) | house convention | coverage | tooling | other
```

## After each session

1. A fresh-context agent mines the transcript into `B-<armour|quest>-<mod-slug>.md` here, with an authorship stamp
   and no local paths (public repo). Aaron checks it. The raw transcript stays local.
2. Add a short "what it shows" note at the top: recurring calls, what was missing, what the dissection caught or
   missed, and the house conventions decided.
3. Add a line to the findings index in `../../recon.md`.

## Sessions

| Session | Mod | Log | Status |
|---|---|---|---|
| Armour | Bloodline (run 2026-11-18 in `arr-personal`, Aaron's personal playthrough) | `B-armour-bloodline.md` (to write) | session done; transcript not mined |
| Quest | *to choose* | | not started |
