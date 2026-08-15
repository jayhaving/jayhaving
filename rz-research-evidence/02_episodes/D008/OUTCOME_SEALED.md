# D008 — OUTCOME_SEALED

Everything below became visible **after** 2026-07-20 22:07:24 −0400.

---

## The required tests were written 69 minutes later

ADR-005 stated its validation obligation in the future tense. The baseline
report at `ba9d042` (23:16:05) records that gateway commit `285c748` contains
two Rust unit tests answering it precisely:

```
llm::tests::malicious_model_output_cannot_change_enforcement_state
llm::tests::unavailable_model_cannot_change_enforcement_state
```

These map one-to-one onto the ADR's two required properties — arbitrary model
output cannot mutate state, and deterministic rules fail closed when the model
service is unavailable. The report also records that "Removal of every
LLM-to-enforcement mutation path found in the reviewed code" was item 9 of the
remediation, and that `llm.rs` is thereafter "Advisory only; cannot mutate
authorization, revocation, or quarantine."

Recorded results: 44/44 Python security-boundary methods and 6/6 Rust unit
tests. Both are VAULT-ASSERTED — no run log, artifact, or CI record exists.

## The reclassification propagated

The consequence "the current prototype path is a verified vulnerability, not a
behavioral-analysis control" was applied consistently in later artifacts:

- `Known Gaps.md` lists it under **Verified Vulnerabilities**, not under limitations.
- The baseline report's remaining-risks section states flatly: "**ML detection is not implemented.** Content inspection is deterministic regex, substring, and rolling-average logic with known bypasses; it must not be described as ML or AI-powered detection."

The labeling constraint decided here became a standing disclosure in the
project's terminal document.

## The forward obligation was never exercised

ADR-005's third consequence — "Future runtime review skills must flag any
model-to-enforcement mutation path" — binds skills that do not exist. Phase 3
(Runtime Inspection, Behavioral Analysis, Telemetry Correlation, Threat Hunting,
Incident Builder, Timeline Reconstruction, Root Cause Analysis) is **0 of 7** at
S1 HEAD, unchanged since vault initialization. No runtime review skill was ever
built, so the obligation has had nothing to apply to.

## Later discovery — the fix is not in the reachable record

**Verified in this reconstruction on 2026-08-15:** commit `285c748` is not
present in the public gateway repository (`git cat-file -t` fails against a full
clone; the remote advertises only `main` at `38ca81f` and `v4-session13` at
`13e79c8`).

The vulnerable path is therefore still the current public code. Re-verified at
`13e79c8` today, byte-for-byte as recorded in PRE_DECISION.md:

```
llm.rs:99    if text.contains("DECISION: MALICIOUS")
llm.rs:100       is_malicious = true;
llm.rs:127   if is_malicious {
llm.rs:138       INSERT OR IGNORE INTO quarantine (agent_id, timestamp) VALUES (?1, ?2)
```

`RISK-004-LLM-Controlled-Enforcement` remains `status: open` at S1 HEAD. The
baseline report classifies it as remediated at `285c748`; the risk record itself
was never updated, so the vault's two documents disagree on its state — the
report says remediated for the tested branch, the risk file says open.

## The compounding weakness was addressed in the same unreachable commit

`RZ-004`'s alias bypass is recorded as remediated at `285c748` by keying
quarantine to a stable `(tenant_id, subject_id)` pair rather than the
caller-selected alias, with Test 40 cited. As with RZ-005, this is
VAULT-ASSERTED and not reachable.

## Not an evaluation

This file records outcomes and later observations. It takes no position on
whether the prohibition was correctly scoped, and it does not assess the
prototype's engineering.
