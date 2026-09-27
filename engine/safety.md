# Safety

Two-tier system. Tier 1 is checked at the SAFETY SCREEN stage (early, before
expensive work). Tier 2 is computed by the Ranker. Both can kill a proposal.

## Tier 1 — Categorical exclusions (never pursued, no EV calc)

Defined by property, not field, so they port to every field pack:

1. Materially enabling weapons of mass destruction — biological, chemical,
   nuclear/radiological, or cyber-physical attacks on critical infrastructure.
2. Information hazards: methods whose broad dissemination foreseeably causes
   net harm even when the research intent is benign.
3. Non-consensual human experimentation, or violation of established research
   ethics (e.g., Declaration of Helsinki).
4. Uncontained release of self-replicating or persistent agents — pathogens,
   engineered organisms, large-scale environmental interventions.

The veto list is user-editable for additions; the core above is non-removable.
A Tier-1 hit closes the record immediately (`closed_tier1`) with the reason
recorded. Field packs may tune wording; they may not narrow the core.

## Tier 2 — Net-EV nogo

Net EV < 0 → automatic nogo. The human reviewer may reinstate only with a
written rationale appended to `reviews[]` (accountability, not a quiet override).

## Uncertainty guardrail

For severity estimates above the catastrophic threshold (≥100K QALYs), a
low-confidence P(harm) estimate is itself a nogo — escalate to human instead
of passing on "tiny but unsure." The equation cannot be trusted precisely
where it matters most.

## Notes for the cancer-repurposing pack

Repurposing approved drugs is inherently bounded-risk: known safety profiles,
phased clinical trials. The residual risk term will usually be small — the
formula handles this naturally, no special-casing needed. The main Tier-1
relevance is dual-use screening of mechanisms (e.g., proposals touching
pathogen biology get extra scrutiny).
