# D005 — PRE_DECISION

**Episode:** Make deterministic checks authoritative over LLM reasoning (ADR-003)
**Decision moment:** at or before 2026-07-20 21:03:10 −0400 `[R-D005-01]`
**Decision maker of record:** `Jason Awuah` `[R-D005-01]`
**Participants beyond the commit author:** UNKNOWN

Shares a receipt commit with D004. Separated because this decision governs
*authority between two kinds of evidence*, is cited independently by later work,
and is the constraint under which a later finding was classified.

---

## Situation as visible at the decision moment

### The general commitment already on record

The project's founding memory note, written 1h 43m earlier, already listed
"Deterministic enforcement in the critical path" and "LLM analysis in the
intelligence path" as core product ideas `[R-D005-02]`. That is a statement
about the *product being built*.

What did not exist before this moment is the same split applied to **RankZero's
own review skills** — a rule about which of the review system's outputs may
override which `[R-D005-03]`.

### The stated problem

ADR-003's Context, committed with the decision (category-2 information)
`[R-D005-04]`:

> LLMs are useful for interpreting evidence and explaining security
> implications, but they are not reliable enforcement engines or schema
> validators. The new review skills need an explicit boundary between
> reproducible checks and model judgment.

Two properties are named as the concern: reliability as an enforcement engine,
and reliability as a schema validator. Neither is supported by a cited study,
measurement, or trial in the corpus `[R-D005-05]`. The claim is asserted as
general knowledge about LLMs.

### Alternatives on the table

Three, with recorded rejection grounds `[R-D005-04]`:

| Alternative | Recorded rejection ground |
|---|---|
| Let the model synthesize final check states | "results would not be reproducible" |
| Avoid model reasoning entirely | "evidence interpretation and prioritization still benefit from contextual analysis" |
| Use confidence as a substitute for validation | "confidence measures evidence quality, not control correctness" |

The second rejection is what keeps this decision a *boundary* rather than a
prohibition — model reasoning is retained, with a ceiling.

### No observed violation

At this moment no system had been reviewed, no finding recorded, and no code
examined `[R-D005-06]`. The boundary is set before any case requires it.

---

## The decision

Two lists, one authoritative and one interpretive `[R-D005-04]`:

**Authoritative (deterministic):** check results, graph reachability, policy
evaluation, schema validation, regression-test results.

**Interpretive (LLM):** interpretation, prioritization, hypothesis generation,
deduplication, explanation.

And four explicit prohibitions — an LLM must not:

1. convert a deterministic failure into a pass,
2. replace missing evidence with confidence,
3. override a deny decision,
4. claim reachability contradicted by the reviewed graph.

### Consequences accepted

Four, as recorded `[R-D005-04]`:

- output schemas separate deterministic checks, evidence, confidence, and findings;
- every check records method and result;
- confidence follows a shared evidence-quality scale from 0.0 to 1.0;
- invalid schemas or fixtures fail **without model intervention**.

### The mechanism shipped with the decision

Unlike D003's decision, this one arrived with enforcement in the same commit
`[R-D005-07]`. `scripts/validate_phase2_skills.py` is 345 lines of standard
library Python with no model in the loop:

| Consequence | Implementing function |
|---|---|
| confidence on a 0.0–1.0 evidence scale | `validate_confidence_values` (line 270) |
| invalid fixtures fail without model intervention | `validate_instance` (line 190) run against a deliberately invalid fixture per skill |
| identifiers cannot be silently renamed | `unique_ids` (263), `validate_cross_references` (284) |
| secret values must not appear in outputs | `detect_literal_secrets` (242) |

The ADR names the script by path as its validation basis `[R-D005-04]`, and the
script exists at that path in the same commit `[R-D005-07]`.

### The reproducibility claim, as scoped at the decision moment

`validate_phase2_skills.py` "uses only the Python standard library and verifies
each package, schema, positive fixture, negative fixture, cross-reference
contract, and literal-secret screen" `[R-D005-04]`. Its declared coverage is
four skills `[R-D005-08]`:

```python
PHASE2_SKILLS = (
    "rankzero-asset-discovery",
    "rankzero-attack-surface-mapper",
    "rankzero-authentication-review",
    "rankzero-authorization-review",
)
```

Architecture Discovery and Threat Model Generator — the two earliest pipeline
stages — are outside that tuple at this moment `[R-D005-08]`.

### Follow-up recorded

- "Reuse this boundary in future API, MCP, RAG, cloud, runtime, and compliance skills."
- "Add deterministic domain checks as executable validators **when implementations exist**." `[R-D005-04]`

The second acknowledges that the deterministic domain checks the ADR makes
authoritative — policy evaluation, graph reachability, regression tests — did
not yet exist as executable validators in the repository `[R-D005-09]`.

---

## Recorded scope limit

The ADR's authority list includes "policy evaluation" and "graph reachability"
as authoritative evidence. At the decision moment the repository contained no
policy engine, no graph implementation, and no regression suite `[R-D005-09]`.
The decision therefore assigns authority to categories of evidence that were, at
that moment, produced by procedures outside the repository. Whether that was
understood as a gap is UNKNOWN; the follow-up bullet is the only artifact
touching it.
