# Backtest Protocol — backtest-01

## Purpose
Prove the machine works before it ever proposes something new. Run the full
pipeline retrospectively and check whether it rediscovers known repurposing
successes from pre-cutoff knowledge alone.

## Cutoff
**2009-12-31.** The Scout may use only sources published on or before this
date. All role briefs carry the cutoff; reasoning must come from the dossier,
not from model memory.

## Held-out targets (discoveries AFTER the cutoff — the Scout/Generator must
not know these)
1. **Target A — Aspirin → colorectal cancer prevention.** Pre-cutoff:
   observational signals existed. Post-cutoff proof: Rothwell et al., Lancet
   2010/2011 (20-year follow-up of cardiovascular aspirin trials showing
   reduced CRC incidence/mortality).
2. **Target B — Itraconazole (antifungal) → anti-cancer via hedgehog pathway
   inhibition.** Post-cutoff: Kim et al., ACS Chemical Biology 2010.

The coordinator holds these targets; no role agent is told them.

## Leakage control
1. Scout writes a leakage attestation (cutoff, search method, exclusion steps).
2. Coordinator audits the dossier for post-cutoff references before generation.
3. Known limitation (recorded honestly): role agents run on models whose
   training includes post-cutoff knowledge. Mitigation: briefs require
   reasoning strictly from the dossier; any claim not traceable to the dossier
   is flagged by the Verifier as untested. This limitation bounds how
   strongly a positive result can be interpreted.

## Success criteria
- **Primary (rediscovery):** do the held-out targets — or mechanistically
  equivalent hypotheses — appear in the Ranker's top-N? (N=5, the digest size.)
- **Secondary (calibration):** are the Ranker's P(success) estimates
  well-calibrated against known outcomes in the retrospective set?
- **Process:** did every knockout gate, role-separation rule, and human gate fire
  as designed? (Audit the blackboard.)

## Run config
- Generator quantity: 8–12 hypotheses.
- Triage: express mode, M=6 auto-advance by net EV.
- Liaison digest: N=5.
- Human gates: Gate 1 express (auto), Gate 2/3/4 live with the user.
