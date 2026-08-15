# D009 — OUTCOME_SEALED

Everything below became visible **after** 2026-07-20 23:16:05 −0400. Because
this is the corpus's terminal commit, almost all of it comes from the
2026-08-15 reconstruction rather than from later project artifacts.

---

## The first roadmap item was never done

The baseline's immediate roadmap opened with:

> 1. Review and integrate `285c748` into the canonical gateway branch through
>    the normal repository workflow.

**Verified 2026-08-15, 26 days later:**

```
$ git ls-remote https://github.com/jayhaving/agentic-iam-gateway
38ca81f431dd20056def093dc5f6f0a9a1ee8199   HEAD
38ca81f431dd20056def093dc5f6f0a9a1ee8199   refs/heads/main
13e79c8b2e607e07cfc0629f89cb8654edc5383e   refs/heads/v4-session13

$ git cat-file -t 285c748065a014a202b66a2638e5b86c8361daa3
fatal: git cat-file: could not get object info
```

`285c748` was never pushed. Two branches, no tags, and `main` still sits at
`38ca81f` — an "Initial commit" from 2026-07-13 that does not contain the V4
gateway at all.

## What that means for the published baseline

The baseline report is honest about its own scope: it says the remediation was
"not pushed or merged," and it scopes every closure claim to the local branch.
It made no claim that later turned out false.

But the consequence is structural, and it is the single most important later
fact about this episode: **the baseline's verified-improvement half is now
unverifiable.** Its pre-remediation half — every finding at `13e79c8` — remains
fully re-verifiable in the public repository, and this reconstruction confirmed
the central ones at source level. Its post-remediation half rests entirely on a
commit that exists, if anywhere, on one workstation.

| Half of the baseline | Reachable today | Re-verified here |
|---|---|---|
| Pre-remediation findings at `13e79c8` | yes, public | yes — `/mint`, revocation, `llm.rs`, dashboard assets, test count |
| Remediation and 44/44 + 6/6 at `285c748` | no | not possible |

## The other roadmap items

None of the baseline's four "Immediate" items has a reachable outcome:

| Item | State 2026-08-15 |
|---|---|
| Integrate `285c748` into the canonical branch | not done — commit absent |
| Restore reproducible tracked dashboard build inputs | not done — `soc-dashboard/dist` still untracked at `13e79c8`, verified `git ls-files \| grep -c` → 0 |
| Add CI running the suites from a clean checkout | not done — neither repository contains any CI configuration |
| Preserve and require the `X-RankZero-Denial` marker | not observable — the marker exists only in the unreachable commit |

## An internal disagreement was left standing

The baseline states that `285c748` remediates RISK-001, RISK-003, and RISK-004,
and partially remediates RISK-002 and RISK-006. The six risk records themselves
were not updated: all six still read `status: open` at S1 HEAD. The vault's two
documents therefore describe different states, with no artifact reconciling
them.

## Both repositories went quiet

| Repository | Last commit | Last push (GitHub metadata) | Commits since |
|---|---|---|---|
| `rankzero-security-os` | 2026-07-20 23:16:05 | 2026-07-21 03:21 | 0 |
| `agentic-iam-gateway` | 2026-07-20 01:39:22 | 2026-07-21 | 0 |

The vault was pushed roughly four hours after this commit and never written to
again. Whether work continued elsewhere — on the workstation, in another
repository, or not at all — is UNKNOWN from the reachable record.

## What the corpus produced, end to end

In one 3h 56m session on 2026-07-20, starting from an empty repository:

- a memory substrate and its conventions (D001);
- 14 skill packages, 5 with schemas and fixtures (D002, D003, D004, D007);
- 5 ADRs, none superseded (D003–D008);
- a 426-line dependency-free validator (D004, D007);
- a reconciliation that inverted a 34/34 headline into a verified revocation
  defect (D006);
- 7 verified vulnerabilities and 6 risk records against a real executable
  (D007, D008);
- a 274-line baseline that declines to claim readiness (D009).

And, in the reachable record, zero lines of remediated product code.

## Not an evaluation

This file records outcomes and later observations. It takes no position on
whether publishing the baseline in this form was correct, and it does not assess
the engineering of either system.
