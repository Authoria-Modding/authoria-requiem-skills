# A8 / A9 docs recheck against the live vendor docs

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (finding). Part of the A8 / A9 live pass; summary in [`A8-A9-live-pass.md`](A8-A9-live-pass.md).*

Recheck of `dev/rebuild/recon/hosts/A8-A9-codex-and-distribution.md` (desk pass, corpus from 2026-09-05) against
the live docs on 2026-11-18. Where the docs are silent, the `openai/codex` source on `main` (read 2026-11-18 through
the GitHub API) is cited instead. That source is `main`, not exactly the 0.162.0-alpha build we ran live, so treat
those rows as strong evidence, not proof.

**Live ground truth (2026-11-18).** Codex CLI 0.162.0-alpha installed the pack with `codex plugin marketplace add
owner/repo` + `codex plugin add <plugin>@<marketplace>`, from a repo with only `.claude-plugin/marketplace.json` and
`.claude-plugin/plugin.json`. Skills landed in `~/.codex/plugins/cache/<marketplace>/<plugin>/<version>/skills/`.
GPT called them `authoria-requiem:requiem-patching`. Claude Code installed the same repo with `claude plugin
marketplace add` + `claude plugin install`.

Verdicts: **CONFIRMED** = docs say it now. **CHANGED** = docs now say something different. **NOT FOUND** = the
current docs don't say it (where we looked is given).

Short URL keys used in the table:

| Key | URL |
|---|---|
| CC-mkt | https://code.claude.com/docs/en/plugin-marketplaces (create-marketplace) |
| CC-host | https://code.claude.com/docs/en/plugins/host-marketplace.md |
| CC-mref | https://code.claude.com/docs/en/plugins/marketplace-reference.md |
| CC-man | https://code.claude.com/docs/en/plugins-reference (manifest reference) |
| CC-pub | https://code.claude.com/docs/en/plugins/publish.md |
| CC-skills | https://code.claude.com/docs/en/skills |
| AN-bp | https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices |
| OA-pbuild | https://developers.openai.com/codex/plugins/build |
| OA-plugins | https://learn.chatgpt.com/docs/plugins |
| OA-skills | https://learn.chatgpt.com/docs/build-skills (developers.openai.com/codex/skills redirects here) |
| OA-pskills | https://developers.openai.com/plugins/build/skills |
| OA-submit | https://developers.openai.com/plugins/guides/submit-claude-plugin |
| OA-import | https://learn.chatgpt.com/docs/import |
| OA-astra | https://developers.openai.com/api/docs/guides/latest-model/gpt-6-astra |
| OA-latest | https://developers.openai.com/api/docs/guides/latest-model |
| AS-spec | https://agentskills.io/specification |
| SRC | github.com/openai/codex `main`, files named in the row |

## Claim table

### Distribution (A9)

