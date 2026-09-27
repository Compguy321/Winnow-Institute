# Scoring

## Stage 1 — Knockout gates (cheap, early; SCREEN stage)

Each dimension scored 1–10. Fail line at ≤2 ("completely" bad):

- **Novelty**: already proven in literature → fail. (Prior-art check per hypothesis.)
- **Plausibility**: core claim contradicted, or mechanism incoherent → fail.
- **Feasibility**: no feasible experimental path → fail.
- **Impact**: likely zero or negative marginal impact → fail.

Gates are deliberately lenient — they catch the clearly-dead; ranking does
the rest. Anything scoring ≥3 everywhere proceeds.

## Stage 2 — Net expected value (RANKER stage, survivors only)

```
Net EV = P(success) × Value(good) − P(harm) × Severity(harm) − Cost(program)
```

Denominated in **QALY-equivalents**.

- **P(success) = P(mechanism real) × P(decisive test)**. P(mechanism) grounded in
  verifier verdicts (all core claims supported by multiple sources → high;
  mixed → middling; mostly untested → low). The ranker must show its work.
- **Value(good)**: marginal QALYs — health (mortality + morbidity), plus rough
  economic and knowledge/VOI components (a clean falsification has value too).
  Impact estimated in order-of-magnitude bins (10s → 1M+), never false precision.
- **P(harm) × Severity**: residual risk in the same units; small for phased
  clinical-trial pathways by construction.
- **Cost(program)**: money/time/attention in QALY-equivalents (opportunity cost).

Rank by Net EV descending.

## Display

Each ranked proposal shows: Net EV, the EV component breakdown (show-your-work),
the 5-dimension profile (so the *shape* is visible, not just the number), and
tags. **high-risk-high-reward** tag: high impact bin + low P(success) — surfaced
separately as the moonshot list, never buried.

## Calibration

- Anchored 1–10 scale descriptions + historical reference cases as few-shot anchors.
- Human triage decisions recorded against ranker ordering; systematic
  disagreement → weight/threshold review.
- Backtest mode: check P calibration (did 30% ideas succeed ~30% of the time?),
  not just hit rate.
- Elo pairwise tournaments: deferred upgrade if absolute estimates drift.
