# Blackboard Schema

One JSON record per hypothesis. File: `cycles/<run-id>/proposals/<id>.json`.
Agents append to their own sections only. Sections they may not write are
simply absent from their filtered view.

```json
{
  "id": "prop-001",
  "field_pack": "cancer-repurposing",
  "status": "draft | screened | criticized | verified | ranked | triaged | protocol | approved | handed_off | results_in",
  "hypothesis": {
    "title": "one-line",
    "statement": "full hypothesis",
    "mechanism": "proposed biological mechanism",
    "predictions": ["testable prediction 1", "..."]
  },
  "claims": [
    {"id": "c1", "text": "atomic factual claim", "supports": "which part of hypothesis"}
  ],
  "literature": [
    {"citation": "...", "relevance": "...", "url": "..."}
  ],
  "prior_art_check": {
    "already_proven": false,
    "closest_prior_work": "...",
    "novelty_note": "..."
  },
  "safety_screen": {
    "tier1_hit": false,
    "tier1_detail": "...",
    "residual_risk_note": "..."
  },
  "objections": [
    {"claim_id": "c1", "objection": "...", "counter_evidence": "...", "status": "open | answered | escalated"}
  ],
  "verdicts": [
    {"claim_id": "c1", "verdict": "supported | contradicted | untested",
     "provenance": [{"source": "...", "quote": "...", "url": "..."}]}
  ],
  "screen": {
    "decision": "pass | fail",
    "failed_gate": "novelty | plausibility | feasibility | impact | safety | none",
    "note": "..."
  },
  "scores": {
    "novelty": 1, "plausibility": 1, "testability": 1, "impact": 1, "feasibility": 1
  },
  "ev": {
    "p_mechanism": 0.0,
    "p_decisive_test": 0.0,
    "p_success": 0.0,
    "estimation_mode": "base-rate | bottom-up",
    "base_rate_note": "reference class + rate, or why none exists (mode B)",
    "sub_claims": [
      {"claim": "...", "p": 0.0, "basis": "verdict ids / rubric range"}
    ],
    "binding_constraint": "which sub-claim most limits P(mechanism)",
    "p_test_feasible": 0.0,
    "p_test_interpretable": 0.0,
    "impact_bin": "10s | 100s | 1K | 10K | 100K | 1M+",
    "impact_qaly": 0,
    "value_native": [0, 0],
    "value_unit": "pack-declared native unit",
    "conversion_to_qaly": "pack rule + one-line uncertainty note",
    "display_default": "native | qaly",
    "p_harm": 0.0,
    "severity_qaly": 0,
    "program_cost_qaly": 0,
    "net_ev_qaly": 0.0,
    "work_shown": "why each number; 2-4 sentences per component"
  },
  "tags": ["high-risk-high-reward"],
  "rank": 1,
  "rank_justification": "...",
  "protocol": {
    "objective": "...",
    "methods": "...",
    "controls": "...",
    "sample_size": "...",
    "expected_outcomes": "...",
    "falsification_criteria": "...",
    "est_cost": "...",
    "est_duration": "..."
  },
  "reviews": [
    {"gate": "triage | pre_handoff | escalation | publication",
     "reviewer_role": "user | domain_expert | panel",
     "decision": "approve | reject | revise",
     "rationale": "...",
     "timestamp": "..."}
  ]
}
```

## Dossier (Scout output)

File: `cycles/<run-id>/dossier/dossier.md` — literature survey: key papers
(with dates), findings, open questions, contradictions, epidemiology numbers
for impact estimation, and (in backtest mode) the cutoff date + leakage attestation.

## Prediction ledger

File: `~/workspace/discovery-agents/predictions/ledger.jsonl` — global across
runs, one JSON object per line, append-only. Written by the ranker at score
time; outcome filled by the coordinator at terminal status transitions.

```json
{"proposal_id": "cyb-010", "run_id": "run-003-cyber-defense",
 "date_scored": "2026-09-27", "p_success": 0.60,
 "p_mechanism": 0.75, "p_decisive_test": 0.80,
 "estimation_mode": "base-rate | bottom-up",
 "net_ev_qaly": 159.0, "rank": 2,
 "outcome": null,
 "outcome_date": null, "outcome_note": null}
```

`outcome`: `confirmed | partial | refuted | abandoned | superseded` — filled when the
proposal reaches `results_in`, `closed_*`, or is withdrawn. A terminal
transition without an outcome entry is incomplete.