| # | Claim | Verdict | Current wording (short) | URL |
|---|---|---|---|---|
| 1 | Claude Code: repo with `.claude-plugin/marketplace.json`, then `/plugin marketplace add owner/repo`, then `/plugin install` | CONFIRMED | Same flow. Shell form is `claude plugin marketplace add` + `claude plugin install <name>@<mkt>`. There is now a one-step `--marketplace` form (v2.1.292+). Matches the live install | CC-mkt, CC-pub |
| 2 | Updates follow the `plugin.json` version | CONFIRMED | Users get a new copy only when the computed version changes. Omit `version` to track commit SHAs instead. `plugin.json` beats the marketplace entry | CC-host, CC-man |
| 3 | Tags `{plugin}--v{version}` | CONFIRMED | `claude plugin tag` creates `{name}--v{version}`. Dependency version ranges resolve against these tags | CC-pub, CC-host |
| 4 | Auto-update is off by default for third-party marketplaces | CONFIRMED | Off by default. The user turns it on in `/plugin` or an admin sets `autoUpdate`. No `marketplace.json` field turns it on | CC-host |
| 5 | Zip routes: `--plugin-dir` takes a `.zip`; `archive` sources with SHA-256 pinning | CONFIRMED (+ new) | `--plugin-dir` accepts the `.zip` itself. `archive` source takes `url` + `sha256`. New: `--plugin-url` pointed at a release `.zip` | CC-pub, CC-mref |
| 6 | Codex manifest is `.codex-plugin/plugin.json`, with `skills/`, `.mcp.json`, `hooks/` at the root | CHANGED | The portable manifest is now a root `plugin.json` (with `mcp.json`, no dot). `.codex-plugin/plugin.json` "remain[s] supported as a compatibility fallback". The scaffold still writes `.codex-plugin/`. The source also discovers `.claude-plugin/plugin.json` (SRC `exec-server-protocol/src/protocol.rs`, `DISCOVERABLE_PLUGIN_MANIFEST_PATHS`), which matches the live install | OA-pbuild, SRC |
| 7 | Codex `version` must be semver and change on each release | NOT FOUND | The build page shows `1.0.0`-style values but says nothing about semver or a required bump. The cache is keyed per version (row 9), so a bump is still the safe practice [inference] | OA-pbuild |
| 8 | Marketplaces are read from `.agents/plugins/marketplace.json`, a "legacy-compatible" `.claude-plugin/marketplace.json`, and `~/.agents/plugins/marketplace.json` | CONFIRMED | All three are listed, with the same "legacy-compatible" label. The source list also has `.agents/plugins/api_marketplace.json` and `.cursor-plugin/marketplace.json` (SRC `core-plugins/src/marketplace.rs`) | OA-pbuild, SRC |
| 9 | CLI `codex plugin marketplace add owner/repo`; installs cached per version | CONFIRMED | `marketplace add/list/upgrade/remove` are documented. Cache is `~/.codex/plugins/cache/$MARKETPLACE/$PLUGIN/$VERSION/` (`local` for local plugins), which matches the live path. `codex plugin add` is not in the docs, but it is in the source (SRC `cli/src/plugin_cmd.rs`: `add`, `list`, `marketplace`, `remove`) and we used it live | OA-pbuild, SRC |
| 10 | IDE extension doesn't support plugins; standalone skills work there | CONFIRMED | "The IDE extension doesn't support plugins." Skills work in the desktop app, the CLI and the IDE extension | OA-plugins, OA-skills |
| 11 | Portal submission converts `.claude-plugin/plugin.json`; skills required at `skills/<name>/SKILL.md` | CONFIRMED | The portal converts it to `.codex-plugin/plugin.json`. A direct upload needs at least one `skills/<skill-name>/SKILL.md` | OA-submit |
| 12 | Dropped or refused at submission: `marketplace.json`, `commands/`, `agents/`, `userConfig`, output styles, Claude-only settings | CHANGED | `commands/` and agents are now **converted into skills**, not dropped. Hooks are removed for public submission (they can still be installed manually in the desktop app). `userConfig` is replaced by explicit inputs or config. Output styles, LSP, themes, monitors and channels move into skills or are removed. `settings*`, `CLAUDE.md` and `.claude/settings*` are removed. `marketplace.json` and MCP config are "not relied on" | OA-submit |
| 13 | Local stdio MCP is refused at submission but works for a local install | CONFIRMED | Submission needs a public HTTPS Streamable-HTTP endpoint. A local server goes to a manual-install, desktop-only route | OA-submit |
| 14 | A local `/import` maps skills to skills | CONFIRMED (wider) | Skills→skills, plugins→plugins, slash commands→skills, hooks→Codex hooks, subagents→Codex subagents, instruction files→`AGENTS.md`, MCP→Codex MCP | OA-import |
| 15 | Codex ships `$skill-installer`; OpenAI prefers plugins for distribution | Half CONFIRMED | `$skill-installer` is a bundled system skill and can pull skills from other repos. The docs don't say "prefer plugins". Weak signal [secondary]: the `openai/skills` repo README carries a deprecation notice pointing at `openai/plugins` | OA-skills |
| 16 | Nothing on Claude installing a skill for the user beyond `/plugin marketplace add` | CONFIRMED (+ new) | Still no agent-driven install flow. New: CC-pub tells CLI/SDK authors to have their installer run or print the two `claude plugin` commands. A plugin directory dropped under `~/.claude/skills/` also loads at startup | CC-pub |
| 17 | houseCARL setup copies skills into `~/.agents/skills/` | CONFIRMED (path) | `$HOME/.agents/skills` is the documented user path | OA-skills |
| 18 | houseCARL registers `[mcp_servers.housecarl]` in `~/.codex/config.toml` | Not rechecked | houseCARL's own code, not vendor docs. `config.toml` is the documented Codex config file | OA-skills |

