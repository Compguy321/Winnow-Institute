# Pipeline variant: Score-my-idea

Interactive mode: the user submits a hypothesis in plain language and gets a
full scoring + feedback report. Reuses the batch pipeline's roles from the
Safety Screen onward; the user replaces Scout and Generator.

```
0. INTAKE ........ reads: user's free-text idea
                   writes: draft proposal (hypothesis, claims; no literature)
                   GATE 0: user confirms or corrects the structuring.
1. SAFETY SCREEN . as in pipeline.md (Tier-1 hit = refused with reason).
2. SCREEN ........ as in pipeline.md (knockout gates; fail = closed with
                   feedback explaining which gate and why).
3. CRITIC ........ as in pipeline.md (filtered view: hypothesis+claims only).
4. VERIFIER ...... as in pipeline.md (blind; claims only; LIVE knowledge —
                   no cutoff in this mode, current literature applies).
5. RANKER ........ as in pipeline.md (full EV scoring + tags).
6. FEEDBACK ..... coordinator composes the feedback report (below) and
                   delivers it to the user. No digest, no handoff.
```

## Blindness
Same filtered-view enforcement as the batch pipeline. The Intake's structuring
notes are not shown to Critic/Verifier (they'd anchor them); only the confirmed
proposal record is.

## The feedback report
Delivered to the user, containing:
1. **Verdict up front**: net EV + one-paragraph plain-language assessment.
2. **EV breakdown**: every component with its justification (from Ranker
   work_shown) — the user should see *why*, not just the number.
3. **Per-claim verdicts**: supported / contradicted / untested with
   provenance. Contradicted claims highlighted.
4. **Strongest objections**: the Critic's best 2–3, in plain language.
5. **What would change the score**: the single most valuable next evidence —
   e.g. "a pre-registered cohort study showing X would move p_mechanism
   from 0.15 to 0.4".
6. **Nearest novel variant** (when the idea fails the novelty gate): the
   closest adjacent hypothesis that isn't already proven, with why it's
   distinct. This is the killer feature — never just say "already done."
7. **Suggested next step**: revise-and-rescore, request a protocol draft
   (Protocol Writer as opt-in follow-up), or park it.

## Notes
- Prospective mode: ideas are scored against current knowledge. There is no
  backtest cutoff here.
- A user idea that hits Tier 1 is refused plainly, with the reason — the
  same standard as generated hypotheses.
- Repeated submissions are independent runs; the blackboard keeps each
  proposal's full record for comparison.
