# D008 — TECHNICAL_STATE

State at the episode boundary: S1 `6cb5ef0` (2026-07-20 22:07:24 −0400).
Shares the commit with D007; this file records the state relevant to the
enforcement boundary.

## The enforcement surface in the reviewed system at `13e79c8`

| Enforcement state | Written by | Guarded by |
|---|---|---|
| `quarantine` | admin route `POST /api/quarantine/{agent_id}` | `verify_admin_key` (`gateway.rs:341`) |
| `quarantine` | **`llm.rs:138`, from a substring match on model text** | **nothing beyond `if is_malicious`** |
| `revoked_tokens` | admin route `DELETE /api/revoke/{agent_id}` | `verify_admin_key` (`gateway.rs:402`) |
| `incidents.soc_report` | `llm.rs:118` (`UPDATE incidents SET soc_report`) | none — advisory field |
| authorization decision | Rego policy evaluated in `auth.rs` | deterministic |
| authentication | JWT + DPoP in `auth.rs` | deterministic |

Two write paths reach the same `quarantine` table: one administrative and
authenticated, one from model output and unguarded.

## The model path in detail

```
llm.rs:91    let mut is_malicious = false;
llm.rs:93    client.post(&url).json(&req_body).send().await     ← external Gemini call
llm.rs:97    json_resp["candidates"][0]["content"]["parts"][0]["text"].as_str()
llm.rs:99        if text.contains("DECISION: MALICIOUS")
llm.rs:100           is_malicious = true;
llm.rs:118   UPDATE incidents SET soc_report = ?1 WHERE id = ?2   ← advisory write
llm.rs:126   // 3. Auto-Quarantine if malicious
llm.rs:127   if is_malicious {
llm.rs:128       tracing::warn!("Auto-Quarantining Agent {} based on LLM analysis!", agent_id);
llm.rs:138       INSERT OR IGNORE INTO quarantine (agent_id, timestamp) VALUES (?1, ?2)
```

Failure handling on this path is `let _ = conn.execute(...)` with an error branch
that only logs — the enforcement write's result is discarded either way.

## Quarantine's other observed weakness at this boundary

`RZ-004`: quarantine is keyed by the caller-selected `agent_id`, and `/mint`
(`gateway.rs:204`, handler at 219) accepts caller-chosen identity without
authentication. A quarantined identifier can therefore be replaced by minting a
new alias. The two findings compound: the state is writable by model output and
escapable by re-minting.

## Test coverage of the boundary at this moment

| Property ADR-005 requires proving | Test present |
|---|---|
| Arbitrary model output alone cannot change enforcement state | none |
| Deterministic rules fail closed when model services are unavailable | none |

The prototype's Python suite contains a test named for LLM-failure resilience
(Test 10), which the prototype's own audit had already classified TRACEABLE /
WEAK: it "does not cause, mock, or observe an LLM failure." Rust-native test
count is zero; `v4-single-binary/Cargo.toml` declares no `[[test]]` section and
no `[dev-dependencies]`.

## S1 artifacts recording the decision

| Artifact | State |
|---|---|
| `04-Decisions/ADR-005-…md` | created, `status: accepted` |
| `07-Risks/RISK-004-LLM-Controlled-Enforcement.md` | created, `status: open`, severity high |
| `07-Risks/Known Gaps.md` | created; lists "LLM substring output can directly write quarantine state" under Verified Vulnerabilities |
| `05-Research/2026-07-20-Rust-Gateway-Security-Review.md` | created; RZ-005 at confidence 0.98 |
| Product source | unchanged in both repositories |