### Authoring for both hosts (A8)

| # | Claim | Verdict | Current wording (short) | URL |
|---|---|---|---|---|
| 19 | Both hosts read only `name` and `description` | CHANGED | Claude Code documents about 20 keys (`when_to_use`, `paths`, `allowed-tools`, `disable-model-invocation`, `hooks`, `model`, and others), now including the spec's `license`, `compatibility` and `metadata`. The Codex parser reads `name`, `description` and `metadata.short-description` (SRC `skills/src/parser.rs`) | CC-skills, SRC |
| 20 | Codex requires both, non-empty | CHANGED (partly) | The docs say SKILL.md "must include" both. The source rejects an empty `description`, but a missing `name` falls back to a default (the folder name) instead of failing | OA-skills, SRC |
| 21 | Codex description ≤ 1,024 characters | CONFIRMED by source, NOT FOUND in docs | The docs give no limit. The source truncates listing descriptions at 1,024 characters with `...` (`MAX_CATALOG_SKILL_DESCRIPTION_CHARS`). It does not reject them. The name limit is 64 characters | OA-skills, SRC `ext/skills/src/render.rs` |
| 22 | agentskills.io: `name` ≤ 64, lowercase + hyphens, equals the folder name | CONFIRMED (+) | Also: no leading or trailing hyphen, no `--`. `description` ≤ 1,024. Optional `license`, `compatibility`, `metadata`, `allowed-tools` (experimental) | AS-spec |
| 23 | Codex is silent on every other key; Claude-only fields don't carry over | Docs still silent; source resolves it | Unknown keys are ignored silently. The serde struct has no `deny_unknown_fields`, so Claude-only keys parse and are dropped. There is also a repair pass for prose YAML like `argument-hint: <x: y>` | OA-skills, SRC `parser.rs` |
| 24 | `agents/openai.yaml` sets display name, invocation policy and `dependencies.tools` | CONFIRMED | `interface.display_name` (+ short_description, icons, brand_color, default_prompt), `policy.allow_implicit_invocation`, `dependencies.tools` (type, value, description, transport, url) | OA-skills |
| 25 | Codex listing ≈ 2 % of context, 8,000 characters when unknown; shortens descriptions first, may omit skills | CONFIRMED (+) | Same numbers. New: `skills.max_context_tokens` sets the budget, capped at 10,000 tokens | OA-skills, SRC `render.rs` |
| 26 | Claude Code listing 1 % of context, 1,536-character per-entry cap | CONFIRMED (+) | 1 % of the context window. Each entry's `description` + `when_to_use` is capped at 1,536 characters. Both are now tunable: `skillListingBudgetFraction`, `SLASH_COMMAND_TOOL_CHAR_BUDGET`, `skillListingMaxDescChars`, plus `skillOverrides` "name-only" | CC-skills |
| 27 | Codex invocation: implicit from the description, explicit with `$skill`; opt-out `policy.allow_implicit_invocation: false` | CONFIRMED | `$` or `/skills` in the CLI and IDE, `@` in ChatGPT. With the policy `false`, explicit `$skill` still works | OA-skills |
| 28 | Claude Code opt-out is `disable-model-invocation` | CONFIRMED | Listed in the frontmatter table and in troubleshooting | CC-skills |
| 29 | Claude Code siblings are written `plugin:skill` | CONFIRMED (+ caveat) | `/plugin-name:skill-name`. Caveat: a frontmatter `name` replaces the folder name in the last segment. The prefix is the manifest name, not the marketplace entry name | CC-skills, CC-mkt |
| 30 | Codex sees the bare folder name; Codex plugin-skill namespacing undocumented | CHANGED | The docs still barely cover it: the plugin `name` is "the plugin identifier and component namespace". The source qualifies plugin skills as `{namespace}:{name}` (SRC `ext/skills/src/loader/namespace.rs`, `qualify`). Live, GPT used `authoria-requiem:requiem-patching`. So Codex uses `plugin:skill` too, not the bare name | OA-pbuild, SRC |
| 31 | Shared body style: imperative steps, concise SKILL.md, detail one hop away, forward-slash paths, no contradictions | CONFIRMED | AN-bp: under 500 lines, one level deep, forward slashes, consistent terms. OA-pskills: concise, detail in `references/`. OA-skills: imperative steps. OA-astra: audit for conflicting instructions | AN-bp, OA-pskills, OA-skills, OA-astra |
| 32 | Codex: provider-neutral language ("the model") | CONFIRMED (moved) | Stated on the submit-a-Claude-plugin guide, not on the skills pages | OA-submit |
| 33 | Codex: state inputs, steps, output, facts not to infer, when to ask/stop/decline | CONFIRMED | The same list, plus "which supporting files to consult" | OA-pskills |
| 34 | GPT-6 Astra "can be more sensitive to instructions contained in skills"; may block early; recommended precedence line; warns against unsolicited approval flows | CONFIRMED (moved) | All four now sit on the GPT-6 Astra guide page. The latest model is now **GPT-6.2 Astra**, and the generic latest-model page no longer carries the skill guidance | OA-astra, OA-latest |
| 35 | Vendors differ: explaining the why, all-caps, negatives | Partly rechecked | AN-bp shows `ALWAYS` in a template and suggests "MUST filter", so its emphasis advice is still mixed. It does not explicitly say to explain the why. OpenAI's pages don't discuss these. skill-creator not rechecked | AN-bp |
| 36 | Codex evals: manual five-case matrix only; no trigger-rate harness, no validate command | CONFIRMED (moved) | The five cases are on OA-pskills (direct, indirect, incomplete, should-not-trigger, edge). OA-skills only says to test prompts against the description. No validate command or harness on either page. By contrast, Claude Code now has `claude plugin eval` with a `tool_used: Skill` trigger grader, and `claude plugin validate` on skills dirs | OA-pskills, OA-skills, CC-skills |

