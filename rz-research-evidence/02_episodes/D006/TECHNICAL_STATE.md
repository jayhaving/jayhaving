# D006 — TECHNICAL_STATE

Two systems are in scope at this episode. Both states are as of
2026-07-20 21:33:10 −0400.

---

## S1 — RankZero Security OS vault (the reviewing system)

| Property | Value |
|---|---|
| HEAD | `df3cace` |
| Tracked files | 92 |
| ADRs | 3 |
| Risk records | 0 |
| Research notes | 1 (added this commit) |
| Evaluations directory | does not exist |
| Validator | `scripts/validate_phase2_skills.py`, 345 lines, 4 skills in scope |
| Orchestrator | 0.3.0 |
| Roadmap Phase 2 | 5 of 9 |

The commit added no skill package and changed no schema. It is the corpus's only
documentation-only commit that does not also ship code or contracts.

---

## S2 — Agentic IAM Gateway at `13e79c8` (the reviewed system)

This is the state as it stood *before* the reconciliation's findings. Every row
below is re-verified against S2 in this reconstruction.

### Source layout

| Path | Size | Role per the project's own architecture overview |
|---|---|---|
| `v4-single-binary/src/main.rs` | 3,075 B | startup, config, Rego compilation |
| `v4-single-binary/src/gateway.rs` | 17,835 B | identity issuance, management routes, audit reads |
| `v4-single-binary/src/auth.rs` | 15,723 B | JWT + DPoP verification, revocation lookup, OPA call |
| `v4-single-binary/src/proxy.rs` | 13,645 B | target parsing, credential attach, upstream forwarding |
| `v4-single-binary/src/behavior.rs` | 17,283 B | secret/injection pattern inspection, redaction |
| `v4-single-binary/src/db.rs` | 2,377 B | SQLite state |
| `v4-single-binary/src/llm.rs` | 6,963 B | optional asynchronous incident triage |
| `v4-single-binary/src/telemetry.rs` | 1,008 B | WebSocket telemetry |
| `v4-single-binary/src/web.rs` | 1,354 B | embedded dashboard, static fallback |
| `v4-single-binary/src/ebpf.rs` | 1,739 B | sensor surface |

### Route registrations (re-verified)

| Route | Method | File:line |
|---|---|---|
| `/mint` | POST | `gateway.rs:204` |
| `/api/incidents` | GET | `gateway.rs:205` |
| `/api/quarantine/{agent_id}` | POST | `gateway.rs:206` |
| `/api/revoke/{agent_id}` | DELETE | `gateway.rs:207` |
| `/api/audit` | GET | `gateway.rs:208` |
| `/api/test-incident` | POST | `gateway.rs:209` |
| `/api/secure-action` | POST | `gateway.rs:210` |
| `/healthz` | GET | `gateway.rs:211` |
| `/api/telemetry` | GET (WebSocket) | `telemetry.rs:20` |
| `/api/kms/domains` | GET | `proxy.rs:98` |
| `/proxy/{*target_url}` | any (wildcard) | `proxy.rs:97` |
| static fallback | — | `web.rs:17` |

**Count discrepancy, recorded neutrally:** the vault describes this surface as
"11 named HTTP/WebSocket routes, a wildcard proxy route, and a static fallback."
Re-verification finds **10 named routes + 1 wildcard proxy + 1 static fallback**
— 11 non-fallback route registrations in total. The discrepancy is one route
between the vault's phrasing and a direct count. Which convention the vault used
is UNKNOWN.

### Tests

| Suite | Count | Location |
|---|---|---|
| Python integration | 34 `test_*` methods | `tests/test_security_boundaries.py` |
| Rust native | — | `test_regorus.rs` exists at `v4-single-binary/` root, outside the crate's test paths |
| Load | separate | `tests/test_load.py` |

### Build inputs

`soc-dashboard/dist` — required for compile-time embedding — is **not tracked**
at `13e79c8`: `git ls-files | grep -c "soc-dashboard/dist"` → 0. Re-verified.

### The prototype's own documentation vault

| File | Lines | Content relevant here |
|---|---|---|
| `docs/CONTEXT_BUNDLE.md` | 5,549 | historical claim set |
| `docs/vault/01-Decision-Log.md` | 199 | `DEC-001` … `DEC-013`, dated 2026-07-16/17 |
| `docs/vault/04-Known-Gaps-and-Honesty-Log.md` | 313 | `GAP-001` … `GAP-016` |
| `docs/vault/10-Test-Quality-Audit.md` | 193 | all 34 tests classified; Test 04 TRACEABLE |
| `docs/vault/NEXT_TASK.md` | — | active scoped task; "Do not run mutation testing" |
| `docs/vault/status.json` | — | `last_verified` 2026-07-17, 34 passing, 13 capabilities |

### Repository branch state

| Ref | Commit | Note |
|---|---|---|
| `main` | `38ca81f` (2026-07-13 19:49) | does not contain the V4 gateway |
| `v4-session13` | `13e79c8` (2026-07-20 01:39) | carries all V4 work |

The V4 single-binary gateway was never on the default branch at this episode.

---

## Relationship between the two systems

They are separate repositories with separate histories. The vault's architecture
note records the boundary explicitly: findings "describe a separate recovered
prototype repository and do not mean its runtime has been merged into this
vault."
