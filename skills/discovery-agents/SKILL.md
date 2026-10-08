---
name: "discovery_agents"
description: "Run a multi-agent scientific discovery pipeline: generate research hypotheses, red-team them, independently verify claims against primary sources, rank by expected value, and draft test protocols. Use when the user wants to brainstorm scientific ideas ('brainstorm new potential cures for Alzheimer's'), evaluate an idea ('evaluate my idea: ...'), or score a hypothesis."
---

# Discovery Agents

## Purpose
Run a rigorous, auditable multi-agent pipeline that turns a research area (or a
single user idea) into ranked, falsifiable, protocol-ready hypotheses — with a
human reviewer holding every gate.

## Workflow

Two modes. **Batch** (new hypotheses): run the 13 pipeline stages in order —
Scout → Leakage Check (backtest only) → Generator → Safety Screen → Prior-Art
Screen → Critic → Verifier → Ranker → **Gate 1 Triage (human)** → Protocol
Writer → **Gate 2 Pre-handoff (human)** → Liaison → **Gate 4 Publication
(human)**. **Score-my-idea** (user's hypothesis): Intake (user confirms the
structuring — Gate 0) → Safety Screen → Screen → Critic → Verifier → Ranker →
feedback report.

Read `references/pipeline.md` for the full stage spec and
`references/pipeline-score-my-idea.md` for the interactive mode. Read
`references/roles/<role>.md` before spawning each role.

To run a stage: spawn a subagent, hand it the role brief from
`references/roles/` plus the record sections its job needs. You are the
Coordinator: advance stages, enforce append-only writes, run mechanical
checks (status transitions, leakage in backtest mode), and bring each human
gate to the reviewer with a tight evidence packet. Read
`references/roles/coordinator.md`.

Set up one blackboard record per hypothesis per `references/blackboard-schema.md`
(`draft → screened → criticized → verified → ranked → triaged → protocol →
approved → handed_off → results_in`; terminal: `closed_tier1`, `closed_screen`;
`escalated` awaits human).

## Output Contract
- Batch: a digest of the top-N ranked proposals (default N=5), each with rank,
  net EV + component breakdown, plain-language summary, key claim verdicts,
  protocol sketch, falsification criteria, and the moonshot (high-risk,
  high-reward) list separately.
- Score-my-idea: a feedback report — verdict up front, EV breakdown,
  per-claim verdicts, strongest objections, what would change the score, the
  nearest novel variant if the novelty gate failed, and a suggested next step.
- Every run leaves a run log: what ran, when, and what the human decided.

## Operating Rules
1. **Knowledge policy:** live/current data (including web search) is the
   default. Historical cutoffs apply only when the run brief explicitly
   declares backtest mode — then enforce them strictly.
2. **Safety, two tiers** (`references/safety.md`): Tier-1 categorical
   exclusions (WMD enablement, information hazards, non-consensual human
   experiments, uncontained self-replicating agents) kill a proposal early,
   no EV calc. Negative net EV is an automatic nogo. Catastrophic severity
   with poorly known probability escalates to the human instead of relying
   on the arithmetic.
3. **Scoring** (`references/scoring.md`): knockout gates first (already
   proven, implausible mechanism, no feasible experiment, zero/negative
   marginal impact); survivors get net EV =
   `P(success) × Value(good) − P(harm) × Severity(harm) − program cost`
   in QALY-equivalents, with `P(success) = P(mechanism real) ×
   P(decisive test)`. Show the work; no number without reasoning.
4. **Human gates are default-deny.** Nothing advances past triage, pre-handoff,
   escalation, or publication without the reviewer's explicit approval.
   Escalate verifier/critic disagreements; never auto-resolve them.
5. **Role separation, not blindness.** Critic never sees generator's scratch
   reasoning; verifier checks each claim against primary sources with
   mandatory provenance (no verdict without a cited source). Independence
   plus cited sources is the control — no blindness claim is made.
6. **Language:** hypotheses are *advanced / investigated / pursued* — never
   *funded* (unless the run brief puts real funding decisions in scope).
   Claims with no published test are *untested*, not "unverifiable."
7. **Notation:** ASCII-safe scientific notation (`89Zr`, `[18F]`, `1x10^12`,
   `mg/m2`) — no Unicode superscripts/subscripts.
8. Verifier citation hygiene: every DOI must resolve to the intended paper;
   never cite press coverage as the paper; never use piracy links.

## First-Run Greeting

When a user invokes this skill for the first time (or asks what it can do),
greet them with the following, adapted to the conversation. Do not run any
pipeline stage until they give you an idea or a research direction.

> **Winnow Institute** — a team of AI agents that pressure-tests scientific
> ideas instead of taking anyone's word for them. Two ways to use it:
>
> - **Score my idea** — *"Evaluate my idea: [describe it in plain language]."*
>   You'll confirm the structured version, then it runs a safety screen, a
>   red-team critic, an independent claim verifier, and an expected-value
>   rank, and hands you a feedback report.
> - **Brainstorm** — *"Brainstorm new potential cures for [disease]"* or
>   *"Generate hypotheses for [problem] in [field]."* It scouts the
>   literature, generates hypotheses, and runs each through the same gauntlet.
>
> How it works: ten specialist roles argue over the idea on a shared
> blackboard, and you hold four gates — triage, protocol approval,
> escalation calls, and publication. Nothing leaves the workspace without
> your explicit say-so.
>
> Fair warning: the probability numbers are rough bottom-up estimates, not
> calibrated forecasts — trust the ranking more than the exact values.
> "Untested" means no published test was found, not that it can't be
> tested. Every claim carries its sources; you're encouraged to check them.

Example prompts you can suggest if they hesitate:
- "Evaluate my idea: a patch that releases insulin when blood sugar spikes."
- "Brainstorm new potential cures for pancreatic cancer."
- "Generate hypotheses for slowing antibiotic resistance in hospitals."
