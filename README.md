# Winnow Institute

*An AI research institute that takes nobody's word for it.*

Winnow Institute is an open, field-agnostic engine for **multi-agent scientific
discovery**: a team
of AI agents that generates research hypotheses, red-teams them against the
literature, independently verifies their claims against primary sources,
ranks them by expected value, and
drafts testable protocols — with a human reviewer holding every gate.

It was built by Jonathan Copeland, a computer scientist, as a general
scientific-discovery engine; its first field pack targets **cancer drug
repurposing**, because that is where the need — and the potential good — is
most urgent. A second pack covers **cyber-defense technology scouting**.

## How it works

Ten roles, one append-only blackboard, strict role separation (each agent works
from its brief and the record sections its job needs), and four human gates:

| Stage | Role | Job |
|---|---|---|
| Intake | Idea structuring | Turns a plain-language hypothesis into a structured, scorable proposal (score-my-idea mode) |
| Scout | Literature scout | Builds the dossier the pipeline reasons from |
| Generator | Hypothesis generator | Proposes testable hypotheses from the dossier |
| Screener | Safety + knockout screen | Kills unsafe or clearly-dead ideas cheaply |
| Critic | Red team | Attacks each hypothesis with cited evidence |
| Verifier | Independent fact-checker | Checks every atomic claim against primary sources, with cited provenance for every verdict |
| Ranker | Scorer | Knockout gates, then net expected value — estimated in field-native units, ranked in QALY-equivalents |
| Protocol Writer | Experimentalist | Turns survivors into falsifiable protocols |
| Liaison | Delivery | Digests and handoff packets |
| Coordinator | Orchestrator | Runs the pipeline, enforces contracts, brings human gates |

Surviving hypotheses are scored by **net expected value**:

```
Net EV = P(success) × Value(good) − P(harm) × Severity(harm) − program cost
```

denominated in QALY-equivalents, where `P(success) = P(mechanism real) ×
P(decisive test)`. Every protocol carries **pre-registered falsification
criteria**: the exact result that would kill the hypothesis.

Safety is two-tier: categorical exclusions (WMD enablement, information
hazards, non-consensual human experiments, uncontained self-replicating
agents) close a proposal immediately; negative net EV is an automatic nogo.

## Backtest-01 (first validation)

To test whether the engine can find anything real, it was run with knowledge
cut off at December 31, 2009, against two held-out targets from the
pre-2010 literature: aspirin's colorectal-cancer prevention benefit and
itraconazole's anticancer activity. Of 10 generated hypotheses, an independent
verifier checked 44 atomic claims (43 supported, 1 contradicted, 0 untested).
Aspirin was rediscovered at **rank #1** (net EV 297,400 QALY-equivalents);
itraconazole was a partial hit at rank #8 with the wrong mechanism. One cycle,
two targets — encouraging, not conclusive.

## Honesty box

This is a **research prototype**, not a validated platform:
- One backtest cycle and one live run; the probabilities are **uncalibrated**.
- Every hypothesis the engine produces is **untested** — it needs real-world
  experimental verification by real laboratories. The engine is the brain;
  it has no hands.
- Treat scores as decision-support, not verdicts. The human reviewer is the
  decision-maker at every gate, by design.

## How to use it

**Option A — with the Muse skill (recommended).** Install the
`discovery-agents` skill in your Muse workspace and ask it to run a discovery
cycle or score your idea. The skill carries the full engine.

**Option B — with any capable agent.** Hand this repository to an AI agent
that can spawn subagents, browse the literature, and write files. Start it at
`engine/pipeline.md` for batch discovery or
`engine/pipeline-score-my-idea.md` to score a single hypothesis, then follow
the role briefs in `engine/roles/`. The blackboard schema is in
`engine/blackboard-schema.md`.

**Option C — as a design reference.** Steal the ideas: independent verification
with mandatory provenance,
pre-registered falsification, EV ranking, human gates. They port to any
serious research-evaluation workflow.

Field packs live in `packs/`; the engine itself (`engine/`) is field-agnostic.
`packs/cancer-repurposing/` defines the scout sources, evidence standards, and
protocol templates for repurposing approved drugs against cancer;
`packs/cyber-defense/` does the same for defensive cybersecurity technologies,
with a hard defensive-only safety boundary. Write your own pack for your field.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, improve it. If you build on
this, a citation or a note back would be appreciated but is not required.

## Support

This project is free and open because the mission — curing cancer and
advancing science — matters more than commercial potential. If it helped you
and you'd like to show appreciation, donations are welcome via PayPal to
**jonathan.l.copeland@gmail.com**. Every contribution goes toward continuing
this work.
