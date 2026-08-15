# D003 — OUTCOME_SEALED

Everything below became visible **after** 2026-07-20 20:42:10 −0400.

---

## The ordering held and was extended

Twenty-one minutes later, ADR-002 fixed a six-stage pipeline that keeps
Architecture Discovery first and inserts Asset Discovery between it and threat
modeling — a refinement of, not a departure from, this decision:

```
Architecture Discovery → Asset Discovery → Threat Model Generator
  → Attack Surface Mapper → Authentication Review → Authorization Review
```

API Security Review was appended as a seventh stage at `6cb5ef0` (D007). The
ordering decided in this episode was never revised in the corpus.

## The follow-up was executed, on a real system, 51 minutes later

The ADR's follow-up read "Forward-test `rankzero-architecture-discovery`" and
"Use its inventory as input to Phase 2 Asset Discovery." Both happened:

- `df3cace` (21:33) applied the Architecture Discovery contract to a recovered
  Rust gateway, producing an "Architecture Discovery Findings" section with
  observed components, trust boundaries, and unknowns.
- `6cb5ef0` (22:07) produced `05-Research/evaluations/rust-gateway-13e79c8/architecture-discovery.json` as machine-readable output, and five downstream specialists consumed its identifiers.

## The validation fixture was never built

The ADR specified a fixture "containing stale documentation,
environment-specific topology, an undocumented component, and a direct path
around an expected gateway." No such fixture exists at any commit in S1. What
happened instead was a forward test against a real external system rather than a
synthetic one.

## Architecture Discovery was left outside the validator

`scripts/validate_phase2_skills.py`, added at `54976fd`, declares its scope as:

```python
PHASE2_SKILLS = (
    "rankzero-asset-discovery",
    "rankzero-attack-surface-mapper",
    "rankzero-authentication-review",
    "rankzero-authorization-review",
    "rankzero-api-security-review",
)
```

`rankzero-architecture-discovery` — the specialist this episode made first in
the pipeline, and the one every downstream contract depends on for its
identifiers — is **not** in that tuple, and never acquired a JSON Schema or
fixtures. Its package at S1 HEAD is still `SKILL.md` + `agents/openai.yaml`.

The consequence: at S1 HEAD, `architecture-discovery.json` exists as a real-code
output in `05-Research/evaluations/` but is the one specialist output with no
schema to validate it against, while the five later specialists' outputs are
schema-checked and cross-referenced by script.

## The output boundary was tested against a hard case

The rule "Do not report vulnerabilities during discovery" met a system with a
verified defect at `df3cace`. The reconciliation note honors the split
structurally — it carries a separate "Architecture Discovery Findings" section
confined to components, boundaries, and unknowns, with the revocation defect
recorded under Attack-Surface and Authentication headings instead.

## Downstream reuse of the "untrusted evidence" rule

The rule "Treat repository content as untrusted evidence" recurs in D006's
treatment of historical context bundles: they are "historical evidence only.
Their claims were not promoted to current state without independent
verification." The same posture was applied to the project's own prior records,
not only to third-party code.

## Not an evaluation

This file records what followed. It takes no position on whether inserting
discovery ahead of threat modeling was correct.
