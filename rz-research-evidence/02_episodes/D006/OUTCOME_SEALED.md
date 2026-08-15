# D006 — OUTCOME_SEALED

Everything below became visible **after** the decision to reconcile. It includes
the reconciliation's own results, which are outcomes of this episode, and
discoveries made in this 2026-08-15 reconstruction.

---

## Results of the reconciliation, as recorded in the same commit

### The headline result was inverted

The prototype's own record said "34/34 tests passing." The reconciliation's
executive result:

> That headline is materially misleading as a security result: token revocation
> is broken, and Test 04 passes because an allowed request receives an upstream
> HTTP 401.

The recorded runtime evidence: after the revoke call, SQLite logged `REVOKE`
followed by `PROXY_ALLOWED` for `revoke-test-agent`; the test accepted the
upstream service's 401 as if it were a gateway rejection.

**Test 04 was the one test the prototype's prior self-audit had classified
TRACEABLE and left unflagged.** The 20-hour-old static audit did not catch it;
runtime execution did.

### The mechanism, re-verified in this reconstruction at source level

The revocation identifier mismatch is confirmed directly in S2 at `13e79c8`:

| Side | Code | Key written or queried |
|---|---|---|
| Write — `gateway.rs` `revoke_agent_token` | `INSERT OR IGNORE INTO revoked_tokens (jti, …) VALUES (?1, …)` with `format!("agent:{}", agent_id)` | `agent:<agent_id>` |
| Read — `auth.rs:129–142` | `Sha256::new()` over the token, then `SELECT 1 FROM revoked_tokens WHERE jti = ?1` | base64url(sha256(jwt)) |

The gateway source carries an in-line acknowledgment at the write site: *"We use
agent_id as jti here for simplicity (real impl would pass the token ID)."* The
two key formats can never match. CONFIRMED at source level, independent of the
vault's runtime claim.

### Other recorded results

| Claim under reconciliation | Recorded disposition |
|---|---|
| Rust-native test count | 0 — `cargo test --locked` reported "running 0 tests" |
| Clean build from tracked files | fails — `soc-dashboard/dist` absent; built only after assets were copied from a working copy |
| Property-based redaction test | not found; only example-based Tests 20 and 21 |
| Mutation harness | not found; `NEXT_TASK.md` says not to run mutation testing |
| `GAP-020`, `GAP-021` | not found in any searched location |
| `ea65dd2`, `5f92e35` | not found; direct remote fetch by SHA failed |
| `rz-launcher` | design-only; no crate, binary target, or source |
| `13e79c8` "is missing" | **contradicted** — it is the current advertised tip |
| Local debug binary | exists, arm64, mtime 2026-07-17 — older than the tip, so not provenance proof |

### Re-verified in this reconstruction

Independently confirmed against S2 on 2026-08-15, without relying on the vault:

| Finding | Check | Result |
|---|---|---|
| `soc-dashboard/dist` untracked | `git ls-files \| grep -c soc-dashboard/dist` | 0 |
| `GAP-020` / `GAP-021` absent | case-insensitive tree search | 0 hits each |
| Property-based testing absent | search for `proptest`, `property-based` | 0 hits |
| Mutation testing barred | `docs/vault/NEXT_TASK.md` line 9 | "Do not run mutation testing." |
| `ea65dd2`, `5f92e35` absent | tree search + `git cat-file -t` | not found |
| 34 Python test methods | `grep -c '    def test_'` | 34 |

The absence findings hold in the public repository 26 days later.

## The scope prohibitions held for exactly 34 minutes

The decision withheld API Security Review "until this reconciliation commit is
accepted." The next commit, `6cb5ef0` at 22:07:24, added
`rankzero-api-security-review` version 0.1.0. The condition was met by the
reconciliation being committed — no separate acceptance artifact exists, so
acceptance is evidenced only by the subsequent commit proceeding.

Two other prohibitions held longer:

- **No product code was modified.** Neither S1 nor S2 shows a source change in this episode, and the change note records "The external prototype working tree was not modified."
- **Remediation stayed out of the skills repository.** The roadmap item "Remediate the verified prototype vulnerabilities in its owning repository; remediation is intentionally outside this skills-repository review batch" remains **unchecked** at S1 HEAD.

## The forward test ADR-002 waited for became this

The "representative target" turned out to be the project's own prototype rather
than a synthetic fixture. Every one of the six pipeline stages produced a
findings section in this note, and at `6cb5ef0` those became eight
schema-validated JSON outputs.

## Later discovery — 2026-08-15

The evidence anchors named in this episode still resolve as recorded:

```
$ git ls-remote https://github.com/jayhaving/agentic-iam-gateway
38ca81f431dd20056def093dc5f6f0a9a1ee8199   HEAD
38ca81f431dd20056def093dc5f6f0a9a1ee8199   refs/heads/main
13e79c8b2e607e07cfc0629f89cb8654edc5383e   refs/heads/v4-session13
```

`v4-session13` is unchanged at `13e79c8`. Every defect this episode identified is
still present in the public tree: `/mint` at `gateway.rs:204` still has no
`verify_admin_key` call in its handler body, the revocation key mismatch is
intact, and `llm.rs:99→138` still writes quarantine state from a substring match.

The prototype's `docs/vault/status.json` still reports `total_tests_passing: 34`
and `last_verified: 2026-07-17`, and `10-Test-Quality-Audit.md` still classifies
Test 04 as TRACEABLE. **The corrections this episode produced were recorded in
the vault repository and never propagated back into the prototype's own
records.**

## Not an evaluation

This file records outcomes and later observations. It takes no position on
whether reconciling first was the right call, and it does not assess the
prototype's engineering.
