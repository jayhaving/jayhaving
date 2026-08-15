# D006 — PRE_DECISION

**Episode:** Reconcile the recovered Rust prototype before building on its claims
**Decision moment:** at or before 2026-07-20 21:33:10 −0400 `[R-D006-01]`
**Decision maker of record:** `Jason Awuah` `[R-D006-01]`
**Participants beyond the commit author:** UNKNOWN

This is the first episode in which the review system is pointed at a real
system. The decision under reconstruction is a **scope and posture decision** —
what to verify, what authority to give the existing record, and what to withhold
until verification completes. The *results* of the verification are outcomes and
appear in OUTCOME_SEALED.md.

---

## Situation as visible at the decision moment

### The review system was complete and untested against real evidence

Thirty minutes earlier, Phase 2 stood at 5 of 9, with a six-stage pipeline, four
JSON Schemas, eight fixtures, and a 345-line validator `[R-D006-02]`. ADR-002's
follow-up explicitly awaited a target: "Add cross-skill end-to-end fixtures when
a representative target is available" `[R-D006-03]`.

### A prototype existed and was reachable

The `agentic-iam-gateway` repository carried `origin/v4-session13` at
`13e79c8b2e607e07cfc0629f89cb8654edc5383e`, authored 2026-07-20 01:39:22 −0400
— 19h 54m before this decision `[R-D006-04]`. Its `v4-single-binary/src/`
contained ten Rust modules; `tests/test_security_boundaries.py` contained 34
`test_*` methods `[R-D006-05]`.

### The historical claim set, and where it came from

The claims to be reconciled came from **two sources of very different quality**.

**Source A — the tracked context bundle**, `docs/CONTEXT_BUNDLE.md`, 5,549 lines,
tracked in the prototype repository and therefore datable `[R-D006-06]`. Its
claims include:

| Claim | Bundle text |
|---|---|
| Test headline | "What is implemented and tested (34/34 tests passing)" |
| Capability headline | "13/13 capabilities verified, 34/34 tests passing" |
| Disposition | "This is a **working research prototype**, not production software" |
| Disposition | "It is not production-ready" |
| Secrets | "env-var `SecretProvider`, not a real KMS — see GAP-001" |
| Kernel enforcement | "eBPF kernel sensors … 🔴 Stub — Mock only on macOS; deferred for Linux VM" |
| `rz-launcher` | Session 13, 2026-07-19: "designed `rz-launcher` concept; opened GAP-016; **no code written**" |
| Detection limits | "Known bypass vectors (documented, not closed): Base64-encoded secrets, multilingual injection phrases, token-split injection … leetspeak" |

**INFERENCE:** the claim set available at this decision was already
self-hedged on production readiness, KMS, eBPF, `rz-launcher`, and detection
bypasses. Basis: the eight bundle rows above, all present at `13e79c8`. The
reasoning step — that these constitute prior disclosure rather than later
discovery — rests on the bundle being tracked in git at a datable commit.

**Source B — claims with no locatable origin.** Five items were in play whose
text appears **nowhere** in the reachable prototype repository, its bundle, its
vault, or S1 `[R-D006-07]`:

- `GAP-020`
- `GAP-021`
- a property-based redaction test
- a mutation harness
- commits `ea65dd2` and `5f92e35`

The reconciliation note itself records that the two commit identifiers came from
outside the located bundle: "The requested identifiers imply prior historical
context outside the located bundle" `[R-D006-08]`. **Where Source B claims
originated is UNKNOWN.** Their presence in the reconciliation's scope is
evidence that something — a request, a recollection, or a record on an
unreachable machine — asserted them.

### A prior self-audit already existed

The prototype's own vault contained `10-Test-Quality-Audit.md`, 193 lines,
committed 2026-07-20 01:33:39 — 20 hours before this decision `[R-D006-09]`. It
had already classified all 34 tests against four labels (TRACEABLE,
TRACEABLE/WEAK, CHARACTERIZATION — FLAGGED, INVALID FIXTURE — FLAGGED) and had
already recorded, among others `[R-D006-09]`:

- Test 13 "name still says `opa_fail_closed`" but "does not test startup fail-closed behavior" — flagged as characterization;
- Test 09 "only asserts 'status is not 403'" and "does not prove forwarding";
- Test 10 "does not cause, mock, or observe an LLM failure";
- Test 12 assertions "skipped whenever their APIs return non-200";
- Test 07 incident verification "conditional on `GET /api/incidents` returning 200."

Its stated method is notable as available context: a test whose only support was
"a description of the current implementation" was to be "classified as a
characterization test, not independent proof."

**Test 04 — the revoked-token test — was classified TRACEABLE in that audit and
was not flagged** `[R-D006-09]`.

### An active scoped task constrained the prototype work

`docs/vault/NEXT_TASK.md` at `13e79c8` carried an open task list and the explicit
line "Do not run mutation testing" `[R-D006-10]`.

### Staleness signal in the machine-readable status

`docs/vault/status.json` recorded `last_verified: 2026-07-17T03:39:03Z`,
`last_verified_session: 8`, `total_tests_passing: 34` `[R-D006-11]`. The
prototype's own status file was therefore three days stale relative to its tip
commit at the decision moment.

---

## The decision

Reconcile before building. Four components, all recorded in the research note
committed at this moment `[R-D006-08]`:

**1. Question.** "Which claims about the RankZero Rust prototype are supported by
current, reproducible evidence, and which claims remain historical, unavailable,
contradicted, or stale?"

**2. Evidence posture.** Historical bundles are "historical evidence only. Their
claims were not promoted to current state without independent verification."
Deterministic filesystem, Git, source, database, build, and test results are
authoritative; "Interpretation and confidence labels do not override those
results" — a direct application of ADR-003 `[R-D006-08]` `[R-D006-12]`.

**3. Scope limits, stated as prohibitions.** The review "was read-only with
respect to product code. It did not redesign or recreate the gateway, add API
Security Review, or add product features." Carried into the RankZero
implications as: "Keep API Security Review and new feature work out of scope
until this reconciliation commit is accepted" `[R-D006-08]`.

**4. A classification scheme decided in advance**, with confidence tied to
evidence type rather than belief `[R-D006-08]`:

| Level | Basis |
|---|---|
| High | Direct source, Git object, fresh build, fresh execution, or database evidence |
| Medium | Consistent historical documentation without current executable proof, or an exhaustive absence result limited to the searched evidence set |
| Low | Unsupported recollection or a claim whose evidence could not be located |

Findings were to be sorted into: Verified Current / Historical but Unverified /
Lost, Contradicted, or Stale.

### The declared search scope

Recorded before results `[R-D006-08]`: the vault and its git repository; the
attached historical bundle; user-home locations including Documents, Desktop,
Downloads, and the scratch repository; sibling repositories; local branches,
remote-tracking branches, worktrees, reflogs, stashes, reachable and unreachable
git objects, advertised remote heads and tags; and exact object lookups for
`ea65dd2`, `5f92e35`, and `13e79c8`.

With an explicit limit on what absence would mean: "Absence findings apply to
this enumerated evidence set; they do not prove that an object never existed on
an unavailable device or expired remote" `[R-D006-08]`.

---

## What was not decided here

No architecture decision was taken. The note records: "No new architecture
decision was made" `[R-D006-08]`. No ADR was written at this commit, and the
commit touched no skill package `[R-D006-13]`.
