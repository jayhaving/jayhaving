# D007 — TECHNICAL_STATE

State at the episode boundary: S1 `6cb5ef0` (2026-07-20 22:07:24 −0400).
Shared with D008.

## S1 — the reviewing system

| Property | Value |
|---|---|
| Tracked files | 118 |
| ADRs | 5 |
| Risk records | 6 + `Known Gaps.md` |
| Research notes | 2 + index |
| Evaluations | 8 JSON under `05-Research/evaluations/rust-gateway-13e79c8/` |
| Validator | 426 lines, 5 skills in scope, real-code output checking |
| Orchestrator | **0.4.0** |
| Roadmap Phase 2 | 6 of 9 |

### Pipeline, now seven stages

```
Architecture Discovery → Asset Discovery → Threat Model Generator
  → Attack Surface Mapper → Authentication Review → Authorization Review
  → API Security Review
```

### Schema coverage across the pipeline

| Stage | Schema | In validator |
|---|---|---|
| Architecture Discovery | no | no |
| Asset Discovery | yes | yes |
| Threat Model Generator | no | no |
| Attack Surface Mapper | yes | yes |
| Authentication Review | yes | yes |
| Authorization Review | yes | yes |
| API Security Review | yes | yes |

Five of seven stages are schema-backed. `architecture-discovery.json` and
`threat-model.json` exist as real-code outputs with no schema to check them.

### API skill package, as shipped

| File | Role |
|---|---|
| `SKILL.md` | version 0.1.0 |
| `agents/openai.yaml` | agent manifest |
| `schemas/output.schema.json` | Draft 2020-12 output contract |
| `examples/valid-output.json` | positive fixture |
| `tests/invalid-output.json` | negative fixture |
| `references/review-checks.md` | check reference — the only `references/` directory among the five Phase 2 packages |

## S2 — the reviewed system at `13e79c8` (unchanged by this episode)

The API surface cited by ADR-004, re-verified:

| Route | Method | File:line | Authenticated in handler? |
|---|---|---|---|
| `/mint` | POST | `gateway.rs:204` | **no** — handler at `gateway.rs:219` contains no `verify_admin_key` call |
| `/api/incidents` | GET | `gateway.rs:205` | yes — handler at 305, `verify_admin_key` at 310 |
| `/api/quarantine/{agent_id}` | POST | `gateway.rs:206` | yes — handler at 335, check at 341 |
| `/api/revoke/{agent_id}` | DELETE | `gateway.rs:207` | yes — handler at 396, check at 402 |
| `/api/audit` | GET | `gateway.rs:208` | yes — handler at 436, check at 441 |
| `/api/test-incident` | POST | `gateway.rs:209` | yes — handler at 366, check at 371 |
| `/api/secure-action` | POST | `gateway.rs:210` | **no** — handler at 270 contains no `verify_admin_key` call |
| `/healthz` | GET | `gateway.rs:211` | n/a |
| `/api/telemetry` | GET (WS) | `telemetry.rs:20` | none observed |
| `/api/kms/domains` | GET | `proxy.rs:98` | none observed |
| `/proxy/{*target_url}` | any | `proxy.rs:97` | JWT/DPoP + OPA path |
| static fallback | — | `web.rs:17` | n/a |

`verify_admin_key` is defined at `gateway.rs:34` and called at lines 310, 341,
371, 402, and 441 — five call sites, all inside management handlers. Neither
`mint_agent_identity` (line 219) nor `secure_agent_action` (line 270) is among
them. The admin key default is the literal
`"v4_default_admin_key_CHANGE_ME"` (`gateway.rs:64`); the JWT signing default is
`"v4_development_secret_key_only"` (in the mint handler).

**Counting note:** the vault describes "11 named HTTP/WebSocket routes." A direct
count gives 10 named + 1 wildcard proxy + 1 static fallback. The discrepancy is
one route; which convention the vault applied is UNKNOWN. It does not affect any
finding, since every finding names its route explicitly.

## Findings recorded at this boundary

Seven verified vulnerabilities (`RZ-001` … `RZ-005`, `RZ-013`, `RZ-014`), three
verified missing-control classes (`RZ-006`, `RZ-007`, `RZ-008`), test-coverage
gaps, and architectural limitations. Six of these were promoted to `RISK-001`
… `RISK-006`.

## Validation state

| Artifact | Checked by script |
|---|---|
| 5 Phase 2 skill packages | yes |
| 5 schemas + 10 fixtures | yes |
| 5 of 8 real-code outputs | yes — `validate_evaluation_outputs` maps exactly five skills to five filenames |
| `architecture-discovery.json`, `threat-model.json`, `orchestrated-review.json` | no — no schema exists for any of the three |
| Finding content and reasoning | not checkable by any artifact in the repository |
