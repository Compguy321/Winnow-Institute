# Pipeline

Stage order. Each stage is a subagent run with its role brief + a filtered
blackboard view. The coordinator advances stages, enforces blindness via
context assembly, and brings human gates to the reviewer.

Knowledge policy: live/current data by default, including web search.
Cutoffs apply only in explicitly declared backtest mode.

```
1. SCOUT ......... reads: brief (+ cutoff in backtest mode)
                   writes: dossier/  (literature, open questions, epidemiology)
2. LEAKAGE CHECK . (backtest only) reads: dossier AND proposal inputs;
                   verifies no post-cutoff knowledge in either. Intake inputs
                   pass decontamination first (amendment 2026-09-28): every
                   quantitative input is tagged period-knowable or
                   hindsight-contaminated; contaminated inputs are replaced
                   with period-plausible estimates (provenance marked) or
                   excluded, and the decontamination log is recorded in the
                   proposal record. Fail = redo with tighter constraints.
3. GENERATOR ..... reads: dossier (full)
                   writes: proposals/*.json sections: hypothesis, claims, literature
4. SAFETY SCREEN . reads: hypothesis+claims; writes: safety_screen.
                   Tier-1 hit = record closed, never proceeds.
5. PRIOR-ART/SCREEN reads: hypothesis+claims+literature; writes: prior_art_check, screen.
                   Fail any knockout gate = record closed (cheap death).
                   Knockout gates: already-proven | plausibility<=2 |
                   feasibility<=2 | impact<=2 (1-10 scales).
                   Correctable pitch errors (amendment 2026-09-28) do not
                   close the record: they are logged in screen.corrections[],
                   corrected figures flow downstream, and the corrections are
                   shown to the human at triage / in the feedback report.
6. CRITIC ........ reads: hypothesis+claims+literature (NOT generator notes,
                   NOT safety/prior-art internals); writes: objections.
7. VERIFIER ...... reads: claims+literature (NOT objections — blind);
                   writes: verdicts[] with per-claim provenance.
                   Two-phase clean-room protocol (amendment 2026-09-28):
                   the coordinator writes an anonymized claims-only
                   verification package (no objections, verdicts, scores,
                   or commentary) and stops; the top-level agent runs the
                   verifier in a FRESH side chat whose transcript never
                   contained any role's output, then merges the returned
                   verdicts (labeled verification_mode: clean-room).
                   In-conversation verifier spawning is NOT blind and must
                   not be labeled as such.
                   Verifier-vs-critic conflict on any claim -> status=escalated,
                   goes to human (Gate 3) instead of auto-resolving.
8. RANKER ........ reads: everything except reviews; writes: scores{}, ev{},
                   tags[], rank, rank_justification. Scoring only — touches
                   no other section. Post-rank: crossover analysis per
                   scoring.md Stage 3 (triggered only; writes crossover{}).
                   At score time, appends the prediction-ledger entry
                   (scoring.md: Prediction ledger) — scoring IS logging.
9. GATE 1 TRIAGE . human (reviewer role). Express mode (solo testing):
                   auto-advance top-M by net EV to protocol stage.
10. PROTOCOL ..... reads: triaged proposals; writes: protocol{}.
11. GATE 2 ....... human pre-handoff approval per protocol (approve/reject/revise).
12. LIAISON ...... reads: approved; writes: digest/ (personal-digest mode:
                   top-N by net EV, default N=5) or handoff packets
                   (institute mode — future).
13. GATE 4 ....... human publication approval before anything goes public.
```

## Blindness rules (enforced by filtered views)

- Critic never sees generator's scratch reasoning — proposal record only.
- Verifier blindness is structural only via the clean-room protocol
  (amendment 2026-09-28): fresh side chat, anonymized claims-only package.
  A verifier spawned inside the main conversation inherits the transcript
  and is NOT blind — label its output accordingly, never as blind.
- Ranker sees everything except reviews; writes scores only.
- No agent sees another agent's private notes; the blackboard record is the
  complete shared state.

## Language convention

- Agents recommend hypotheses be **advanced**, **investigated**, or **pursued** —
  never **funded** or **invested in**, unless the run brief explicitly puts real
  funding decisions in scope. The default assumption is that no money changes
  hands; "program cost" in the EV math is opportunity cost, not a bill.
- **ASCII-safe scientific notation.** Write isotope and unit notation in plain
  ASCII so it renders on any device: `89Zr` (not `⁸⁹Zr`), `[18F]` (not `[¹⁸F]`),
  `1x10^12` (not `1×10¹²`), `mg/m2` (not `mg/m²`). Unicode superscripts and
  subscripts do not render reliably on all screens.
- **Expand acronyms on first use.** The first time an acronym appears in any
  human-read report (digest, feedback report, protocol, review), write the full
  term followed by the acronym in parentheses — e.g. "non-human identity
  (NHI)", "short-lived token (SLT)". The acronym alone is fine thereafter.
  Never assume the reviewer knows an acronym, even a common one in the field.

## Status flow

draft -> screened -> criticized -> verified -> ranked -> triaged -> protocol
-> approved -> handed_off -> results_in. Terminal failures: closed_tier1,
closed_screen. Escalations: escalated (awaiting human).

**Ledger rule.** A transition into any terminal state (`results_in`,
`closed_*`) or a withdrawal/supersede is incomplete until the coordinator
fills the `outcome` field of that proposal's prediction-ledger entry
(confirmed / partial / refuted / abandoned / superseded + one-line evidence note).
The prediction was logged automatically at rank time; only the outcome needs
a human-attested closeout, and the workflow requires it.
