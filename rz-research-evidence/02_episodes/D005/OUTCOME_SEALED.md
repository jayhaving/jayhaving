# D005 — OUTCOME_SEALED

Everything below became visible **after** 2026-07-20 21:03:10 −0400.

---

## The boundary met a real violation 64 minutes later

ADR-003 was set with no case in hand. At `6cb5ef0` (22:07:24) the reviewed
gateway was found to contain a code path that violates it, recorded as **RZ-005
— LLM-controlled enforcement state (high, confidence 0.98)**:

> optional model output is substring-matched and can write quarantine state.
> This violates RankZero's deterministic-enforcement boundary.

This reconstruction independently verified the code path in S2 at
`13e79c8b2e607e07cfc0629f89cb8654edc5383e`:

- `v4-single-binary/src/llm.rs:99` — `if text.contains("DECISION: MALICIOUS")`
- `v4-single-binary/src/llm.rs:138` — `INSERT OR IGNORE INTO quarantine (agent_id, timestamp) VALUES (?1, ?2)`

The substring test and the enforcement write are in the same function body,
39 lines apart. The finding is confirmed at source level.

## The boundary was promoted to a product-level ADR

Rather than treating RZ-005 as one finding among others, the same commit added
**ADR-005 — LLM Output Cannot Mutate Enforcement State** (reconstructed as
D008), generalizing this episode's review-system rule into a prohibition on the
product. ADR-005 also directs a reclassification:

> The current prototype path is a verified vulnerability, not a
> behavioral-analysis control.

So this episode's boundary became the criterion by which an existing feature was
reclassified as a defect.

## The reproducibility claim was extended to real output

At `6cb5ef0` the validator grew from 345 to 426 lines, adding
`validate_evaluation_outputs` (line 341) so the eight real-code specialist
outputs are schema-checked, secret-screened, and cross-referenced by the same
model-free script. Two categories that were authoritative-by-declaration at this
episode — reachability and policy evaluation — remained without executable
validators in S1 at HEAD.

## The confidence scale was used as decided

Findings recorded at `6cb5ef0` carry explicit numeric confidence (RZ-001 at
0.99, RZ-002 at 0.98, RZ-013 at 0.99, RZ-014 at 0.96), and the reconciliation
note publishes a three-level confidence basis table keyed to evidence type
rather than to certainty of belief. ADR-003's rule that "confidence measures
evidence quality, not control correctness" is applied verbatim in the
reconciliation's structure.

## The prohibition on substituting confidence for evidence was honored

The reconciliation records absence findings as "Verified absence **within
scope**" at Medium confidence, with an explicit statement that they "do not
prove that an object never existed on an unavailable device or expired remote."
Missing evidence was recorded as missing rather than resolved by inference —
the second of ADR-003's four prohibitions.

## Where the boundary did not reach

The deterministic side of every check in this corpus validates **structure**:
schemas, identifiers, uniqueness, confidence ranges, secret shapes. The
**content** of every specialist finding was produced by a model executing a
prompt, and no transcript, tool log, or reproducible run record for that side
exists at any commit in S1. The authority boundary is enforceable over the
output envelope and, in the reachable record, not over the reasoning that filled
it.

## Not an evaluation

This file records what followed. It takes no position on whether the
deterministic/interpretive boundary was correctly drawn or correctly scoped.
