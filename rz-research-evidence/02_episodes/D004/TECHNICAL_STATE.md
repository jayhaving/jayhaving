# D004 — TECHNICAL_STATE

State at the episode boundary: S1 `54976fd` (2026-07-20 21:03:10 −0400).
Shared with D005.

## Pipeline as of this boundary

```
Architecture Discovery → Asset Discovery → Threat Model Generator
  → Attack Surface Mapper → Authentication Review → Authorization Review
```

Six stages ordered. No stage had processed a real evidence set.

## Skill inventory

| Package | Version | Schema | Valid fixture | Invalid fixture | Agent manifest |
|---|---|---|---|---|---|
| `rankzero-architecture-discovery` | 0.1.0 | — | — | — | yes |
| `rankzero-asset-discovery` | 0.1.0 | yes | yes | yes | yes |
| `rankzero-attack-surface-mapper` | 0.1.0 | yes | yes | yes | yes |
| `rankzero-authentication-review` | 0.1.0 | yes | yes | yes | yes |
| `rankzero-authorization-review` | 0.1.0 | yes | yes | yes | yes |
| `rankzero-threat-model-generator` | 0.1.0 | — | — | — | — |
| `rankzero-security-orchestrator` | **0.3.0** | — | — | — | — |
| 5 other RankZero packages | 0.1.0 / — | — | — | — | — |

Two of the six pipeline stages — Architecture Discovery and Threat Model
Generator — carry no schema at this boundary.

## Verification capability (new in this episode)

`scripts/validate_phase2_skills.py`, 345 lines, standard library only
(`json`, `re`, `sys`, `pathlib`, `typing`):

| Function | Line | Checks |
|---|---|---|
| `validate_skill_package` | 63 | frontmatter, version, metadata, placeholders, line limits |
| `resolve_pointer` / `walk_refs` | 120 / 132 | local `$ref` resolution |
| `validate_schema_document` | 146 | Draft 2020-12 document structure |
| `validate_instance` | 190 | fixture-against-schema validation |
| `detect_literal_secrets` | 242 | rejects `token`/`secret`/`password`/`api_key`/`private_key`/`cookie`/`credential_value` keys and secret-shaped values |
| `unique_ids` | 263 | identifier uniqueness |
| `validate_confidence_values` | 270 | 0.0–1.0 confidence scale |
| `validate_cross_references` | 284 | identifier agreement between specialist outputs |

Declared scope at this commit:

```python
PHASE2_SKILLS = (
    "rankzero-asset-discovery",
    "rankzero-attack-surface-mapper",
    "rankzero-authentication-review",
    "rankzero-authorization-review",
)
EXPECTED_VERSION = "0.1.0"
```

Four of the six pipeline stages are covered. There is no function for validating
real-code evaluation output at this boundary — the validator checks the
project's own fixtures only.

## Vault content

| Directory | Count |
|---|---|
| `04-Decisions/` | 3 ADRs |
| `07-Risks/` | 0 records |
| `05-Research/` | 0 notes; `evaluations/` does not exist |
| `11-Change-Log/` | 2 dated entries |
| `03-Skills/` | 13 skill notes + registry |
| `scripts/` | 1 file |

Tracked files: 90.

## Roadmap

Phase 1: 8 of 8. **Phase 2: 5 of 9** — Architecture Discovery, Asset Discovery,
Attack Surface Mapper, Authentication Review, Authorization Review complete;
API, MCP, RAG, and Cloud/Infrastructure open.

## External systems

Still none. No target repository or commit hash appears in S1 at this boundary.
