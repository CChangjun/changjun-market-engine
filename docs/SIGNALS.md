# Chart signals and visual guide

## Structure events

| Signal | Interpretation |
|---|---|
| `BOS ↑` | Confirmed close above a swing in the stored bullish structure direction |
| `BOS ↓` | Confirmed close below a swing in the stored bearish structure direction |
| `CHOCH ↑/↓` | First confirmed break against the stored structure direction; an early change warning |
| `MSS ↑/↓` | CHOCH with a matching recent opposing-side liquidity sweep |

BOS is continuation structure. CHOCH is a possible direction change, while MSS requires additional liquidity context and is therefore more selective. None is a standalone entry instruction.

## Liquidity events

| Signal | Interpretation |
|---|---|
| `MSWP` | Major Sweep: price removes major high/low liquidity and reclaims |
| `SWP` | Qualified Minor Sweep |
| `m` | Raw Minor Sweep that has not passed the qualification filter |
| `EQH` | Equal-high liquidity built from confirmed pivots within ATR tolerance |
| `EQL` | Equal-low liquidity built from confirmed pivots within ATR tolerance |

An EQH/EQL calculation record is consumed after price removes the level. Its displayed line may fade before the next source period or lifecycle update.

## Candidate and final signals

| Signal | Interpretation |
|---|---|
| `C` | One-shot Candidate created by a valid expert/archetype route and Candidate Posterior |
| `L` | Long confirmation after Pending, price confirmation and all execution responsibilities |
| `S` | Short confirmation after Pending, price confirmation and all execution responsibilities |

`C` is not a buy/sell call. It owns a frozen direction, expert, archetype, confirmation price and invalidation price. The Candidate retires through confirmation, invalidation or expiry.

R7 Final does not require legacy score, coherence, adverse-selection and zone gates to pass again independently. Their information remains in the stage that owns it; current RR, EV, target reachability and execution state still must pass.

## Lines and zones

| Visual | Meaning |
|---|---|
| Orange solid line | Fast EMA |
| Blue solid line | Slow EMA |
| Yellow stepped line | Dealing Range equilibrium (`EQ`) |
| Long purple dashed line | Previous Week High/Low (`PWH/PWL`) |
| Yellow dashed line | Previous Day High/Low (`PDH/PDL`) |
| Orange / cyan dashed line | Active `EQH/EQL` liquidity |
| Bright green / pink short dashed line | Bull/Bear FVG or IFVG consequent encroachment (`CE`) |
| Teal / red shaded zone | Bull/Bear FVG, IFVG or Native Order Block according to its label |

Consumed external-liquidity lines can become gray or transparent. A zone display toggle affects drawings, not necessarily the internal calculation record.

## Zone timeframe controls

### Show Native TF Zones

Displays zones calculated from the active chart timeframe.

- 4H chart → 4H zones
- 1D chart → 1D zones
- 1W chart → 1W zones

### Show HTF1 Zones

Displays the first higher core timeframe.

- 4H chart → 1D
- 1D chart → 1W
- 1W chart → 1M

### Show HTF2 Zones

Displays the second higher core timeframe.

- 4H chart → 1W
- 1D chart → 1M
- 1W and above → disabled

For a cleaner chart, start with Native only and enable HTF1/HTF2 when higher-timeframe location is needed.

## Interpretation cautions

- Structure signals occur after confirmed breaks and therefore can appear after a sizable move.
- A later Long after an earlier Long is not automatically an error; it can represent a new leg or setup after re-arming.
- The model intentionally does not force an alternating `L -> S -> L` sequence.
- Historical placement does not imply the signal was available before its confirmed bar.
