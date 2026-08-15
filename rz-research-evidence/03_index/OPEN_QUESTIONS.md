# Open questions

Everything this reconstruction could not establish, with what would resolve it.
Listed so a future reader can distinguish "not investigated" from "investigated
and not findable."

## Unreachable evidence — the largest single gap

| Question | What would resolve it |
|---|---|
| What is in commit `285c748065a014a202b66a2638e5b86c8361daa3`? | Pushing the `remediation/security-boundaries` branch, or any archive of the workstation clone. Everything the baseline report claims about remediation depends on it |
| Did the 44/44 Python and 6/6 Rust runs happen as recorded? | A run log, CI record, or reproducible checkout. None exists in either repository |
| Did the 34-method run, the `cargo build --locked` attempts, and the SQLite audit inspection happen as recorded? | Same. The reconciliation's runtime evidence is VAULT-ASSERTED throughout |
| Are the `~/Downloads` specialist packages identical to what was installed? | The originals, or a recorded digest. `skills-lock.json` never covered them |
| What did `/Users/jasonawuah/Desktop/RANKZERO_CONTEXT_BUNDLE.md` contain? | The file. Note that the *tracked* `docs/CONTEXT_BUNDLE.md` in the gateway repo is reachable and was used instead; whether the two are identical is unknown |

## Claims with no locatable origin

`GAP-020`, `GAP-021`, a property-based redaction test, a mutation harness, and
commits `ea65dd2` and `5f92e35` were all in scope for the D006 reconciliation,
and none of the six strings appears anywhere in either reachable repository —
not in the context bundle, not in the gateway's own gap log (which stops at
`GAP-016`), not in the vault.

The reconciliation note says of two of them: "The requested identifiers imply
prior historical context outside the located bundle."

**Where these claims came from is the sharpest unresolved question in the
corpus.** The word "requested" suggests they entered as an instruction rather
than from a document, but no request, transcript, or session record exists.
Resolving it would require the session history of whatever produced the
reconciliation.

## Process and authorship

| Question | Status |
|---|---|
| Was one person involved, or more? | UNKNOWN. Author equals committer on all 8 commits; no trailers, reviews, issues, or PRs. The identity change at `17a50b7` is a git-config change, not evidence of a second person |
| What degree of AI assistance produced the vault documents? | UNKNOWN. The gateway repo shows explicit AI session handoffs (`Codex session instructions`, `NEXT_TASK.md`); the vault shows skill packages but no transcript or tool log |
| Why was the `YOUR_GITHUB_EMAIL` placeholder never corrected? | UNKNOWN |
| What happened in the 17h 41m between the gateway tip and the vault's first commit? | UNKNOWN. No commit in either repository |
| Why did both repositories go silent after 2026-07-21? | UNKNOWN. 26 days with no commit as of observation |

## Decisions with no recorded rationale

| Decision | What is missing |
|---|---|
| D001 — the memory substrate | No ADR, no alternatives. Recorded only as change-log lines and README setup steps |
| D002 — "upload specialist skills individually", "orchestrator last" | Bare imperatives; no reasoning recorded |
| D004 — batching four skills into one commit | Departs from D002's "individually" rule with no note reconciling the two |
| D007 — ADR-004 has no "Alternatives Considered" section | Unlike ADR-001, ADR-002, and ADR-003, which each list three |

## Verification artifacts named but absent

| Named in | Artifact | Status |
|---|---|---|
| D003 change note | "Skill structure validation", "YAML and JSON syntax checks", "Repository link and placeholder checks" | No script, config, or output in the repository |
| D009 baseline | Status evidence verifier, no-unwrap check, secret screen, `git diff --check` | Live in the unreachable remediation change set |
| D003 ADR-001 | The validation fixture (stale docs, undocumented component, gateway bypass path) | Never created at any commit |
| D004 ADR-002 | Cross-skill end-to-end fixtures | Never created; a real target was used instead |

## Internal inconsistencies left unresolved by the corpus

| Inconsistency | Detail |
|---|---|
| Risk status | The baseline says `285c748` remediates RISK-001/003/004 and partially 002/006; all six `RISK-*` files still read `status: open` at HEAD |
| Route count | The vault says "11 named HTTP/WebSocket routes"; a direct count gives 10 named + 1 wildcard + 1 fallback |
| Memory rule 5 | "Record failed experiments and rejected approaches" — no experiment record exists; the experiment template is never instantiated |
| Validator coverage | Architecture Discovery and Threat Model Generator are pipeline stages with real-code outputs, no schemas, and no validator entry |

## Saddle Engineering

No artifact naming "Saddle Engineering" exists in the reachable corpus. A
case-insensitive search for `saddle` across the entire RankZero vault returns
zero files. Its relationship to these episodes is UNKNOWN, and per the
instructions governing this reconstruction it is neither evaluated nor
characterized anywhere in this workspace.

## What would most improve this reconstruction

In descending order of value:

1. The `remediation/security-boundaries` branch — it would convert the entire
   second half of the baseline from VAULT-ASSERTED to verifiable.
2. Any session transcript from 2026-07-20 evening — it would date decisions
   rather than bounding them, and would likely resolve the Source B claim origin.
3. The workstation's `~/Downloads` skill packages — they would settle the
   provenance of eight of the fourteen RankZero skill packages.
