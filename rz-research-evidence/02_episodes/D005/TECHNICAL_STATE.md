# D005 — TECHNICAL_STATE

State at the episode boundary: S1 `54976fd` (2026-07-20 21:03:10 −0400).
Shares the commit with D004; this file records the state relevant to the
deterministic/interpretive boundary.

## The authority boundary as of this boundary

| Category ADR-003 calls authoritative | Implemented in the repository? |
|---|---|
| Schema validation | **yes** — `validate_schema_document`, `validate_instance` |
| Check results (structure, uniqueness, cross-reference) | **yes** — `unique_ids`, `validate_cross_references` |
| Graph reachability | no implementation |
| Policy evaluation | no implementation |
| Regression-test results | no suite exists |

Two of five authoritative categories are executable in the repository at this
boundary. The other three are authoritative by declaration.

## Deterministic tooling present

| Artifact | Size | Dependencies |
|---|---|---|
| `scripts/validate_phase2_skills.py` | 345 lines | stdlib only: `json`, `re`, `sys`, `pathlib`, `typing` |

Coverage: `rankzero-asset-discovery`, `rankzero-attack-surface-mapper`,
`rankzero-authentication-review`, `rankzero-authorization-review`.
`EXPECTED_VERSION = "0.1.0"`.

## Schema-level expression of the boundary

Each of the four new packages ships `schemas/output.schema.json` (Draft 2020-12)
with output separated into deterministic checks, evidence, confidence, and
findings — the first ADR-003 consequence expressed as a contract rather than a
convention.

Each package also ships a **deliberately invalid** fixture at
`tests/invalid-output.json`. The negative case is part of the shipped artifact
set, so failure behavior is exercised rather than assumed.

## Model-in-the-loop surface

| Surface | Model involved? |
|---|---|
| Schema and fixture validation | no — pure Python |
| Identifier cross-referencing | no |
| Secret screening | no |
| Confidence scale enforcement | no (range check only) |
| Producing specialist output content | yes — the skills are prompts executed by an agent |
| Interpreting and prioritizing findings | yes, by design |

No transcript, tool log, or run record for the model-driven side exists in the
repository at this boundary or any later one.

## Vault content

Tracked files: 90. `04-Decisions/`: 3 ADRs. `07-Risks/`: 0. `05-Research/`: index
only. `scripts/`: 1 file.

## External systems

None referenced.
