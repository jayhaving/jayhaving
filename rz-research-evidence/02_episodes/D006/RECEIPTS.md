# D006 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D006-01 | Decision moment bound; author | S1 `df3cacefe0ddd1d5c9ca1a4e7e2901a92b8f785d`, `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 21:33:10 −0400 | VERIFIED-HERE |
| R-D006-02 | Review system state 30 minutes earlier | S1 @ `54976fd`: 4 schemas, 4 valid + 4 invalid fixtures, `scripts/validate_phase2_skills.py` (345 lines), roadmap Phase 2 five items `[x]` | VERIFIED-HERE |
| R-D006-03 | ADR-002 awaited a representative target | S1 `04-Decisions/ADR-002-Phase-2-Evidence-Pipeline.md` @ `54976fd`, "## Follow-up", second bullet | VERIFIED-HERE |
| R-D006-04 | Prototype ref and its age at the decision moment | S2 `git log -1 --format='%H %ad' v4-session13` → `13e79c8b2e607e07cfc0629f89cb8654edc5383e`, 2026-07-20 01:39:22 −0400. Still the advertised tip on 2026-08-15 | VERIFIED-HERE |
| R-D006-05 | Prototype module and test inventory | S2 @ `13e79c8`: `v4-single-binary/src/` → `auth.rs`, `behavior.rs`, `db.rs`, `ebpf.rs`, `gateway.rs`, `llm.rs`, `main.rs`, `proxy.rs`, `telemetry.rs`, `web.rs`. `grep -c '    def test_' tests/test_security_boundaries.py` → 34 | VERIFIED-HERE |
| R-D006-06 | Context bundle content and size | S2 `docs/CONTEXT_BUNDLE.md` @ `13e79c8`, 5,549 lines. Quoted rows at lines 49, 51, 60, 67, 71, 114, 185, 252, 334, 342 | VERIFIED-HERE |
| R-D006-07 | Five claims have no locatable origin in the reachable corpus | S2 @ `13e79c8`, case-insensitive counts: `GAP-020` → 0, `GAP-021` → 0, `proptest` → 0, `property-based` → 0 in bundle, `ea65dd2` → 0, `5f92e35` → 0, across the whole working tree excluding `.git`. `docs/vault/04-Known-Gaps-and-Honesty-Log.md` defines `GAP-001` … `GAP-016` and no higher identifier. S1 contains no definition of any of them either | VERIFIED-HERE (absence within corpus) |
| R-D006-08 | The reconciliation note: question, posture, scope prohibitions, confidence table, search scope, absence caveat, "no new architecture decision" | S1 `05-Research/2026-07-20-Rust-Prototype-Reconciliation.md` @ `df3cace` — created in this commit; sections "Question", "Scope and Method", "Confidence basis", "Source", "RankZero Implications" item 6, "Limitations", "Decisions Influenced" | VERIFIED-HERE (as the project's own record) |
| R-D006-09 | A prior test-quality audit existed 20 hours earlier, and Test 04 was unflagged in it | S2 `docs/vault/10-Test-Quality-Audit.md`, 193 lines, added at `bae9842` (2026-07-20 01:33:39 −0400). Section "1. Tautology and Requirement-Traceability Findings": Test 04 classified `TRACEABLE`; Tests 09, 10, 12, 07, 01 classified `TRACEABLE / WEAK`; Test 13 `CHARACTERIZATION — FLAGGED`. Method section defines the four labels | VERIFIED-HERE |
| R-D006-10 | An active scoped task barred mutation testing | S2 `docs/vault/NEXT_TASK.md` @ `13e79c8`, line 9: "Do not run mutation testing."; line 5 lists four test-quality fixes to make first | VERIFIED-HERE |
| R-D006-11 | Prototype status file was stale at the decision moment | S2 `docs/vault/status.json` @ `13e79c8`, `_meta`: `last_verified: "2026-07-17T03:39:03Z"`, `last_verified_session: 8`, `total_tests_passing: 34`, `test_file: "tests/test_security_boundaries.py"` | VERIFIED-HERE |
| R-D006-12 | The posture is an application of ADR-003 | S1 `04-Decisions/ADR-003-Deterministic-Checks-Are-Authoritative.md` @ `54976fd`, "## Decision"; reconciliation note "Scope and Method" paragraph 2 restates it | VERIFIED-HERE |
| R-D006-13 | Commit touched no skill package and added no ADR | S1 `git show --name-status df3cace` → 5 paths: `A 05-Research/2026-07-20-Rust-Prototype-Reconciliation.md`, `A 11-Change-Log/2026-07-20-Rust-Prototype-Reconciliation.md`, `M 02-Architecture/Current Architecture.md`, `M 11-Change-Log/Change Log.md`, `M 12-Memory/Project Memory.md`. No `.agents/skills/` path, no `04-Decisions/` path | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| The origin of `GAP-020`, `GAP-021`, the property-based redaction test, the mutation harness, `ea65dd2`, and `5f92e35` | Zero occurrences in either reachable repository. Whether they came from a request, a recollection, or an unreachable record is UNKNOWN |
| `/Users/jasonawuah/Desktop/RANKZERO_CONTEXT_BUNDLE.md` | Local macOS path (S4). Note the *tracked* `docs/CONTEXT_BUNDLE.md` in S2 **is** reachable and is used above; whether the two files are identical is UNKNOWN |
| The scratch clone at `/Users/jasonawuah/.gemini/antigravity-ide/scratch/agentic-iam-gateway` | Local path (S4) |
| Any log of the enumerated searches (reflogs, stashes, unreachable objects) | No output was recorded; the search is described, not captured |
| Whether the decision to reconcile was prompted or self-initiated | No artifact addresses it |
