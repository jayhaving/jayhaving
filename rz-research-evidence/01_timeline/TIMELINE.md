# Timeline

All times EDT (−0400), taken from git author timestamps. Episode boundaries are
upper bounds on the decision moment, per `00_method/METHOD.md`.

## Background: gateway repository (S2)

| Time | Ref | Event |
|---|---|---|
| 2026-07-13 18:47 | `1a648f3` | Initial commit: Agentic IAM Gateway V1 prototype |
| 2026-07-13 19:49 | `38ca81f` | Initial commit: RankZero Agentic IAM Gateway — **still the tip of `main` on 2026-08-15** |
| 2026-07-13 20:00 | `1ced058` | SDK branding updated to RankZero Shield |
| 2026-07-20 00:53 | `fb44b19` | V4 single-binary gateway + vault + context bundle (Session 13) |
| 2026-07-20 01:01 | `8cbf03c` | Two stale doc counts corrected |
| 2026-07-20 01:16 | `4eaee8d`, `5028104` | Codex session instructions and scoped task handoff added |
| 2026-07-20 01:17–01:34 | `ea5cd4b` … `ac4cea1` | Vault entry point, status verifier prerequisite, test integrity/tautology audits |
| 2026-07-20 01:39 | `13e79c8` | `docs: scope test-audit fixes` — tip of `v4-session13`, the ref reviewed in D006–D008 |

**17h 41m with no commit in either repository.**

## Vault repository (S1) — the episode sequence

| Time | Commit | Episode | Event |
|---|---|---|---|
| 19:20:25 | `b8638a1` | **D001** | Vault initialized: 33 files — vision, architecture, 8 skill notes, decision log, risk register, roadmap, change log, project memory, 6 templates, 4 dashboards, canvas |
| 19:24:14 | `39283a6` | D001 | Four third-party Obsidian skills added from `kepano/obsidian-skills` with `skills-lock.json` hashes |
| 20:33:36 | `17a50b7` | **D002** | Seven RankZero specialist skill packages installed; orchestrator at v0.1.0 |
| 20:42:10 | `b2fa397` | **D003** | Architecture Discovery skill + **ADR-001**; orchestrator → v0.2.0 |
| 21:03:10 | `54976fd` | **D004**, **D005** | Four Phase 2 skills with JSON schemas and fixtures + **ADR-002**, **ADR-003** + validator script; orchestrator → v0.3.0 |
| 21:33:10 | `df3cace` | **D006** | Rust prototype reconciliation research note; architecture and memory updated; no skill changes |
| 22:07:24 | `6cb5ef0` | **D007**, **D008** | Grounded gateway security review, 6 machine-readable specialist outputs, API Security Review skill, **ADR-004**, **ADR-005**, 6 risk records, known-gaps taxonomy; orchestrator → v0.4.0 |
| 23:16:05 | `ba9d042` | **D009** | Security Baseline Report v0.1 (274 lines); research index, change log, project memory updated |

Elapsed from first to last vault commit: **3h 55m 40s**.

## Interval structure

| Gap | Duration | What it produced |
|---|---|---|
| `39283a6` → `17a50b7` | 1h 09m | Longest gap in the sequence. Contents **UNKNOWN**; the vault records a skill installation audit whose activity is not otherwise dated. |
| `17a50b7` → `b2fa397` | 9m | ADR-001 + one skill package + orchestrator bump |
| `b2fa397` → `54976fd` | 21m | 4 skill packages, 4 JSON schemas, 8 fixtures, validator, 2 ADRs |
| `54976fd` → `df3cace` | 30m | Reconciliation of an external repository (**VAULT-ASSERTED** builds, test runs, and filesystem searches) |
| `df3cace` → `6cb5ef0` | 34m | 6 specialist evaluations, review note, API skill package, 2 ADRs, 6 risk records |
| `6cb5ef0` → `ba9d042` | 1h 09m | Baseline report; the vault dates the separate gateway remediation `285c748` to this window |

## After 2026-07-20

| Date | Event |
|---|---|
| 2026-07-21 03:21 | Last recorded push to `rankzero-security-os` (GitHub metadata) |
| 2026-07-21 | `agentic-iam-getway` — a separately named, empty repository — last pushed |
| 2026-08-15 | This reconstruction. S1 HEAD unchanged at `ba9d042`; S2 `main` unchanged at `38ca81f`; `285c748` not present on S2 |

No commit exists in either repository between 2026-07-20 23:16 and the
2026-08-15 observation — a span of 26 days.
