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

## Kickoff prompt (paste into a fresh session opened in the task folder)

> Patch `<mod>` for Requiem for the ARR list, through houseCARL, the way you would without any Requiem skill. Work
> in three phases and stop between them for me:
> 1. Understand the whole mod first: every record, script, asset and runtime-layer line it ships. Tell me what it
>    adds, and what needs a Requiem decision.
> 2. Give me a decision list of every judgement call, with your recommendation and the evidence for it. I choose.
> 3. Write the patch into a new plugin.
>
> Keep a decision log in `decision-log.md` in this folder. Append one entry per decision as we go, in the format
> below. Also log anything I had to tell you that you didn't know.

## Decision log entry format

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

1. Copy `decision-log.md` here as `B-<armour|quest>-<mod-slug>.md`, with an authorship stamp and no local paths
   (public repo).
2. Add a short "what it shows" note at the top: recurring calls, what was missing, what the dissection caught or
   missed, and the house conventions decided.
3. Add a line to the findings index in `../../recon.md`.

## Sessions

| Session | Mod | Log | Status |
|---|---|---|---|
| Armour | *to choose* | | not started |
| Quest | *to choose* | | not started |
