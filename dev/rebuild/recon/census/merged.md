# Census conventions, merged (with dominance)

*Author: Aaron (+ Claude session) · 2026-11-18*

*Class: ARCHIVE (finding). Input for the spec. File: [`conventions.merged.json`](conventions.merged.json). Built
from the 12 `*.conventions.json` files in `stage1/` and `stage2/` (unchanged) and the census ledgers in the local
eval harness (`census/scripts/dominance_units.py`, `merge_conventions.py`; local, unpublished).*

## What it is

One list of all **277** census entries. Each keeps its original fields and gains four:

| Field | Meaning |
|---|---|
| `doc` | Source file, e.g. `stage1/ARMO` |
| `class` | Normalised label: `requiem-aligned`, `house`, `baked`, `mixed`, `noise`, `bug-outlier`, `bug-suspected`, … (`class_raw` keeps the original) |
| `dominance` | `top_plugin`, `top_share` (top plugin's rows ÷ the convention's non-held-out rows), `top_rows`, `rows_non_held_out`, `plugins`, `matched` (which census unit it was matched to) |
| `dominance_flag` | `one-plugin` (top share ≥ 0.8), `dominated` (≥ 0.5), `spread` (< 0.5), or null when no unit matched |

**How dominance is matched, not guessed.** The census grouped ledger rows into units: mechanical rules, residual
families, and the patterns inside a family. A convention gets a dominance only when one unit of its record type has
exactly its `support_rows`. Ties are broken by `support_plugins`. An entry with `support_plugins = 1` and no unit
match gets `top_share = 1.0`, marked `derived`, with no plugin named. Everything else stays null. Most of the
unmatched entries are a sum of several units, or a count of records rather than rows.

## Results

178 entries are real conventions (`requiem-aligned`, `house`, `baked`, `mixed`). The other 99 are bugs, noise and
leads.

| Class | Total | Spread | Dominated | One-plugin | Unmatched |
|---|---|---|---|---|---|
| requiem-aligned | 104 | 24 | 9 | 19 | 52 |
| house | 51 | 10 | 6 | 10 | 25 |
| baked | 14 | 10 | 0 | 1 | 3 |
| mixed | 9 | 2 | 0 | 0 | 7 |
| **All** | **178** | **46** | **15** | **30** | **87** |

- **91 of 178 have a dominance. Half of those (45) rest mostly on one plugin.**
- **Bruma's master patch is the top plugin in 22** of the dominated or one-plugin entries, across all classes.
  Then come Vigilant (7), Glenmoril (6) and Apocalypse (3). This agrees with split hunt 11, which measured 14 Bruma
  habits with and without Bruma.
- **Baked conventions are spread** (10 of 11 matched): the build stamps them everywhere, as expected.
- A `requiem-aligned` entry that is `one-plugin` still stands on Requiem's own records. Dominance says how much **ARR**
  evidence it has, not whether it is right.

## For the spec

- **A `house` convention flagged `one-plugin` or `dominated` is one author's habit until Aaron or Heisen confirms
  it.** That's 16 entries; read them first in the spec interview.
- **For `requiem-aligned` entries, the Requiem comparable is the evidence**, per the reference stance (decisions.md
  2026-10-31). Dominance only tells us which ARR patch to check against.
- **Unmatched entries (87) aren't weaker.** Their counts just don't map to one unit. Where one matters, read its
  `spread` text, or split hunt 11's Bruma table.
