# D002 — OUTCOME_SEALED

Everything below became visible **after** this episode's moments. None of it
appears in PRE_DECISION.md.

---

## The orchestrator exemption was exercised four times

The rule that six packages stay byte-for-byte unchanged while the orchestrator
is versioned deliberately held for the rest of the corpus:

| Version | Commit | Time | Reason recorded |
|---|---|---|---|
| 0.1.0 | `17a50b7` | 20:33:36 | as installed |
| 0.2.0 | `b2fa397` | 20:42:10 | route Architecture Discovery (D003) |
| 0.3.0 | `54976fd` | 21:03:10 | route the four Phase 2 specialists (D004/D005) |
| 0.4.0 | `6cb5ef0` | 22:07:24 | route API review and consolidate a six-class finding taxonomy (D007) |

Four versions in 1h 34m. The six other installed packages were modified in the
corpus only at `6cb5ef0`, and only their **vault notes** under `03-Skills/`
changed there — the packages under `.agents/skills/` for the six foundation
specialists were never edited after installation.

## The pinning asymmetry was never closed

`skills-lock.json` remains `version: 1` with four `kepano/obsidian-skills`
entries at S1 HEAD. No RankZero package ever acquired a hash, source URL, or
lockfile entry. Consequently, the audit claim that six packages "remain
byte-for-byte unchanged" from their `~/Downloads` originals is not
reconstructible: no recorded digest of the originals exists, and the originals
are on an unreachable filesystem.

## The registry stub was filled, in stages

`03-Skills/Skill Registry.md` was still embed-only at this episode. It was
modified at `54976fd` and again at `6cb5ef0`, and per-skill notes accumulated to
14 by S1 HEAD.

## Skill count at the end of the corpus

| Boundary | RankZero packages | Third-party packages |
|---|---|---|
| D002 (`17a50b7`) | 8 | 4 |
| S1 HEAD (`ba9d042`) | 14 | 4 |

Six packages were added after this episode: `rankzero-architecture-discovery`
(D003), `rankzero-asset-discovery`, `rankzero-attack-surface-mapper`,
`rankzero-authentication-review`, `rankzero-authorization-review` (D004/D005),
and `rankzero-api-security-review` (D007).

## The verification gap was closed for later packages, not for these

The five packages added at D004/D005 and D007 each carry a JSON Schema, a valid
fixture, and a deliberately invalid fixture, checked by
`scripts/validate_phase2_skills.py`. The seven packages installed in **this**
episode never acquired schemas or fixtures, and the validator does not cover
them — it is named and scoped to the Phase 2 set. At S1 HEAD, the seven earliest
specialist packages remain unvalidated by any script in the repository.

## The admission decision has no successor record

`rankzero-skill-admission-review` was installed in this episode as a skill for
reviewing skill admission. The CyberForge decline — the corpus's one actual
admission judgment — was recorded as prose in project memory and as an ADR
alternative, **not** as an output of that skill. No admission-review output
exists anywhere in the corpus.

## Later discovery — 2026-08-15

The seven specialist packages' provenance remains unestablished. Searching S1
for any reference to where they came from yields only the `~/Downloads` path in
the audit bullet. There is no upstream repository, release, or author recorded
for any RankZero specialist package. Whether they were authored by the project,
generated, or obtained elsewhere is UNKNOWN from the reachable corpus.

## Not an evaluation

This file records subsequent state. It takes no position on whether installing
unmodified, exempting the orchestrator, or declining the CyberForge file was
correct.
