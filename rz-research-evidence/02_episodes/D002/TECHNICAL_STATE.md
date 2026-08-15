# D002 — TECHNICAL_STATE

State at the episode boundary: S1 `17a50b7` (2026-07-20 20:33:36 −0400).

## Skill inventory under `.agents/skills/`

| Package | Origin | Version | Files | Pinned |
|---|---|---|---|---|
| `rankzero-agent-call-lifecycle` | `~/Downloads` (S4) | 0.1.0 | SKILL.md, README.md | no |
| `rankzero-context-isolation` | `~/Downloads` (S4) | 0.1.0 | SKILL.md, README.md | no |
| `rankzero-runtime-debug` | `~/Downloads` (S4) | 0.1.0 | SKILL.md, README.md | no |
| `rankzero-security-plugin-builder` | `~/Downloads` (S4) | 0.1.0 | SKILL.md, README.md | no |
| `rankzero-skill-admission-review` | `~/Downloads` (S4) | 0.1.0 | SKILL.md, README.md | no |
| `rankzero-threat-model-generator` | `~/Downloads` (S4) | 0.1.0 | SKILL.md, README.md | no |
| `rankzero-security-orchestrator` | `~/Downloads` (S4) | **0.1.0** | SKILL.md, README.md | no |
| `rankzero-project-memory` | vault package (D001) | — | SKILL.md, references/ | no |
| `json-canvas` | `kepano/obsidian-skills` | — | SKILL.md, references/ | SHA-256 |
| `obsidian-bases` | `kepano/obsidian-skills` | — | SKILL.md, references/ | SHA-256 |
| `obsidian-cli` | `kepano/obsidian-skills` | — | SKILL.md | SHA-256 |
| `obsidian-markdown` | `kepano/obsidian-skills` | — | SKILL.md, references/ | SHA-256 |

**Pinning asymmetry at this boundary:** the four third-party Obsidian skills
carry SHA-256 hashes in `skills-lock.json`; the eight RankZero packages carry no
hash, no source URL, and no lockfile entry. `skills-lock.json` is unchanged from
D001.

## Verification capability

| Capability | Present |
|---|---|
| JSON Schemas | none |
| Output fixtures | none |
| Validator script | none |
| `scripts/` directory | does not exist |
| CI | none |

## Vault content

| Directory | Count | Change from D001 |
|---|---|---|
| `03-Skills/` | 8 notes + registry stub | unchanged |
| `04-Decisions/` | 0 ADRs | unchanged |
| `07-Risks/` | 0 records | unchanged |
| `05-Research/` | 0 notes | unchanged |
| `11-Change-Log/` | rolling log only | unchanged |

Tracked files: 57 (43 at D001 boundary + 14).

## Declared skill set vs. installed package set

`12-Memory/Project Memory.md` lists a "Current Skill Set" of seven foundation
skills. All seven now have packages. The registry note that would map skill
notes to packages is still an embed-only stub — the vault's readable layer and
its package layer are not yet cross-referenced at this boundary.

## Roadmap

Phase 1 — Foundation: 8 of 8 complete (unchanged).
Phase 2 — Engineering: 0 of 9 complete (unchanged).
