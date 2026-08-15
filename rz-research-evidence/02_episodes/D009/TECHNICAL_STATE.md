# D009 — TECHNICAL_STATE

State at the episode boundary: S1 `ba9d042` (2026-07-20 23:16:05 −0400) — the
terminal state of the corpus.

## S1 — RankZero Security OS vault

| Property | Value |
|---|---|
| Commits | 8 |
| Tracked files | 120 |
| ADRs | 5 |
| Risk records | 6, all `status: open` |
| Research notes | 3 + index |
| Change-log entries | 5 dated + rolling |
| RankZero skill packages | 14 |
| Third-party skill packages | 4, SHA-256 pinned |
| Validator | `scripts/validate_phase2_skills.py`, 426 lines, 5 skills |
| Orchestrator | 0.4.0 |
| CI | none |

### Roadmap

| Phase | Complete |
|---|---|
| 1 — Foundation | 8 of 8 |
| 2 — Engineering | 6 of 9 (MCP, RAG, Cloud/Infrastructure open) |
| 2 — Evidence Status | 3 of 4 (remediation item open by design) |
| 3 — Runtime Intelligence | 0 of 7 |
| 4 — Enterprise Trust | 0 of 6 |

## S2 — the reviewed system, in two states

### Reachable state — `v4-session13` at `13e79c8`

Unchanged throughout the corpus. All defects recorded at D006–D008 present:
unauthenticated `/mint` (`gateway.rs:204`, handler 219), revocation key mismatch
(`gateway.rs` write vs `auth.rs:129–142` read), model-to-quarantine path
(`llm.rs:99→138`), unauthenticated `/api/kms/domains` and `/api/telemetry`,
untracked `soc-dashboard/dist`, 34 Python test methods, zero Rust tests.

### Claimed state — `remediation/security-boundaries` at `285c748`

Not reachable. Every row below is VAULT-ASSERTED from the baseline report.

| Module | Claimed boundary at `285c748` |
|---|---|
| `main.rs` | exits before binding when required keys or policy are unavailable |
| `gateway.rs` | admin-authenticated issuance; tenant-scoped quarantine/revocation |
| `auth.rs` | JWT + DPoP verification, canonical principal construction, revocation, OPA — "no LLM dependency" |
| `policies.rego` | evaluates signed identity, tenant, action, method, path, domain, quarantine, credential context |
| `proxy.rs` | HTTPS-only targets; positive outbound-header allowlist; 15-second upstream timeout |
| `behavior.rs` | deterministic regex/substring and rolling average — "not ML" |
| `db.rs` | one local SQLite database; "not shared across replicas" |
| `llm.rs` | "Advisory only; cannot mutate authorization, revocation, or quarantine" |
| `telemetry.rs`, `web.rs`, `ebpf.rs` | "No verified kernel enforcement" |

Claimed test totals: 44 Python security-boundary methods, 6 Rust unit tests.

## The two-state gap

| Aspect | Reachable (`13e79c8`) | Claimed (`285c748`) |
|---|---|---|
| `/mint` authentication | none | `X-Admin-Key` required |
| Revocation identifier | mismatched write/read keys | one canonical signed `jti` |
| DPoP replay protection | none | atomic proof-key + `jti` consumption |
| Quarantine key | caller-selected alias | stable `(tenant_id, subject_id)` |
| LLM → enforcement | writes quarantine | advisory only, two unit tests |
| Outbound headers | — | positive allowlist |
| Denial attribution | absent | `X-RankZero-Denial` |
| Python tests | 34 | 44 |
| Rust tests | 0 | 6 |

Only the left column is verifiable. The report itself scopes the right column:
"Closure claims apply to the local `remediation/security-boundaries` branch at
`285c748` and the recorded test environment."

## Explicitly not implemented, per the published baseline

`rz-launcher`; OS containment (cgroup, namespace, seccomp, kernel, eBPF); KMS
integration; ML detection; validated production deployment; DPoP server nonce;
distributed replay/revocation/quarantine state; per-admin identity and key
rotation; tenant-scoped audit and telemetry; request/response size bounds;
tamper-evident audit; restrictive CORS; path-level upstream authorization.
