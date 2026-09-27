# Pipeline

Stage order. Each stage is a subagent run with its role brief + a filtered
blackboard view. The coordinator advances stages, enforces blindness via
context assembly, and brings human gates to the reviewer.

Knowledge policy: live/current data by default, including web search.
Cutoffs apply only in explicitly declared backtest mode.

```
1. SCOUT ......... reads: brief (+ cutoff in backtest mode)
                   writes: dossier/  (literature, open questions, epidemiology)
2. LEAKAGE CHECK . (backtest only) reads: dossier; verifies no post-cutoff
                   knowledge. Fail = redo scout with tighter constraints.
3. GENERATOR ..... reads: dossier (full)
                   writes: proposals/*.json sections: hypothesis, claims, literature
4. SAFETY SCREEN . reads: hypothesis+claims; writes: safety_screen.
                   Tier-1 hit = record closed, never proceeds.
5. PRIOR-ART/SCREEN reads: hypothesis+claims+literature; writes: prior_art_check, screen.
                   Fail any knockout gate = record closed (cheap death).
                   Knockout gates: already-proven | plausibility<=2 |
                   feasibility<=2 | impact<=2 (1-10 scales).
6. CRITIC ........ reads: hypothesis+claims+literature (NOT generator notes,
                   NOT safety/prior-art internals); writes: objections.
7. VERIFIER ...... reads: claims+literature (NOT objections — blind);
                   writes: verdicts[] with per-claim provenance.
                   Verifier-vs-critic conflict on any claim -> status=escalated,
                   goes to human (Gate 3) instead of auto-resolving.
8. RANKER ........ reads: everything except reviews; writes: scores{}, ev{},
                   tags[], rank, rank_justification. Scoring only — touches
                   no other section.
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
- Verifier never sees objections before writing verdicts.
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

## Status flow

draft -> screened -> criticized -> verified -> ranked -> triaged -> protocol
-> approved -> handed_off -> results_in. Terminal failures: closed_tier1,
closed_screen. Escalations: escalated (awaiting human).
