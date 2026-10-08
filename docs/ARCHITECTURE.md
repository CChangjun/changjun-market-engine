# Architecture

## Design objective

Changjun Market Engine(창준지표)은 구조 이벤트를 미래 정보 없이 순서대로 확정하고, 설정의 방향성 품질과 실제 진입 가능성을 분리해 판단하는 것을 목표로 합니다. 현재 출력은 경험적 승률이 아니라 설계된 model score입니다.

## Runtime pipeline

```text
Asset profile
  -> Native / HTF feature calculation
  -> confirmed timeframe router
  -> Daily / Weekly Bull-Range-Bear regime
  -> structure, liquidity and zone lifecycle
  -> TC / CT / REV / RNG expert routing
  -> structural Prior
  -> confirmation Evidence and Posterior
  -> one-shot Candidate snapshot
  -> Pending: confirmation / invalidation / expiry
  -> RR + EV + target probability + execution
  -> Long / Short
```

## Asset profiles

| Profile | Intended universe | Target model |
|---|---|---|
| Crypto | BTC, ETH and crypto pairs | Explicit default 7-day 6-7% first-passage barrier |
| US Semiconductor | Major US semiconductor equities | Realized-volatility-normalized horizon barrier |
| Tech ETF | QQQ, QLD and related ETFs | Realized-volatility-normalized horizon barrier |
| Other | Unsupported symbols | Neutral fallback with volatility-normalized barrier |

`Auto` detects supported symbols. Crypto-only ETH/BTC relative-value data is not applied to US profiles.

## Timeframe router

| Chart timeframe | Native | HTF1 | HTF2 |
|---|---|---|---|
| Below 1D | Chart TF | 1D | 1W |
| 1D to below 1W | Chart TF | 1W | 1M |
| 1W and above | Chart TF | 1M | Disabled |

HTF values use completed source bars. Daily/Weekly regime ownership is persistent rather than changing immediately on every raw probability fluctuation.

## Causal structure rules

- Pivot information is used only after confirmation.
- HTF requests use completed bars.
- A reversal sequence preserves the order `Sweep -> MSS/CHOCH -> Displacement -> FVG -> CE reaction`.
- A continuation sequence preserves the order `BOS -> Displacement -> FVG -> CE reaction`.
- Candidate `C` is emitted once per accepted setup.
- Final confirmation cannot occur on the Candidate bar; at least one completed bar is required.
- Invalidation and expiry are evaluated before final confirmation.
- An active Candidate owns a single slot and cannot be overwritten by an opposite setup.

## Zone lifecycle

### FVG / IFVG

```text
FVG -> first directional invalidation -> IFVG
IFVG -> opposite invalidation -> retired
```

Fill, CE interaction, overlap volume, repeated touch, rejection and consumption are state variables. Display limits remove drawing objects without silently deleting economic calculation records.

### Native causal Order Block

```text
Opposing source candle
  -> displacement snapshots that exact source
  -> BOS confirms the causal chain
  -> Active
  -> Retest / CE mitigation
  -> Rejection or Consumption
  -> Invalidation / Full mitigation / Retirement
```

The source body defines the visible OB zone. The source wick extreme is retained separately for invalidation. BOS confirmation never rescans history to substitute a more convenient candle. R7 keeps OB diagnostic-only to avoid duplicating FVG evidence before independent validation.

## R7 probability responsibilities

Earlier revisions could allow a single feature to influence Prior, Posterior, EV and Final independently. R7 reduces this conjunctive duplication.

| Stage | Owns | Does not independently own |
|---|---|---|
| Prior | structural state, zone stability, liquidity, regime and location | entry execution |
| Evidence | new reaction, displacement, acceptance and coherence information | final RR veto |
| Posterior | directional model confidence | literal calibrated win rate |
| Target / EV | adverse selection, directional risk, reward and horizon reachability | setup identity |
| Final | latched Posterior, current RR/EV/target, execution state and price confirmation | repeated score/coherence/zone vetoes |

Candidate birth uses the routed archetype and Candidate Posterior threshold. During Pending, Final Posterior qualification can latch. RR, EV, target probability and execution state remain current-bar requirements when price confirms.

The R7 Data Window mask is:

| Bit | Meaning |
|---:|---|
| 1 | Candidate price confirmation |
| 2 | Final Posterior latched |
| 4 | RR passed |
| 8 | EV passed |
| 16 | Target/adverse first-passage probability passed |
| 32 | Armed and cooldown execution state |
| 64 | Valid frozen expert/archetype route |

`127` means every final responsibility is open on the current confirmed bar.

## Expert routes

| Persistent regime | Long route | Short route |
|---|---|---|
| Bull | Trend Continuation (`TC`) | Counter-trend (`CT`) or major reversal (`REV`) |
| Bear | Counter-trend (`CT`) or major reversal (`REV`) | Trend Continuation (`TC`) |
| Range | Range reversal (`RNG`) or breakout `TC` | Range reversal (`RNG`) or breakout `TC` |

Expert and archetype ownership are frozen into the Candidate snapshot. A pending TC cannot silently become CT, REV or RNG.

## Known limits

- Posterior values are not calibrated empirical probabilities.
- Confirmation-based structure necessarily trades early detection for causal reliability.
- R7 is at TradingView's plot-count limit and should be extended carefully.
- Order Block is not yet permitted to alter C/L/S.
- US relative-strength and macro RLS layers remain future work.
