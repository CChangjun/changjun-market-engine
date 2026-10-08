# Development roadmap

## Status legend

- **Complete**: implementation and the intended checkpoint review are complete.
- **Validation pending**: implementation/static checks are complete, but TradingView compile or historical runtime review remains.
- **Planned**: design scope is defined but implementation has not started.

## Overview

| Revision | Scope | Status |
|---|---|---|
| R0 | V0905 source preservation | Complete |
| R1 | Asset Profile, TF Router, D/W Regime | Complete |
| R2 | FVG/IFVG lifecycle, CE and Consumption | Complete |
| R3 | ICT structure, liquidity and causal sequences | Complete |
| R4 | Candidate State Machine | Complete |
| R5 | Bull/Bear/Range Expert Model | Complete |
| R6 | Native Causal Order Block | Complete |
| R7 | Probability Responsibility Refactor | Validation pending |
| R8 | US Semiconductor Relative Strength | Planned |
| R9 | Dynamic Macro V2 | Planned |
| R10 | Calibration and Validation | Planned |

## Completed foundations

### R0 — V0905 preservation

- Preserved the supplied V0905 indicator as the redevelopment baseline.
- Removed the obsolete 4,051-line implementation from the active development path.
- Established revision boundaries so new layers could be reviewed independently.

### R1 — Asset profile, timeframe router and D/W regime

- Added Crypto, US Semiconductor, Tech ETF and Other profiles with Auto detection.
- Added confirmed Native/HTF1/HTF2 routing.
- Added persistent Daily/Weekly Bull, Range and Bear regime ownership.
- Prevented lower-timeframe requests from being used as higher-timeframe context.

### R2 — FVG/IFVG lifecycle

- Separated calculation records from drawing objects.
- Added one-way `FVG -> IFVG -> retirement` lifecycle.
- Added CE, fill, overlap volume, repeated touch, acceptance, rejection, consumption and survival state.
- Removed simple age as the primary economic deletion rule.

### R3 — ICT structure V2

- Added confirmed-pivot EQH/EQL.
- Added PDH/PDL/PWH/PWL external liquidity with consumption state.
- Defined BOS, CHOCH and sweep-qualified MSS.
- Added ordered reversal and continuation causal sequences.

### R4 — Candidate State Machine

- Added one-shot `C`, monotonic Setup ID and a single-owner Pending slot.
- Enforced a minimum one-completed-bar delay before L/S.
- Added frozen confirmation/invalidation prices, expiry and terminal-event priority.
- TradingView compilation passed at the R4 checkpoint.

### R5 — Bull/Bear/Range Expert Model

- Added persistent-regime ownership of `TC`, `CT`, `REV` and `RNG` routes.
- Froze expert and archetype identity into the Candidate.
- Separated causal sequence responsibility from repeated legacy setup gates.
- Performed subsequent R5.1-R5.3 deadlock analysis and Candidate/Final separation.
- TradingView compilation passed; initial historical L/S observations were reviewed. Statistical performance tuning was intentionally deferred.

### R6 — Native Causal Order Block

- Snapshots the actual opposing source candle at displacement.
- Separates Bull/Bear OB and source body/wick responsibilities.
- Tracks retest, CE mitigation, rejection, consumption, full mitigation and invalidation.
- Prohibits rescanning history at BOS confirmation.
- Keeps OB diagnostic-only so it does not duplicate FVG/IFVG evidence.
- Native-TF compilation and chart review passed. HTF OB is deferred because D/W regime and HTF FVG already provide higher-timeframe context.

## Current checkpoint

### R7 — Probability Responsibility Refactor

Objective: reduce repeated use of the same information without relaxing thresholds simply to manufacture signals.

- Separates structural Prior, confirmation Evidence/Posterior and execution Risk/EV responsibilities.
- Removes repeated Final vetoes for legacy score, coherence, adverse selection and zone quality.
- Keeps Posterior as a model score rather than presenting it as calibrated real-world win probability.
- Preserves the default Crypto 7-day 6-7% first-passage target model.
- Adds realized-volatility-normalized target barriers for US Semiconductor, Tech ETF and Other profiles.
- Preserves R4 Candidate ownership, delay, invalidation, expiry and price confirmation.
- Keeps arbitrary weight/threshold tuning deferred until R10.

Status: implementation and static checks are complete. TradingView compilation, visual regression and historical terminal-path review are pending.

## Planned research

### R8 — US Semiconductor Relative Strength

Primary use case: 4H US semiconductor trading context.

- Individual symbol versus QQQ relative strength.
- Individual symbol versus SMH/SOXX sector relative strength.
- Sector leader and relative-weakness classification.
- Separate QQQ and leveraged QLD behavior.
- QLD volatility scaling.
- Connect to Bull/Bear experts without duplicating regime or target evidence.

Completion time is intentionally not estimated until request limits, symbol availability and relative-strength definitions are validated.

### R9 — Dynamic Macro V2

Asset-aware macro context rather than one universal macro score.

- US01Y, US02Y and US10Y rates.
- DXY.
- USDJPY and EURJPY.
- VIX.
- Recursive Least Squares dynamic coefficients.
- Missing-data availability mask.
- Intercept and coefficient stability controls.
- Separate Crypto and semiconductor macro models.
- Prevent the same macro feature from affecting Posterior and Final twice.

Existing design notes may accelerate implementation, but external data availability and TradingView request limits remain hard constraints.

### R10 — Calibration and validation

Final empirical evaluation phase.

#### Universes

- BTC/ETH: 4H, 1D and 1W.
- US semiconductor equities: primarily 4H.
- QQQ and QLD.

#### Measurements

- Candidate confirmation, invalidation and expiry rates.
- Maximum Adverse Excursion (`MAE`).
- Maximum Favorable Excursion (`MFE`).
- Target-before-stop and stop-before-target rates.
- Performance by `TC`, `CT`, `REV` and `RNG`.
- Performance by Bull, Bear and Range regime.
- Signal latency and trade-frequency distribution.
- In-sample and out-of-sample separation.

#### Calibration rule

Weights and thresholds change only when measured results identify a reproducible error. R10 must not optimize solely for the historical period used to design the feature.

## Deferred items

- Position Lifecycle (`Entry/Hold/Exit/Add/Flip`) remains optional and will be reconsidered only when a concrete execution use case appears.
- Elliott Wave and discretionary chart-pattern naming are not core model gates. Any future addition must be expressed causally and measured independently.
- HTF Order Blocks are deferred until they show information not already supplied by regime and HTF FVG layers.
