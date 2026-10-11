# Security Policy

## What "security" means for this project

Winnow Institute is a set of agent instructions (Markdown briefs, a pipeline
specification, and scoring rules) — it ships no executable code, servers, or
dependencies. Its safety properties live in the design: a two-tier safety
screen, strict role separation, mandatory citation provenance, and human
gates on every outward action.

The security-relevant failure modes for a project like this are therefore
things like:

- Instructions in the engine, a field pack, or the skill that would let an
  agent bypass the safety screen or a human gate.
- Prompts or briefs that weaken the Tier 1 categorical exclusions
  (WMD enablement, information hazards, human experimentation,
  self-replicating agents).
- Anything that causes an agent running this system to exfiltrate a user's
  private data or act outside its operator's instructions.

## Reporting a vulnerability

Please report security concerns **privately** by email to
jonathan.l.copeland@gmail.com rather than opening a public issue, so a
weakness in the safety design is not advertised before it is fixed.

This is a one-person project maintained on the maintainer's own time, so
please allow a reasonable window for a response and a fix before any public
disclosure. Reports are read and taken seriously; confirmed weaknesses in
the safety screen or gate design are the highest-priority fixes this
project has.

## Supported versions

Only the `main` branch is maintained. Fixes land there; there are no
release branches to backport to.
