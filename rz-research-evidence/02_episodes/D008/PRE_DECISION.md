# D008 — PRE_DECISION

**Episode:** Prohibit LLM output from mutating enforcement state (ADR-005)
**Decision moment:** at or before 2026-07-20 22:07:24 −0400 `[R-D008-01]`
**Decision maker of record:** `Jason Awuah` `[R-D008-01]`
**Participants beyond the commit author:** UNKNOWN

Shares a receipt commit with D007. Separated because this decision constrains
the **product**, not the review process, and because it reclassifies an existing
feature.

---

## Situation as visible at the decision moment

### The principle already existed for the review system

ADR-003, decided 64 minutes earlier, held that LLM reasoning may interpret but
not override deterministic results, and prohibited an LLM from "override[ing] a
deny decision" `[R-D008-02]`. That rule governed **RankZero's own review
skills**.

The founding memory note, 2h 47m earlier, listed "Deterministic enforcement in
the critical path" and "LLM analysis in the intelligence path" as product ideas
`[R-D008-03]`.

What did not exist was a rule stating that the product's enforcement state may
never be written by model output — and, critically, a determination of what to
do when an existing code path does exactly that `[R-D008-04]`.

### The observed code path

ADR-005's Context, committed with the decision (category-2 information under
`00_method/METHOD.md`) `[R-D008-05]`:

> The recovered prototype contains a source path where optional model text is
> substring-matched and directly writes quarantine state. Model output is
> untrusted, nondeterministic interpretation; quarantine is a critical
> enforcement control.

**This is independently re-verifiable and was confirmed in this reconstruction**
against the reviewed source, which is public and unchanged `[R-D008-06]`:

| Step | Location at `13e79c8` | Code |
|---|---|---|
| Model response read | `v4-single-binary/src/llm.rs:97` | `json_resp["candidates"][0]["content"]["parts"][0]["text"].as_str()` |
| Substring test | `llm.rs:99` | `if text.contains("DECISION: MALICIOUS")` |
| Flag set | `llm.rs:100` | `is_malicious = true;` |
| Enforcement write | `llm.rs:126`–`138` | `if is_malicious { … INSERT OR IGNORE INTO quarantine (agent_id, timestamp) VALUES (?1, ?2) }` |

All four steps are in one asynchronous block. The write is guarded by nothing
but the substring test. The source comment at the write site reads
"3. Auto-Quarantine if malicious (scoped block — drops before .await)"
`[R-D008-06]`.

### How the path was previously characterized

The prototype's own historical record described the LLM stage as triage and
behavioral analysis, and its detection layer as rule-based `[R-D008-07]`. The
same commit's review note lists as a false-or-stale claim: "Regex/subsequence
behavior matching is not ML or AI-powered detection" `[R-D008-08]`.

**INFERENCE:** the code path was previously understood as a **feature** —
LLM-assisted auto-quarantine — rather than a defect. Basis: the source comment
"Auto-Quarantine if malicious" and a `tracing::warn!` message reading
"Auto-Quarantining Agent {} based on LLM analysis!", both written affirmatively;
plus ADR-005's own directive to reclassify it. The reasoning step — that
affirmative naming indicates prior intent — is inference, not a stated record.

### The finding as recorded in the same commit

`RZ-005 — LLM-controlled enforcement state`, severity high, confidence 0.98:
"optional model output is substring-matched and can write quarantine state. This
violates RankZero's deterministic-enforcement boundary" `[R-D008-09]`.

### Related quarantine weakness already established

`RZ-004 — quarantine alias bypass` (high, 0.99): quarantine was keyed by a
caller-selected `agent_id`, so a newly minted alias escaped it `[R-D008-09]`. So
at the decision moment quarantine was known to be both **writable by model
output** and **evadable by re-minting**.

---

## The decision

LLM output "may propose, prioritize, or explain a response, but it cannot
directly activate, remove, or modify authentication, authorization, quarantine,
revocation, policy, credential, or isolation state. A deterministic rule or
explicit authorized approval must independently validate every enforcement
mutation" `[R-D008-05]`.

Seven state categories are named: authentication, authorization, quarantine,
revocation, policy, credential, isolation.

### Consequences accepted

Three, as recorded `[R-D008-05]`:

1. "The current prototype path is a verified vulnerability, not a
   behavioral-analysis control." — a **reclassification** of existing behavior.
2. "Regex or substring matching is not described as ML or AI-powered detection."
   — a labeling constraint.
3. "Future runtime review skills must flag any model-to-enforcement mutation
   path." — a forward obligation on skills not yet built.

### Validation required, and not yet performed

ADR-005 states the test obligation in the future tense `[R-D008-05]`:

> Tests **must prove** that arbitrary model output alone cannot change
> enforcement state and that deterministic rules fail closed when model services
> are unavailable.

No such test existed at the decision moment. The reviewed prototype had zero
Rust-native tests, and the vault repository contains no test for product
behavior at any commit `[R-D008-10]`.

### Risk record opened

`RISK-004-LLM-Controlled-Enforcement`, severity high, `status: open`, created in
this same commit `[R-D008-11]`.

---

## Scope limit carried forward

This decision does not remediate the path. The commit changed no prototype
source, and remediation remained out of scope per D006 `[R-D008-12]`.
