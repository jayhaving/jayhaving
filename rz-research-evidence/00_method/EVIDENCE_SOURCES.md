# Evidence sources

All source identifiers used by episode receipts are defined here.

## S1 — RankZero Security OS vault

| Field | Value |
|---|---|
| Repository | `jayhaving/rankzero-security-os` (private) |
| Access | Cloned 2026-08-15; full history fetched |
| HEAD at observation | `ba9d042fb83f67c0622f38dc85c0408f80524aec` |
| Commit count | 8 |
| Span | 2026-07-20 19:20:25 −0400 → 2026-07-20 23:16:05 −0400 |
| Status | VERIFIED-HERE |

An Obsidian vault. Contains vision, architecture notes, a skill registry, five
ADRs, six risk records, a change log, research notes, machine-readable
specialist evaluations, and Agent Skill packages under `.agents/skills/`.

Full commit list:

```
b8638a1  19:20:25  Initialize RankZero Security OS knowledge vault
39283a6  19:24:14  Initialize RankZero Security OS vault and agent skills
17a50b7  20:33:36  Install RankZero security agent skills
b2fa397  20:42:10  Add RankZero architecture discovery skill
54976fd  21:03:10  Add Phase 2 discovery and access review skills
df3cace  21:33:10  docs: reconcile recovered Rust prototype
6cb5ef0  22:07:24  Add grounded Rust gateway security review
ba9d042  23:16:05  docs: add security baseline report v0.1
```

All eight commits fall on 2026-07-20, spanning 3h 56m.

## S2 — Agentic IAM Gateway

| Field | Value |
|---|---|
| Repository | `jayhaving/agentic-iam-gateway` (public) |
| Access | Cloned 2026-08-15; full history |
| `refs/heads/main` at observation | `38ca81f431dd20056def093dc5f6f0a9a1ee8199` |
| `refs/heads/v4-session13` at observation | `13e79c8b2e607e07cfc0629f89cb8654edc5383e` |
| Total advertised refs | 2 branches, no tags |
| Status | VERIFIED-HERE |

The executable prototype reviewed in episodes D006–D009. Its `v4-session13`
branch tip `13e79c8` is authored 2026-07-20 01:39:22 −0400, roughly 17h 41m
before the vault's first commit.

## S3 — Profile repository

`jayhaving/jayhaving`, the host of this workspace. Two commits, 2026-04-02,
containing a profile README. It is the write target for this reconstruction and
is **not evidence** for any episode.

## S4 — Referenced but unreachable

Every artifact below is cited by the vault record and could not be reached from
this reconstruction. Claims resting solely on these are labeled VAULT-ASSERTED
or UNAVAILABLE.

| Artifact | Cited in | Status |
|---|---|---|
| `/Users/jasonawuah/Desktop/RANKZERO_CONTEXT_BUNDLE.md` | Reconciliation research note | UNAVAILABLE — local macOS path |
| `/Users/jasonawuah/.gemini/antigravity-ide/scratch/agentic-iam-gateway` | Reconciliation research note | UNAVAILABLE — local scratch clone |
| `~/Downloads` skill packages (7 specialist packages) | Project Memory, ADR-001 | UNAVAILABLE — local path |
| `cyberforge-security-review` loose file | Project Memory, ADR-001 | UNAVAILABLE — local path |
| Gateway branch `remediation/security-boundaries` at `285c748065a014a202b66a2638e5b86c8361daa3` | Baseline Report v0.1 | UNAVAILABLE — absent from S2 remote on 2026-08-15 |
| Commits `ea65dd2`, `5f92e35` | Reconciliation research note | UNAVAILABLE — recorded as unlocatable in 2026-07 and still absent from S2 |
| Local debug binary `v4-single-binary/target/debug/v4-single-binary` (mtime 2026-07-17) | Reconciliation research note | UNAVAILABLE — build artifact, untracked |
| `soc-dashboard/dist` build assets | Reconciliation research note, review | UNAVAILABLE — confirmed untracked at `13e79c8` |
| All recorded test executions (34-method run, 44/44 run, 6/6 Rust run) | Change log, research notes, baseline report | VAULT-ASSERTED — no run logs, CI records, or artifacts in either repository |

## Structural limit of this corpus

The RankZero record is a single-author, single-machine record. Every execution
result it reports was produced on a workstation whose filesystem is not
reachable here, and no continuous-integration system, run log, or published
artifact independently attests to any of them. Source-level claims about the
gateway are re-verifiable because the source is public; execution claims are
not. Episodes state which side of that line each claim falls on rather than
treating the two as equivalent.
