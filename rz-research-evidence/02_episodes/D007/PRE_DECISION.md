# D007 — PRE_DECISION

**Episode:** Build API Security Review only from an observed executable surface (ADR-004)
**Decision moment:** at or before 2026-07-20 22:07:24 −0400 `[R-D007-01]`
**Decision maker of record:** `Jason Awuah` `[R-D007-01]`
**Participants beyond the commit author:** UNKNOWN

D007 and D008 share a receipt commit. They are separate episodes because ADR-004
gates *when a review specialist may be built*, ADR-005 prohibits *a class of
product behavior*, and each is separately documented and separately cited.

---

## Situation as visible at the decision moment

### The item was already planned, and had been for 2h 47m

"API Security Review" was the sixth entry of Phase 2 — Engineering at vault
initialization, unchecked `[R-D007-02]`. Nothing in this episode decides
*whether* the skill belongs in the roadmap. What it decides is the **evidentiary
precondition** for building it `[R-D007-03]`.

### The reconciliation had completed 34 minutes earlier

`df3cace` established the prototype's verified current state, its historical but
unverified claims, and its lost or contradicted claims `[R-D007-04]`. Its final
RankZero implication read: "Keep API Security Review and new feature work out of
scope until this reconciliation commit is accepted" `[R-D007-05]`. That
condition is what this episode acts on.

### The observed surface, as cited by the decision

ADR-004's Context states the evidentiary basis, committed with the decision
(category-2 information under `00_method/METHOD.md`) `[R-D007-03]`:

> The recovered Rust gateway exposes 11 named HTTP/WebSocket routes, a wildcard
> proxy, a static fallback, management mutations, upstream forwarding,
> authentication and policy middleware, and observable test gaps.

Re-verification of that surface against the reviewed source is recorded in
TECHNICAL_STATE.md, including a one-route counting discrepancy `[R-D007-06]`.

The route inventory was produced by the pipeline in this same commit, so it is
the decision-maker's own contemporaneous evidence rather than an independently
pre-existing artifact. It is nonetheless **re-verifiable**, because the reviewed
source is public and unchanged `[R-D007-06]`.

### The rejected counterfactual

ADR-004 names the alternative it is rejecting in its opening sentence
`[R-D007-03]`:

> An API specialist built from a hypothetical product design would risk encoding
> controls and checks that do not match executable behavior.

No separate "Alternatives Considered" section appears in ADR-004 — unlike
ADR-001, ADR-002, and ADR-003, which each list three `[R-D007-07]`. The single
counterfactual in the Context is the only alternative recorded.

### The known limit, acknowledged before the decision

The reconciliation had already established that the prototype's deployment
surface was contradictory: "Rust, Docker/Compose, DaemonSet, and installer assets
disagree about executable surface and port," and "Which surface is deployed was
not observed" `[R-D007-08]`. The decision proceeds with that limit stated rather
than resolved.

---

## The decision

Build and route `rankzero-api-security-review` **only when repository or runtime
evidence establishes a material API surface**, and ground "its route inventory,
checks, findings, and regression recommendations in observed handlers,
middleware, forwarding, error behavior, fallbacks, and tests" `[R-D007-03]`.

### Consequences accepted

Four, as recorded `[R-D007-03]`:

- version 0.1.0 is "grounded in the recovered gateway at `13e79c8`, not an
  aspirational architecture";
- "Unknown deployment activation remains an architectural limitation";
- the skill consumes the preceding architecture, asset, attack-surface,
  authentication, and authorization contracts — placing it seventh in the D004
  pipeline;
- **API findings cannot override deterministic results from those specialists**
  — a direct application of ADR-003.

### Risks linked at the decision moment

ADR-004 is the first ADR in the corpus with a non-empty `related_risks` field:
`RISK-001`, `RISK-002`, `RISK-003` `[R-D007-09]`. ADR-001, ADR-002, and ADR-003
all carry `related_risks: []` `[R-D007-07]`. The six risk records themselves are
created in this same commit `[R-D007-10]`.

### Validation basis stated

"The package schema, fixtures, cross-references, and **real-code output** pass
`scripts/validate_phase2_skills.py`" `[R-D007-03]`. This is the first validation
claim in the corpus that includes real-code output rather than fixtures alone;
the validator was extended in this commit from 345 to 426 lines and gained
`validate_evaluation_outputs` `[R-D007-11]`.

---

## Scope of the commit

41 paths `[R-D007-12]`: the API skill package (SKILL.md, `agents/openai.yaml`,
`schemas/output.schema.json`, `examples/valid-output.json`,
`tests/invalid-output.json`, `references/review-checks.md`), eight
machine-readable evaluations under
`05-Research/evaluations/rust-gateway-13e79c8/`, the gateway security review
note, ADR-004, ADR-005, the API skill's vault note, and modifications to the
orchestrator (0.3.0 → 0.4.0), seven skill notes, the registry, architecture, and
memory.

Six risk records and `07-Risks/Known Gaps.md` also enter the corpus here
`[R-D007-10]`.

## What this episode does not decide

It does not decide the disposition of the reviewed prototype. Remediation
remained explicitly out of scope, carried forward from D006 `[R-D007-05]`.
