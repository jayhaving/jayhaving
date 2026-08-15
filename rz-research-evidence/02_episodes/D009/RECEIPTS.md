# D009 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D009-01 | Decision moment bound; author; terminal commit | S1 `ba9d042fb83f67c0622f38dc85c0408f80524aec`, `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 23:16:05 −0400. `git log` shows no later commit on any S1 ref as of 2026-08-15 | VERIFIED-HERE |
| R-D009-02 | State inherited from the prior commit | S1 @ `6cb5ef0`: 5 ADRs, 6 `RISK-*` files, `Known Gaps.md`, `05-Research/2026-07-20-Rust-Gateway-Security-Review.md`, 8 JSON under `05-Research/evaluations/rust-gateway-13e79c8/` | VERIFIED-HERE |
| R-D009-03 | Baseline report content: scope callout, two-commit distinction, five branch properties of `285c748`, per-finding status table, closure-claim scoping, required disclosures, staged roadmap, `X-RankZero-Denial` rationale | S1 `05-Research/RankZero Security Baseline Report v0.1.md` @ `ba9d042` — 274 lines, created in this commit. Sections 1, 2, 3, 5, 6, 7, 8, 9 and the head callout | VERIFIED-HERE (as the project's own record) |
| R-D009-04 | `285c748` is not reachable | S2 full clone, 2026-08-15: `git cat-file -t 285c748065a014a202b66a2638e5b86c8361daa3` → "fatal: git cat-file: could not get object info". `git ls-remote` advertises only `refs/heads/main` (`38ca81f…`) and `refs/heads/v4-session13` (`13e79c8…`) | VERIFIED-HERE (absence at the remote) |
| R-D009-05 | The six validation results and the test-count change | S1 same report, section 7 "Validation Evidence", complete-suites table and replay/tenant/Rust test lists. Pre-remediation counts (34 Python, 0 Rust) from `05-Research/2026-07-20-Rust-Prototype-Reconciliation.md` @ `df3cace` | VAULT-ASSERTED — no run log, artifact, or CI record exists in S1 or S2 at any commit |
| R-D009-06 | The precedent the 44/44 headline had to answer | S1 `05-Research/2026-07-20-Rust-Prototype-Reconciliation.md` @ `df3cace`, "Executive Result" and section 3: Test 04 passed on an upstream 401 after RankZero recorded `PROXY_ALLOWED`. Independently confirmed at source: revocation key mismatch between `gateway.rs` (`agent:<id>`) and `auth.rs:129–142` (sha256 of the token) | VERIFIED-HERE for the mechanism; VAULT-ASSERTED for the runtime observation |
| R-D009-07 | Commit scope: five paths | S1 `git show --stat ba9d042` → `05-Research/RankZero Security Baseline Report v0.1.md` (+274), `05-Research/Research Index.md` (+6), `11-Change-Log/2026-07-20-Security-Baseline-Report-v0.1.md` (+35), `11-Change-Log/Change Log.md` (+1), `12-Memory/Project Memory.md` (+20 −3). No skill, schema, script, or ADR path | VERIFIED-HERE |
| R-D009-08 | Roadmap state at publication | S1 `09-Roadmap/Roadmap.md` @ `ba9d042`: Phase 1 8/8; Phase 2 main list 6 of 9 `[x]`; Phase 2 Evidence Status 3 of 4, the unchecked item being "Remediate the verified prototype vulnerabilities in its owning repository; remediation is intentionally outside this skills-repository review batch"; Phases 3 and 4 fully unchecked | VERIFIED-HERE |
| R-D009-09 | All six risk records remain open | S1 `grep -h '^status:' 07-Risks/RISK-00*.md` @ `ba9d042` → `status: open` × 6 | VERIFIED-HERE |
| R-D009-10 | Tracked file count at the terminal commit | S1 `git ls-tree -r --name-only ba9d042 \| wc -l` → 120 | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| Commit `285c748` and its diff | Not present at the S2 remote; existed only on a local branch |
| The 44/44 Python run and the 6/6 Rust run | No log, artifact, or CI record anywhere. VAULT-ASSERTED |
| The status evidence verifier, no-unwrap check, and secret screen | Named as passing; the scripts themselves are in the unreachable remediation change set, not in S1 |
| Whether the remediation was reviewed by anyone | No review artifact exists |
| Why the remediation branch was not pushed | Not recorded. The report states the fact and makes integration the first roadmap item |
| Any decision record for the remediation work itself | The remediation happened in S2's working tree between 22:07 and 23:16 and produced no reachable artifact. It is described only from the outside, by the vault |
