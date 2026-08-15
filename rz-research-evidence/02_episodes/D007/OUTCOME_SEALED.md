# D007 — OUTCOME_SEALED

Everything below became visible **after** 2026-07-20 22:07:24 −0400.

---

## The grounding condition held for the rest of the corpus

`rankzero-api-security-review` remained at version 0.1.0 through S1 HEAD, and no
later commit revised its route inventory or checks. The three remaining Phase 2
items — MCP Security Review, RAG Security Review, Cloud and Infrastructure
Review — remain **unchecked** at S1 HEAD.

Under the rule decided here, each of those three would require an observed
executable surface of its own before being built. No such surface entered the
corpus, and none of the three was built. The rule's effect on the roadmap is
therefore observable: the skill with an evidence base shipped; the three without
one did not.

## The findings this episode grounded were acted on within 69 minutes

The gateway review recorded seven verified vulnerabilities and three
missing-control classes. The baseline report at `ba9d042` (23:16) states that a
separate gateway commit, `285c748065a014a202b66a2638e5b86c8361daa3`, remediates
the nine prioritized defects for the tested paths, with recorded results of
44/44 Python methods and 6/6 Rust unit tests.

The API surface changed materially in that remediation, per the baseline report:
`/mint` gained `X-Admin-Key` enforcement, outbound headers moved to a positive
allowlist, and an `X-RankZero-Denial` marker was added so an upstream 401 could
no longer masquerade as gateway enforcement in tests.

## Later discovery — the remediated surface is not reachable

**Verified in this reconstruction on 2026-08-15:** commit `285c748` does not
exist in the public gateway repository.

```
$ git cat-file -t 285c748065a014a202b66a2638e5b86c8361daa3
fatal: git cat-file: could not get object info
```

The remote advertises two refs — `main` at `38ca81f` and `v4-session13` at
`13e79c8`. Consequently the API surface that ADR-004 grounded the skill in is
**still the current public surface**, and the remediated surface exists in the
reachable record only as prose.

Re-verified at `13e79c8` today, unchanged:

- `/mint` (`gateway.rs:204`) — handler at 219 has no `verify_admin_key` call
- `/api/secure-action` (`gateway.rs:210`) — handler at 270 has no `verify_admin_key` call
- `/api/kms/domains` (`proxy.rs:98`) and `/api/telemetry` (`telemetry.rs:20`) — no authentication observed
- revocation key mismatch between `gateway.rs` write and `auth.rs:129–142` read

## The deployment-surface limitation was never resolved

ADR-004 accepted "Unknown deployment activation remains an architectural
limitation." `RISK-005-Deployment-Surface-Drift` was opened in the same commit
and, per the baseline report's status table, is the one risk that commit
`285c748` "does not close." At S1 HEAD it remains `status: open`, and no
deployment observation exists anywhere in the corpus.

## Two pipeline stages stayed outside the validator

`validate_evaluation_outputs` maps exactly five skills to five filenames. Three
of the eight real-code outputs — `architecture-discovery.json`,
`threat-model.json`, and `orchestrated-review.json` — have no schema and are not
loaded by the validator, so the ADR's claim that "real-code output" passes
validation is true of five files rather than all eight.

## The finding taxonomy outlived the episode

The orchestrator's 0.4.0 "six-class finding taxonomy" and the `RZ-###`
identifiers introduced here are the vocabulary the baseline report uses 69
minutes later to state remediation status per finding. No later artifact
renames or renumbers them.

## Not an evaluation

This file records outcomes and later observations. It takes no position on
whether gating the skill on observed evidence was the right call.
