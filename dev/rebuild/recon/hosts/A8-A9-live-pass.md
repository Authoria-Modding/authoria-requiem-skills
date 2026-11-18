# A8 / A9 live pass: install and smoke test on Claude Code and Codex

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (finding). Follows the desk pass [`A8-A9-codex-and-distribution.md`](A8-A9-codex-and-distribution.md)
(2026-10-31). Docs recheck: [`A8-A9-docs-recheck.md`](A8-A9-docs-recheck.md). Aaron lifted the "no live install"
hold for this pass (2026-11-18). The pack installed is the **1.x pack (1.10.0)**, so this tests the install path and
the hosts, not the rebuild's content.*

## Verdict

**One repo installs on both hosts with the manifests we already have.** Codex reads `.claude-plugin/marketplace.json`
and `.claude-plugin/plugin.json`, so no `.codex-plugin/` tree is needed for a marketplace install. Both hosts name the
skills `authoria-requiem:<skill>`. GPT picked the right skills implicitly and drove houseCARL's MCP. On the one real
task it made two stance errors the rebuild has to prevent on both hosts.

## Setup

- Removed the parked 1.x copy (`~/.claude/skills-parked/authoria-requiem`). No other copy existed on either host.
- Claude Code (desktop app's CLI) and Codex CLI 0.162.0-alpha (bundled with the Codex desktop app, ChatGPT login,
  model `gpt-6-luna`). houseCARL 2.2.0 was already installed on both (Claude: skills-dir plugin; Codex:
  `[mcp_servers.housecarl]` plus its skills in `~/.agents/skills`).

## Install (A9)

| Host | Commands | Result |
|---|---|---|
| Claude Code | `claude plugin marketplace add Authoria-Modding/authoria-requiem-skills`, then `claude plugin install authoria-requiem@authoria-requiem-skills` | Cloned over HTTPS, validated, installed at user scope. `claude plugin validate --strict` passes on both manifests. A new session lists all 11 skills as `authoria-requiem:<skill>` next to houseCARL |
| Codex | `codex plugin marketplace add Authoria-Modding/authoria-requiem-skills`, then `codex plugin add authoria-requiem@authoria-requiem-skills` | Read `.claude-plugin/marketplace.json` directly; installed 1.10.0 into `~/.codex/plugins/cache/<marketplace>/<plugin>/<version>/skills/` and enabled it in `config.toml`. No Codex manifest needed |

Not run: a release zip installed by hand. There is no release build yet. That belongs to the build stage, with the
houseCARL lesson that hand-copies into the shared `~/.agents/skills` must record and prune only their own folders.

## Smoke test (A8)

| Host | Query | Result |
|---|---|---|
| Claude Code | 4 trigger queries via `claude -p` | **Blocked:** headless runs fail with "OAuth session expired". Aaron re-logs the CLI in a terminal, then the trigger evals can run (decisions.md: real invocation, real houseCARL loaded) |
| Codex | "Which requiem skills do you have?" | All 11 listed |
| Codex | "New mod with a dozen greatswords, make them fit Requiem (plan only)" | Loaded `requiem-patching` then `requiem-weapon-patching` implicitly, by reading their SKILL.md from the plugin cache. Named them `authoria-requiem:requiem-…` |
| Codex | "Write a SPID line for bandits" (should not trigger) | No requiem skill loaded. It loaded houseCARL's `spid-authoring` instead. It looked up a spell FormID by web search rather than houseCARL |
| Codex | Real read-only task: check `11CCBF:Vigilant.esm` (Holy Greatnail) against Requiem | Read our weapon skill and houseCARL's `mutagen-reference`, then called houseCARL MCP (`load_order_status`, `records`; one call failed and was retried). It **found the speed 9.75 bug** on its own (filed in BUGS.md as W1). It used 1.34M input tokens, 9.4k output |

### What GPT got wrong on the real task

1. **It called a handmade patch "generated".** `Authoria - Reqtificated - Vigilant.esp` is ARR's hand-authored patch,
   but GPT treated it as build output and said to "base any patch on Vigilant.esm". houseCARL's instructions name the
   real generators. The name "Reqtificated" misled it.
2. **It took the build's output as the target.** It compared against `REQ_Weapon_Steel_Greatsword` as the
   **Requiem for the Indifferent** winner (damage 102, baked), and proposed hand-setting Damage 18 → 102. That is
   hand-stamping the Reqtificator's output, the error the pack exists to prevent. It also picked a steel comparable
   for a silver weapon.

Both are stance errors, not install errors, and the 1.x pack was loaded. They're inputs for the rebuild's router:
- say which ARR plugins are handmade patches;
- say that a comparable is read from Requiem's own plugin, not from the RfI output.

The token bill (1.34M on one weapon) matches the eval's finding that 1.x costs about 4×.

## Docs recheck (summary)

46 claims rechecked: about 29 confirmed, 6 changed, 2 not found. Full table in the recheck doc. Changes that matter to
the spec:
- **Codex reads a root `plugin.json`** first, then `.codex-plugin/plugin.json`, and also `.claude-plugin/plugin.json`
  (in the `openai/codex` source on `main`). That's why our install worked.
- **Namespacing is `plugin:skill` on both hosts.** The desk pass's "Codex sees the bare folder name" is wrong.
- **Frontmatter:** Codex needs only `description`; `name` falls back to the folder name. It reads
  `metadata.short-description` and ignores other keys. Claude Code reads about 20 keys.
- **Listing budgets:** Codex uses 2 % of context in tokens (8,000 characters when the context size is unknown), shrinks
  every description evenly, then drops skills from the end of the list (user skills before plugin skills, by name).
  Claude Code uses 1 % of context and 1,536 characters per entry, both now settable. It always lists every name and
  drops the descriptions of the least-used skills first.
- **User skills path:** `~/.agents/skills` (`~/.codex/skills` is deprecated but still scanned).
- **OpenAI's skill-writing guidance** moved to the GPT-6 Astra guide; the latest model is GPT-6.2 Astra.

Still open: whether Codex needs a version bump to pick up an update; where plugin skills fall in Codex's drop order;
`codex plugin add` works but isn't in the published docs; no OpenAI rule for spelling MCP tool names in a skill.

## For the spec

- **Ship one repo with the Claude manifests.** A Codex manifest is optional; add a root or `.codex-plugin/plugin.json`
  only if a Codex-only field is needed (e.g. `agents/openai.yaml` for display name or invocation policy).
- **Write sibling skills as `authoria-requiem:<skill>`.** It is the same on both hosts.
- **Frontmatter: `name` + `description`.** Front-load the trigger words, since both hosts shrink descriptions under
  budget pressure.
- **The router must state the two facts GPT missed** (the handmade-patch list, and comparables from Requiem, not RfI).
  The Codex smoke test is the cheap regression check for both.
- **Graded runs on Codex are possible** with `codex exec --json` (it logs MCP calls and skill-file reads). Pin a
  model with `-m`, because `config.toml`'s `gpt-5.5` is refused for ChatGPT-account Codex.

## Install state left behind

The 1.x pack (1.10.0) is now installed on **both hosts** at user scope, so it loads in every session. Remove it before
B1–B4 or any no-skill run, unless those runs are meant to use it:
- `claude plugin uninstall authoria-requiem@authoria-requiem-skills`
- `codex plugin remove authoria-requiem@authoria-requiem-skills`
