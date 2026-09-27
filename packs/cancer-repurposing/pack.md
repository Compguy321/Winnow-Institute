# Field Pack: Cancer Drug Repurposing

Field pack #1. Everything here is cancer-repurposing-specific; the engine
(`engine/`) stays field-agnostic.

## Focus
Approved non-oncology drugs with signals suggesting anti-cancer activity.
Repurposing is the wedge: known safety profiles, fast validation, legible
claims a non-expert reviewer can check.

## Scout sources (priority order)
1. PubMed / PMC (primary literature, systematic reviews, meta-analyses)
2. bioRxiv / medRxiv (preprints — flagged as such)
3. ClinicalTrials.gov (trial landscape: what's already being tested)
4. DrugBank / repoDB (drug–indication mappings; what's already known)
5. SEER (epidemiology: incidence, mortality by indication — for impact bins)
6. FDA labels / DailyMed (approved indications, safety profiles)

## Evidence standards (Verifier)
- `supported` requires primary source; preprints count as weak support only.
- Observational/epidemiological signals (e.g., "diabetics on metformin show
  lower cancer incidence") support plausibility but never mechanism alone.
- In-vitro-only evidence → mechanism claims capped at "untested" unless
  corroborated in vivo or clinically.

## Impact data
- SEER incidence/mortality per cancer type (note year).
- Standard-of-care baseline: what happens to these patients today.
- Impact bins are MARGINAL vs standard of care, order-of-magnitude only.

## Protocol templates
- Phase: cheapest decisive test first — typically in-vitro dose-response in
  relevant cell lines → in-vivo xenograft → retrospective EHR analysis where
  feasible. State which stage the protocol targets.

## Veto tuning
- Repurposing approved drugs is inherently bounded-risk (known safety, phased
  trials). Residual risk term will usually be small — no special-casing.
- Extra scrutiny for proposals touching pathogen biology (dual-use screen).
- Teratogenicity flags (e.g., thalidomide-class): protocols must include
  pregnancy-exclusion controls explicitly.
