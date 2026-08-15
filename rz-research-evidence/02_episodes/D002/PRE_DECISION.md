# D002 — PRE_DECISION

**Episode:** Install downloaded specialist skills unmodified; version the orchestrator; decline the non-RankZero review file

**This episode has three separately datable moments** `[R-D002-01]` `[R-D002-02]` `[R-D002-08]`:

| Component | Bound | Receipt commit |
|---|---|---|
| Installation policy ("individually", "orchestrator last", "versioned assets") | ≤ 2026-07-20 19:20:25 −0400 | `b8638a1` |
| Execution of the installation | 2026-07-20 20:33:36 −0400 | `17a50b7` |
| Admission judgment on the CyberForge file; unmodified-install audit | ≤ 2026-07-20 20:42:10 −0400 | `b2fa397` |

**Decision maker of record:** `jayhaving` at 19:20:25, `Jason Awuah` at 20:33:36 and 20:42:10 — the same git configuration changed between commits; see `00_method/PROVENANCE_NOTES.md`. Whether more than one person was involved is UNKNOWN.

---

## Situation as visible when the installation policy was recorded (≤ 19:20:25)

Three installation rules were written into the change log at vault
initialization, before any specialist package entered the repository
`[R-D002-01]`:

> - Upload specialist skills individually.
> - Upload the security orchestrator last.
> - Treat skills as versioned software assets, not static prompts.

At that moment the vault contained eight *skill notes* under `03-Skills/` and
zero RankZero specialist *packages* under `.agents/skills/` `[R-D002-03]`. The
seven foundation skills were declared complete on the roadmap `[R-D002-04]`.

The packages themselves were held at a local path, `~/Downloads` `[R-D002-05]`.
That path is not reachable from this reconstruction (S4), so their contents at
19:20:25 are UNKNOWN except as later described by the vault.

No document states *why* individual upload was preferred over a bulk import, or
why the orchestrator specifically was to be last. Both rules are recorded as
bare imperatives `[R-D002-01]`. Any rationale is UNKNOWN.

**INFERENCE:** "orchestrator last" follows from the orchestrator's own stated
function — it "routes work rather than duplicating specialist instructions" and
is the "entry point," so it references specialists that must exist for its
routing to be meaningful `[R-D002-06]`. Basis: the orchestrator SKILL.md text
present in the installed package. The reasoning step — that dependency direction
motivated ordering — is not stated in any artifact.

## Situation as visible at execution (20:33:36)

Fourteen files were committed: seven RankZero specialist packages, each a
`SKILL.md` plus a `README.md` `[R-D002-02]`:

| Package | Installed version |
|---|---|
| `rankzero-agent-call-lifecycle` | 0.1.0 |
| `rankzero-context-isolation` | 0.1.0 |
| `rankzero-runtime-debug` | 0.1.0 |
| `rankzero-security-plugin-builder` | 0.1.0 |
| `rankzero-skill-admission-review` | 0.1.0 |
| `rankzero-threat-model-generator` | 0.1.0 |
| `rankzero-security-orchestrator` | 0.1.0 `[R-D002-07]` |

The orchestrator's frontmatter at installation carries
`metadata.version: "0.1.0"` and `license: Apache-2.0`, and declares itself the
routing entry point `[R-D002-06]` `[R-D002-07]`.

`03-Skills/Skill Registry.md` remained an embed-only stub at this moment — the
per-skill registry notes were not written as part of the installation
`[R-D002-09]`.

The installation commit carries no accompanying vault prose. It modified no
note, no change-log entry, and no ADR `[R-D002-02]`.

## Situation as visible at the admission judgment (≤ 20:42:10)

Nine minutes after execution, an audit was recorded in project memory
`[R-D002-08]`:

> - All seven specialist packages found in `~/Downloads` were installed and matched their source files at audit time.
> - Six remain byte-for-byte unchanged; `rankzero-security-orchestrator` was intentionally advanced from the downloaded 0.1.0 package to 0.2.0 to route Architecture Discovery.
> - `rankzero-project-memory` is installed from the vault package.
> - The loose `cyberforge-security-review` file is not installed because it is not a RankZero specialist and its referenced `schemas/` and `references/` package content is absent.

The same judgment appears as a rejected alternative in the ADR committed in that
same commit: "Install the loose CyberForge review file from Downloads: rejected
because it is not a RankZero specialist and references missing schemas and
guidance files" `[R-D002-10]`.

Two stated grounds for declining, both recorded `[R-D002-08]` `[R-D002-10]`:

1. Provenance — the file is not a RankZero specialist.
2. Completeness — its referenced `schemas/` and `references/` content is absent.

**Whether the CyberForge file was evaluated at 20:33 (during installation) or
between 20:33 and 20:42 is UNKNOWN.** The evidence dates only the *record* of
the judgment, not the judgment. **INFERENCE:** it was contemporaneous with the
installation sweep, because the audit frames it as part of the same `~/Downloads`
enumeration that produced the seven installed packages. Basis: shared source
path in the audit text; reasoning step is co-location in one enumeration.

The CyberForge file itself is UNAVAILABLE (S4). Its contents, size, author, and
the identity of "CyberForge" cannot be established from this corpus
`[R-D002-11]`.

---

## The decision

1. Install the seven `~/Downloads` specialist packages into the vault, one
   package per unit, byte-for-byte unmodified `[R-D002-08]`.
2. Exempt the orchestrator from the unmodified rule and version it deliberately
   as routing scope grows `[R-D002-08]`.
3. Decline the CyberForge review file on provenance and package-completeness
   grounds `[R-D002-08]` `[R-D002-10]`.
4. Treat skills as versioned software assets rather than static prompts
   `[R-D002-01]`.

---

## Verification state at the decision moment

No validator existed. The vault contained no schema, fixture, or checking script
at any of this episode's three moments `[R-D002-12]`. The claim that six packages
"remain byte-for-byte unchanged" was, at the time it was written, an assertion
about a comparison performed against `~/Downloads` — the comparison itself has no
recorded output `[R-D002-08]`.

The installed packages carry `SKILL.md` and `README.md` only. None of the seven
carries a JSON Schema, fixture, or test at this episode's boundary
`[R-D002-13]`.
