# Field Pack: Cyber Defense Technologies

Field pack #2. Everything here is cyber-defense-specific; the engine
(`engine/`) stays field-agnostic.

## Focus
Novel defensive cybersecurity technologies that fit within a defense-in-depth
strategy: prevention, detection, response, and recovery controls. The wedge is
defense: every proposal must make some class of defender strictly better off.

## Hard safety boundary (Screener — non-negotiable)
- DEFENSIVE ONLY. Any proposal whose primary effect is offensive capability
  (exploitation, intrusion tooling, weaponized malware, access-control bypass
  as an end in itself) is a Tier-1-equivalent knockout.
- Dual-use screen: techniques with inherent offensive application (e.g.,
  detection-evasion research, novel attack primitives) are knocked out unless
  the defensive framing is load-bearing and the offensive enablement is
  negligible or already public.
- No non-consensual surveillance: proposals that depend on monitoring people
  without consent are knocked out (workplace/network-owner-consented
  monitoring in enterprise contexts is in scope; anything broader is not).
- No proposals that weaken existing security for others (e.g., mandated
  backdoors, key escrow as a feature).

## Scout sources (priority order)
1. Peer-reviewed venues: IEEE S&P, USENIX Security, ACM CCS, NDSS, ACSAC
   (proceedings papers — primary source)
2. arXiv cs.CR (preprints — flagged as such)
3. MITRE ATT&CK (threat landscape) and MITRE D3FEND (defensive techniques;
   also the novelty check: what's already catalogued)
4. NIST SP 800-series, CISA advisories and binding operational directives
   (baseline practice: what defenders already do)
5. Vendor research blogs / whitepapers (weak support only — marketing filter)

## Evidence standards (Verifier)
- `supported` requires primary source; vendor whitepapers and blog posts
  count as weak support only.
- Evaluations on synthetic benchmarks alone → real-world effectiveness
  capped at "untested" unless validated on operational data or red-team
  exercises.
- "Deployed at scale by industry" claims require a named deployment or
  primary report; otherwise the already-proven knockout does not trigger.

## Impact estimation (Ranker)
- Value measure (pack declaration):
  - `value_unit`: USD averted loss / year vs. current standard of care (the
    control stack a competent enterprise already runs)
  - `display_default`: native
  - `conversion_to_qaly`: flat $100,000 per QALY-eq. Conservative; ignores
    diminishing marginal utility of money (corporate losses convert at the same
    rate as individual welfare — likely overstates QALY-eq); US-centric threshold.
- Estimate value FIRST in native USD as a range, never a point (e.g.,
  breach-cost studies, ransomware impact data), then convert via the rule above.
  State the conversion and its uncertainty in `work_shown`; never bake it in
  silently.
- Order-of-magnitude bins only on the QALY-eq figure; matched granularity on
  the native figure. Display both: "~$10–30M/yr ≈ 100–300 QALY-eq".
- Program cost includes engineering effort, deployment friction, and
  false-positive burden on defenders — estimated natively, converted the same way.

## Protocol templates
- Phase: cheapest decisive test first — typically lab evaluation on
  representative workloads/traffic → red-team exercise → limited operational
  pilot. State which stage the protocol targets. No live-fire testing on
  third-party systems, ever.

## Veto tuning
- The already-proven knockout should be aggressive here: cybersecurity
  re-invents wheels constantly. MITRE D3FEND + vendor landscape is the
  prior-art check.
- Extra scrutiny for proposals touching cryptography: "novel crypto"
  designs are implausible-by-default unless the mechanism argument is
  airtight (history: most novel crypto is broken).
- Extra scrutiny for AI-for-detection claims: benchmark-only evidence is
  the norm and usually does not transfer; demand operational validation.