### Gaps and re-checks list

| # | Gap item (doc's wording) | Verdict | Current state | URL |
|---|---|---|---|---|
| 37 | Silent: Codex handling of other frontmatter keys | Resolved (source) | Ignored silently (row 23) | SRC `parser.rs` |
| 38 | Silent: which skills Codex's trimming drops first | Resolved (source) | See Gaps resolved | SRC `render.rs` |
| 39 | Silent: plugin-skill namespacing at invocation | Resolved | `plugin:skill` on both hosts (rows 29–30) | CC-skills, SRC, live |
| 40 | Silent: how a skill should spell MCP tool names | Partly resolved | Anthropic: fully qualified `ServerName:tool_name`. OpenAI gives no naming rule; it says to declare dependencies in openai.yaml and name the tools and their order | AN-bp, OA-pskills |
| 41 | Silent: body-length guidance | Resolved for Anthropic and the spec | AN-bp and AS-spec: under 500 lines (spec: under 5,000 tokens). OpenAI: "concise" only | AN-bp, AS-spec, OA-pskills |
| 42 | Contradictory: user skills path `~/.agents/skills` vs `~/.codex/skills` | Resolved | Docs list only `$HOME/.agents/skills`. Source: `$CODEX_HOME/skills` (`~/.codex/skills`) is a "Deprecated user skills location", still scanned for backward compatibility (SRC `ext/skills/src/host_roots.rs`). Bundled system skills live in `~/.codex/skills/.system` | OA-skills, SRC |
| 43 | Contradictory: `.claude-plugin/marketplace.json` "don't rely on" vs "legacy-compatible" | Resolved | Both are true, in different contexts. Local Codex reads it as a "legacy-compatible" marketplace (OA-pbuild, source path list), and the live install worked. Portal **submission** does not rely on `marketplace.json` (OA-submit) | OA-pbuild, OA-submit, SRC, live |
| 44 | Contradictory: listing budget in characters on one page, tokens on another | Resolved | Both, depending on context. Tokens (2 % of the window, ≈4 bytes/token) when the window is known, or `skills.max_context_tokens` (≤ 10,000 tokens). 8,000 **characters** when the window is unknown | OA-skills, SRC `render.rs` |
| 45 | Contradictory: local MCP works locally but is refused at submission | Resolved (not a contradiction) | Two routes: public directory needs remote HTTPS; manual install allows local | OA-submit |
| 46 | Stale corpus, re-check every figure | Done | This table | — |

