# Changelog

This file records architectural checkpoints. It does not claim investment performance.

## R7 — Probability Responsibility Refactor

### Added

- Asset-aware target barriers: explicit Crypto target band and volatility-normalized US/Other target band.
- Seven-bit Final Responsibility Mask with a fully open value of `127`.
- R7-specific README and architecture documentation.

### Changed

- Structural features own Prior.
- New confirmation information owns Evidence/Posterior.
- Directional risk and adverse selection are evaluated by target distribution and EV.
- Candidate formation uses the routed archetype and Candidate Posterior.
- Pending state latches Final Posterior qualification.
- Actual confirmation independently requires RR, EV, target probability, execution state, valid frozen route and price confirmation.
- EV uses selected Posterior directly rather than blending coherence into the same evidence again.
- Legacy composite score remains diagnostic instead of acting as an additional Final veto.

### Preserved

- Crypto default 7-day 6-7% objective.
- R4 single-owner Candidate, one-shot C, minimum one-bar delay, invalidation and expiry.
- R5 expert/archetype routing.
- R6 Native OB as a diagnostic layer.
- Seven external `request.security()` calls.

### Validation

- Removed-reference and delimiter checks passed.
- Inputs: `156`.
- Estimated TradingView plot count: `64`.
- TradingView compilation and runtime review pending.

## R6 — Native Causal Order Block

- Added displacement-time source snapshot and BOS confirmation.
- Body zone and wick invalidation stored separately.
- Added retest, CE mitigation, rejection, consumption and retirement lifecycle.
- Added OB event and nearest CE Data Window diagnostics.
- Did not connect OB to C/L/S gates.
- Native-TF TradingView checkpoint passed.

## R5.1-R5.3 — Candidate/Final deadlock corrections

- Removed repeated recreation of causal setup gates.
- Allowed the frozen Candidate archetype to select its Pending evaluation path.
- Added final-quality latching, followed by the R7 responsibility split.
- Preserved price confirmation, invalidation, expiry, ownership and no-overwrite semantics.

## R5 — Regime Expert Models

- Activated persistent Bull/Range/Bear routing.
- Added TC, CT, REV and RNG archetypes.
- Froze expert/archetype ownership into Candidate state.
- Increased signal and structure marker size by one TradingView step.

## R4 — Candidate State Machine

- Added Setup ID, one-shot Candidate and Pending ownership.
- Enforced next-bar-or-later price confirmation.
- Added invalidation, expiry and terminal event codes.

## R3 — ICT Structure V2

- Added EQH/EQL and completed Daily/Weekly external liquidity.
- Added BOS, CHOCH and sweep-qualified MSS.
- Added ordered reversal and continuation sequences.

## R2 — FVG/IFVG Lifecycle

- Added one-way FVG-to-IFVG transition.
- Added CE, volume, touch, acceptance, rejection, consumption and survival state.
- Separated calculation lifecycle from drawing limits.

## R1 — Architecture Foundation

- Added asset profiles, confirmed timeframe routing and D/W regime probabilities.
- Preserved the V0905 signal-model boundary during the initial architecture change.

## R0 — Baseline

- Preserved the supplied V0905 source as the redevelopment reference.
