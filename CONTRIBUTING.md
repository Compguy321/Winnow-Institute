# Contributing to Winnow Institute

Thank you for being here. Winnow's whole premise is that claims should be
checked, not trusted — contributions are held to the same standard the
engine applies to hypotheses.

## Ways to contribute

- **Run it and report back.** The most valuable contribution right now is
  evidence: install the skill (see the README's Quick start), run a
  discovery cycle or score an idea, and open an issue describing what
  happened — especially where the pipeline was wrong, sloppy, or unclear.
  Use the "Run feedback" issue template and include your run's records if
  you can share them.
- **Field packs.** New domains are welcome. A field pack adapts the
  field-agnostic engine to a discipline: its literature sources, its
  value unit, and its domain-specific safety considerations. Look at
  `packs/` for the existing examples before starting one.
- **Engine improvements.** Role briefs, pipeline stages, scoring rules,
  and the blackboard schema all live in `engine/` (and are mirrored in
  `skills/discovery-agents/references/` — see "Keep the copies in sync"
  below). Propose changes via pull request with a clear rationale.
- **Documentation fixes.** If the README or any instruction is wrong,
  ambiguous, or out of date, a correction is a real contribution.

## Ground rules

1. **Claims need provenance.** If your contribution asserts a fact about
   the world (a citation, a benchmark, a prior-art claim), cite a primary
   source. The project's verifier rule applies to humans too: a reference
   must actually resolve to the work it is cited for.
2. **Do not weaken the safety design casually.** Changes to the safety
   screen (`engine/safety.md`), the Tier 1 exclusions, role separation,
   or the human gates need an explicit justification in the pull request
   and will get the closest review this project gives anything.
3. **No hype in either direction.** Describe changes by what they
   demonstrably do. "Improves scoring" is not a description; "adds a
   worked example showing the EV arithmetic for a knocked-out idea" is.
4. **Keep the copies in sync.** The engine exists twice in this repo:
   `engine/` (the design reference) and `skills/discovery-agents/`
   (the installable skill, whose `references/` mirror the engine files).
   If you change one, change the other in the same pull request, or say
   in the PR why the change is intentionally one-sided.
5. **Human gates stay human.** Nothing in a contribution should make the
   system publish, send, or hand off work without its operator's explicit
   approval.

## Pull requests

- One change per PR, with a short description of what changed and why.
- If you ran the pipeline before/after your change, say what differed.
- The PR template has a short checklist — it exists because each item on
  it has caught a real problem at least once.

## Conduct

Participation is covered by the [Code of Conduct](CODE_OF_CONDUCT.md).

## A note on scale

This is a one-person project maintained on the maintainer's own time.
Reviews and replies may take a while. Careful, well-evidenced
contributions are the ones most likely to be merged quickly.
