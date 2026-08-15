# D009 — PRE_DECISION

**Episode:** Publish a security baseline without a production-readiness claim
**Decision moment:** at or before 2026-07-20 23:16:05 −0400 `[R-D009-01]`
**Decision maker of record:** `Jason Awuah` `[R-D009-01]`
**Participants beyond the commit author:** UNKNOWN

This is the terminal commit of the corpus. Nothing was written to either
repository afterward.

---

## Situation as visible at the decision moment

### Everything the review had produced, 69 minutes earlier

Five ADRs, six open risk records, a known-gaps taxonomy, a gateway security
review naming seven verified vulnerabilities and three missing-control classes,
and eight machine-readable specialist outputs `[R-D009-02]`.

### Work had happened in the other repository in the interval

Between 22:07:24 and 23:16:05 the reviewed defects were addressed in the
prototype's own repository. What the vault records about that work at this
moment `[R-D009-03]`:

- the commit is `285c748065a014a202b66a2638e5b86c8361daa3`;
- it was on **local branch** `remediation/security-boundaries`;
- the worktree was **clean**;
- it had **no upstream branch**;
- it was **"not pushed or merged into the gateway's default branch."**

Every one of those five properties is VAULT-ASSERTED. The commit is not
reachable from this reconstruction, and was not at the time reachable to anyone
but the author's workstation `[R-D009-04]`.

**The decision-maker knew this.** The unpushed, unmerged status is stated in the
baseline report's own executive summary rather than discovered later
`[R-D009-03]`.

### Recorded verification results available at the decision moment

| Evidence | Recorded result | Scope as recorded |
|---|---|---|
| Python security-boundary suite | 44/44 passed | fresh gateway and SQLite; external LLM and credential values removed; test-only signing/admin values |
| Rust unit suite | 6/6 passed | OPA failure, credential-provider failure, header isolation, gateway-only authorization header, LLM enforcement independence |
| Status evidence verifier | passed | 44 Python methods, 6 Rust tests, 15 capability claims |
| Draft 2020-12 status schema | passed | `status.json` schema and instance |
| No-unwrap check | passed | `auth.rs`, `proxy.rs`, `gateway.rs` |
| Python syntax, scoped Rust formatting, secret screen, `git diff --check` | passed | remediation change set |

All six rows are VAULT-ASSERTED `[R-D009-05]`. No run log, artifact, or CI
record exists in either repository at this or any commit.

The test count had moved from 34 to 44 Python methods and from 0 to 6 Rust
tests `[R-D009-05]`.

### Two commits with different roles, distinguished before publication

The report separates them explicitly `[R-D009-03]`:

- `6cb5ef0` — the RankZero vault commit recording the grounded review of the
  pre-remediation gateway. "It did not contain the gateway code remediation."
- `285c748` — the separate gateway repository commit containing the remediation.

### The problem the prior headline had created

D006 had established that a passing test count is not a security guarantee: the
34/34 headline had concealed broken revocation because Test 04 accepted an
upstream 401 `[R-D009-06]`. That precedent is directly relevant to publishing a
44/44 headline, and the report addresses it: the remediated suite "uses the
explicit denial marker for relevant assertions," and `X-RankZero-Denial`
"identifies gateway decisions so an upstream 401 or 403 cannot masquerade as
RankZero enforcement in tests" `[R-D009-03]`.

### What remained unverified at the decision moment

Recorded in the report itself `[R-D009-03]`:

- production deployment not validated; the remediation branch "was tested
  locally but was not pushed, merged … or exercised in an observed production
  deployment";
- `rz-launcher` not implemented;
- OS containment not implemented — no verified cgroup, namespace, seccomp,
  kernel, or eBPF enforcement;
- KMS not integrated — credentials are environment-backed;
- ML detection not implemented — deterministic regex, substring, and
  rolling-average logic with known bypasses;
- no DPoP server nonce; no replay/revocation/quarantine state shared across
  replicas;
- audit reads and telemetry not fully tenant-scoped; CORS permissive;
- `RISK-005-Deployment-Surface-Drift` not closed.

---

## The decision

Publish `RankZero Security Baseline Report v0.1` as the project's
evidence-backed baseline, with a **stated refusal to claim production
readiness**, carried in a callout at the head of the document `[R-D009-03]`:

> This report describes verified repository and test evidence. It does not
> establish production readiness. The executable scope is a Rust HTTP gateway;
> `rz-launcher`, OS containment, KMS integration, and ML detection are not
> implemented.

### Structural choices made at publication

1. **Required baseline disclosures as a named section.** Five non-implementation
   facts are given their own subsection rather than being distributed through the
   text `[R-D009-03]`.
2. **Closure claims scoped to their evidence.** "Closure claims apply to the
   local `remediation/security-boundaries` branch at `285c748` and the recorded
   test environment. They are not claims about an unobserved deployment"
   `[R-D009-03]`.
3. **Per-finding remediation status rather than a summary verdict.** A table maps
   each pre-remediation finding to its status at `285c748`, including partial
   entries — RZ-003 "nonce and distributed state remain open", RZ-006 "global
   observability remains", RZ-014 "no database fault-injection closure claim is
   made" `[R-D009-03]`.
4. **A staged security roadmap** whose first immediate item is "Review and
   integrate `285c748` into the canonical gateway branch through the normal
   repository workflow," followed by restoring reproducible dashboard build
   inputs and adding CI that runs the suites "from a clean checkout"
   `[R-D009-03]`.

### Scope of the commit

Five paths `[R-D009-07]`: the 274-line baseline report, and updates to the
research index, the dated change log, the rolling change log, and project
memory. No skill package, schema, validator, or ADR changed.

---

## Recorded state of the project at publication

- Phase 1: 8 of 8. Phase 2: 6 of 9. Phase 3: 0 of 7. Phase 4: 0 of 6 `[R-D009-08]`.
- The Phase 2 evidence item "Remediate the verified prototype vulnerabilities in
  its owning repository" remains **unchecked**, annotated "remediation is
  intentionally outside this skills-repository review batch" `[R-D009-08]`.
- Six risk records remain `status: open` `[R-D009-09]`.