## Gaps resolved

- **Codex extra frontmatter keys.** Silently ignored. The parser reads only `name`, `description` and
  `metadata.short-description`, and has no `deny_unknown_fields`. Claude-only keys are harmless on Codex but do
  nothing. A missing `name` falls back to the folder name. An empty `description` fails the skill.
- **Which skills Codex's trim drops first** (source, `ext/skills/src/render.rs`). There are three stages.
  - (1) If everything fits, all descriptions are kept whole.
  - (2) If names and locators fit but full descriptions don't, description characters are shared out
    round-robin, so every description shrinks and no skill is dropped.
  - (3) If even the bare entries don't fit, entries are kept in list order until the budget runs out, and the rest
    are omitted with a warning. In the core-compatible style the order is System, Admin, Repo, User, then by name.
    So user-scope skills, and late names alphabetically, go first.
  - Not found: where plugin skills sit in that order. Each description is also capped at 1,024 characters before
    budgeting.
- **Plugin-skill namespacing.** `plugin:skill` on both hosts. Codex: `{namespace}:{base_name}` in the source,
  matching the live `authoria-requiem:requiem-patching`. Claude Code: the manifest `name` is the prefix, and a
  frontmatter `name` overrides the folder name. The doc's rule that "Codex sees the bare folder name" is wrong: one
  `plugin:skill` spelling serves both hosts.
- **User skills path.** `~/.agents/skills` is current. `~/.codex/skills` is deprecated but still scanned.
- **`.claude-plugin/marketplace.json` on Codex.** Supported for local marketplace add and install, labelled
  legacy-compatible. The live install worked from it alone. `.claude-plugin/plugin.json` is also discovered as a
  manifest. Only portal submission ignores `marketplace.json`.
- **Listing budget units (Codex).** Tokens when the context window is known (2 %, or `skills.max_context_tokens`
  up to 10,000). Characters (8,000) as the fallback.
- **Claude Code listing budget and per-entry cap.** 1 % of the context window, and 1,536 characters per entry
  (`description` + `when_to_use`). Every name is always listed. On overflow, descriptions are dropped starting with
  the least-invoked skills. Both values can be tuned (`skillListingBudgetFraction`, `skillListingMaxDescChars`,
  `SLASH_COMMAND_TOOL_CHAR_BUDGET`).

## Still unresolved

- Codex `version` rules: the docs don't say whether a version bump is needed for `codex plugin marketplace
  upgrade` to pick up changes, or whether semver is required. Test it live: push without a bump, then upgrade.
- Where plugin-scope skills rank in Codex's omission order (stage 3 above). The order applies only in the
  core-compatible style; the extension and v2 styles keep the incoming order.
- `codex plugin add` is in the source and worked live, but it is absent from the published docs, which only show
  `/plugins` and `marketplace add`.
- Whether OpenAI "prefers plugins over `$skill-installer`" for distribution. Only a secondary signal (the
  `openai/skills` README deprecation) supports it.
- MCP tool spelling for Codex: OpenAI gives no rule. Anthropic's `ServerName:tool_name` advice is Claude-specific.
- The vendor-differences row (explaining the why, all-caps, negatives) was only partly rechecked. skill-creator
  was not re-read.
- The source rows come from `openai/codex` `main` on 2026-11-18, not from the exact 0.162.0-alpha tag.
