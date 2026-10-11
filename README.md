Winnow Institute — an AI research institute that takes nobody's word for it. An open, field-agnostic engine for multi-agent scientific discovery: agents that generate hypotheses, red-team them, verify claims against primary sources, and rank by expected value, with a human holding every gate.

**Winnow Institute is now open source: an AI research institute that takes nobody's word for it.**

I'm Jonathan Copeland, a computer scientist. For the past few weeks I've been building Winnow Institute — a team of AI agents, running in Muse, that works like a small research institute with deliberately separated jobs:

- **Scout and generator** agents develop research hypotheses.
- A **critic** agent red-teams them.
- A **verifier** agent independently checks every atomic claim against primary sources, with citations.
- A **ranker** scores the survivors by expected value, showing its arithmetic.
- A **protocol writer** turns what survives into testable experiments with pre-registered falsification criteria — the exact result that would kill the idea, written down in advance.

I hold four human gates. Nothing is published, sent, or handed off without my explicit approval. It works in both directions: it generates its own ideas, and it evaluates ideas submitted to it, claim by claim, the same way.

It is field-agnostic — the engine doesn't care what science it's pointed at. Its first field pack targets cancer drug repurposing, because that's where the need is most urgent. A second pack covers cyber-defense technology scouting.

Honest status, because this project is about not taking anyone's word for it — including mine: it has run one backtest (with knowledge cut off at the end of 2009, it rediscovered aspirin's colorectal-cancer prevention benefit at rank #1; a second target was a partial hit with the wrong mechanism). Its probability estimates are uncalibrated. And everything it produces is **untested** until a real laboratory tests it. The engine is the brain; it has no hands.

Since the backtest, the engine's top-ranked live proposal has been taken up in discussion with working cancer researchers, and its first test may run on real laboratory data. The components are proven; the combination is untested.

**How to use it:** If you use Muse, copy the `skills/discovery-agents/` folder into your workspace's skills folder and ask Muse to run a discovery cycle or score your idea. The engine also works with any capable agent setup, or as a design reference — the ideas (independent verification with mandatory provenance, pre-registered falsification, expected-value ranking, human gates) port to any serious research-evaluation workflow.

It's free and open under the MIT license, because the mission — curing cancer and advancing science — matters more than commercial potential. If it helps you and you'd like to show appreciation, donations are welcome via PayPal to jonathan.l.copeland@gmail.com.

[Repo link goes here once the GitHub repo exists.]

*Produced by the Winnow Institute — a team of AI agents powered by Muse
