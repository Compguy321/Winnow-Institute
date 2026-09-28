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

### Estimating P(success) = P(mechanism real) × P(decisive test)

Two modes. The ranker must declare which it used — a probability built from a
base rate and one built from pure verdicts have different epistemic status,
and the ledger tags them separately.

**Mode A — reference class exists.** State the base rate first ("of N similar
proposals at this evidence stage, roughly X% panned out"), then update up or
down on the verifier verdicts. The base rate is the prior; the verdicts are
the evidence. Even a rough base rate beats the inside view.

**Mode B — brand new, no precedent.** Fall back to structured bottom-up
(no reference class to borrow — say so explicitly):
1. **Decompose into load-bearing sub-claims** (2–4). A hypothesis is a
   conjunction: score each sub-claim from its verdicts, multiply with a stated
   correlation assumption (default: mild positive correlation → discount the
   product ~10–20%, stated). The decomposition must name the binding
   constraint — the sub-claim doing the most work to keep P low.
2. **Verdict→probability rubric** (ranges, never points — pick within the
   range with a one-line reason):
   - core claim, 2+ independent primary sources → 0.85–0.95
   - core claim, single primary source → 0.60–0.75
   - core claim, untested but coherent → 0.30–0.50
   - peripheral claim contradicted → no cap, note it
   - core claim contradicted → proposal should not have survived triage;
     if it did, cap P(mechanism) at 0.30 and escalate

**P(decisive test), both modes** — split it:
`P(test feasible as specified) × P(outcome interpretable | run)`.
Most "decisive" tests die on the second term: the experiment runs but the
result is ambiguous. Score against the falsification sketch: "if this test
'succeeds,' would we actually believe the mechanism?" If not, P drops.

- **Value(good)**: estimated FIRST in the field pack's native unit
  (`value_native`, as a range never a point), then converted to QALY-equivalents
  via the pack's declared `conversion_to_qaly` rule. The native estimate is what
  domain experts check (health: mortality + morbidity; economic: dollars;
  knowledge: VOI — a clean falsification has value too); the QALY-eq figure is
  what the Ranker sorts by. Both are recorded; the conversion and its uncertainty
  are stated in `work_shown`, never baked in silently. Impact bins (10s → 1M+)
  apply to the QALY-eq figure; the native figure is shown at matched granularity
  (ranges, never false precision). Where welfare conversion is not meaningful
  (basic-science packs), rank within-field on P(success) x native significance /
  cost instead — see amendment 2026-09-28.
- **P(harm) × Severity**: residual risk in the same units; small for phased
  clinical-trial pathways by construction.
- **Cost(program)**: money/time/attention in QALY-equivalents (opportunity cost).

Rank by Net EV descending.

### Ranking fragility note

For the top-N, state how far P(success) would have to move to swap adjacent
ranks. If #1 and #2 flip on a 0.05 shift, the reviewer must know the ordering
is fragile — one line per adjacent pair, no extra math.

## Display

Each ranked proposal shows: Net EV, the EV component breakdown (show-your-work),
the 5-dimension profile (so the *shape* is visible, not just the number), and
tags. **high-risk-high-reward** tag: high impact bin + low P(success) — surfaced
separately as the moonshot list, never buried.

## Stage 3 — Crossover analysis (RANKER stage, post-rank, triggered only)

Net EV is computed for one implicit context. When the EV actually depends on a
contextual variable, say so — with the crossover point, not just the number.

**Trigger (ALL must hold):**
1. The mechanism is reasonably established — binary scientific uncertainty is
   NOT the dominant term (if P(mechanism) is the whole story, skip; one line
   saying so).
2. A single contextual variable (deployment size, population prevalence, unit
   cost, …) could plausibly flip the sign of net EV or move it several-fold
   across its realistic range.
3. The proposal is above the triage bar (top-N / positive EV).
4. **Reviewer selection.** The trigger is the Ranker's *recommendation*, not
   an order. Crossover analysis runs only on proposals the reviewer flags for
   a deeper look (at Gate 1 triage or later). Default selection = the
   trigger-recommended set; the reviewer may add or remove freely.

**Output per selected proposal (a few lines in the digest, not a chart):**
- The key variable and the **crossover range** where net EV ≈ 0
  (a range, never a point — the width of the range IS the uncertainty).
- 2–4 supporting evidence bullets grounding the range (named sources, not vibes).
- Qualitative confidence — **low / medium / high** — with a one-line reason.
  Never a numeric confidence percentage: that would be false precision stacked
  on uncalibrated probabilities and order-of-magnitude bins.
- The standing disclaimer: this is an **estimate / educated guess**, not a
  measurement. It tells you where the proposal clears the bar, not what will
  happen.

**Graph (optional, when the reviewer wants it).** For a selected proposal, plot
net EV against the key variable: central-estimate curve, shaded uncertainty
band from the input ranges, the crossover range shaded, the zero line, and the
reference-context point marked. Log x-axis when the variable spans orders of
magnitude. The figure carries the estimate disclaimer in its title. No
false-precision styling — no exact tick labels on the curve, no R², no
confidence intervals dressed as statistics.

**Skip rule:** when the trigger fails, record one line: "crossover analysis
n/a — EV dominated by [mechanism uncertainty / context-insensitive]."
No analysis is better than a decorative one.

## Prediction ledger

Probabilities become calibrated only if predictions are recorded *before*
outcomes are known. Nobody has to remember to do this — it is structural:

- **Written automatically at rank time.** When the ranker scores a proposal,
  it appends a ledger entry: proposal id, date, run id, P(success) with its
  components (P(mechanism), P(decisive test), sub-claim breakdown), the
  estimation **mode tag** (`base-rate` or `bottom-up`), net EV, and rank.
  No human action required — scoring *is* logging.
- **Outcome filled at status transitions.** When a proposal reaches a terminal
  state (`results_in`, `closed_*`, abandoned/withdrawn), the coordinator fills
  the outcome field as part of the transition: confirmed / refuted /
  abandoned / superseded, with a one-line evidence note. The transition is
  incomplete without it — not a separate chore to remember.
- **Backtests seed it immediately.** Backtest-01 outcomes (aspirin confirmed,
  itraconazole partial) are already known — enter them now.
- **Calibration reads from the ledger.** The calibration checks in this spec
  (did 30% ideas succeed ~30% of the time?) run against ledger entries grouped
  by mode tag. Mode B entries are expected to be worse-calibrated; that is
  fine — the tag makes the difference visible instead of hidden.

Ledger location: `~/workspace/discovery-agents/predictions/ledger.jsonl` — global
across runs (one JSON object per line, append-only), with `run_id` preserving
provenance. Schema in `blackboard-schema.md`.

## Calibration

- Anchored 1–10 scale descriptions + historical reference cases as few-shot anchors.
- Human triage decisions recorded against ranker ordering; systematic
  disagreement → weight/threshold review.
- Backtest mode: check P calibration (did 30% ideas succeed ~30% of the time?),
  not just hit rate. Reads from the prediction ledger, grouped by mode tag.
- Elo pairwise tournaments: deferred upgrade if absolute estimates drift.
