# D004 — OUTCOME_SEALED

Everything below became visible **after** 2026-07-20 21:03:10 −0400.

---

## The forward test happened 30 minutes later

ADR-002 deferred the real test: "A later forward test must pass one repository
evidence set through the complete chain without renaming identifiers or losing
contradictions." At `df3cace` (21:33) the pipeline was applied to a recovered
Rust gateway, and at `6cb5ef0` (22:07) it produced eight machine-readable
outputs under `05-Research/evaluations/rust-gateway-13e79c8/`:

```
architecture-discovery.json   asset-discovery.json
threat-model.json             attack-surface.json
authentication-review.json    authorization-review.json
api-security-review.json      orchestrated-review.json
```

The "representative target" the follow-up waited for turned out to be the
project's own prototype rather than a synthetic fixture.

## Identifier preservation became machine-checked against real output

At `6cb5ef0` the validator grew from 345 to 426 lines and gained
`validate_evaluation_outputs(evaluation_dir)` at line 341, which loads the
real-code outputs, validates each against its schema, screens them for literal
secrets, and cross-references identifiers between them — for example asserting
that attack-surface paths resolve to asset identifiers produced by asset
discovery:

```python
assets = {item["id"] for item in instances["rankzero-asset-discovery"]["asset_discovery"]["assets"]}
surface = instances["rankzero-attack-surface-mapper"]["attack_surface"]
```

The preservation requirement written as prose in ADR-002 thus became executable
in the corpus's next-but-one commit.

## The pipeline was extended, not revised

API Security Review was appended as a seventh stage at `6cb5ef0` and the
orchestrator moved to 0.4.0 to route it. The six-stage order decided here was
never reordered, and no ADR supersedes ADR-002 — its `supersedes` field is empty
at S1 HEAD and no later ADR names it as superseded.

## Coverage remained partial

At S1 HEAD the validator's tuple is five skills:

```python
PHASE2_SKILLS = (
    "rankzero-asset-discovery", "rankzero-attack-surface-mapper",
    "rankzero-authentication-review", "rankzero-authorization-review",
    "rankzero-api-security-review",
)
```

Two of the seven pipeline stages — **Architecture Discovery** and **Threat Model
Generator** — never acquired a schema or entered the validator, though both
produced real-code output JSON at `6cb5ef0`. `architecture-discovery.json` and
`threat-model.json` sit in the evaluations directory unvalidated by the script
that checks their six siblings.

## The "blocked rather than inferred" consequence was exercised

ADR-002 accepted that "missing prerequisites produce partial or blocked outputs
rather than inferred facts." The reconciliation at `df3cace` records absence
findings in that form — "Verified absence within scope", with an explicit
caveat that they "do not prove that an object never existed on an unavailable
device or expired remote" — rather than converting missing evidence into
negative facts.

## The batching departure was never addressed

D002 recorded "Upload specialist skills individually." This episode added four
packages in one commit. No artifact notes the change, reconciles it, or
supersedes the earlier rule, and the rule remains in the change log at S1 HEAD.

## Not an evaluation

This file records what followed. It takes no position on whether the pipeline
order or its coverage was correct.
