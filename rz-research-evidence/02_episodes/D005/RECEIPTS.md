# D005 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D005-01 | Decision moment bound; author | S1 `54976fd2cc62c218652a7390b52f7d67fefb06c2`, `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 21:03:10 −0400 | VERIFIED-HERE |
| R-D005-02 | The product-level split predates this decision | S1 `12-Memory/Project Memory.md` @ `b8638a1` (19:20:25), "Core Product Ideas": "Deterministic enforcement in the critical path", "LLM analysis in the intelligence path" | VERIFIED-HERE |
| R-D005-03 | No prior rule governed authority among the review skills' own outputs | S1 `04-Decisions/` @ `b2fa397` contains ADR-001 only, which concerns stage ordering; no other decision record exists | VERIFIED-HERE (absence within corpus) |
| R-D005-04 | ADR-003 content: context, two authority lists, four prohibitions, three alternatives, four consequences, validation basis, two follow-ups | S1 `04-Decisions/ADR-003-Deterministic-Checks-Are-Authoritative.md` @ `54976fd` — whole file, created in this commit; frontmatter `status: accepted`, `decision_date: 2026-07-20`, tag `deterministic-enforcement` | VERIFIED-HERE (as the project's own record) |
| R-D005-05 | No cited study, measurement, or trial supports the reliability premise | S1 `05-Research/` @ `54976fd` contains only `Research Index.md`; ADR-003 cites no source; no benchmark or experiment artifact exists at any S1 commit | VERIFIED-HERE (absence within corpus) |
| R-D005-06 | No system had been reviewed at the decision moment | S1 @ `54976fd`: `05-Research/evaluations/` does not exist; `07-Risks/` contains only the register stub; no external repository or commit hash is referenced | VERIFIED-HERE |
| R-D005-07 | The validator exists in the same commit as the decision | S1 `git show --name-status 54976fd` → `A scripts/validate_phase2_skills.py`. Function line numbers at this commit: `validate_instance` 190, `detect_literal_secrets` 242, `unique_ids` 263, `validate_confidence_values` 270, `validate_cross_references` 284 | VERIFIED-HERE |
| R-D005-08 | Validator coverage is four skills; two pipeline stages are outside it | S1 `git show 54976fd:scripts/validate_phase2_skills.py` lines 19–24 → `PHASE2_SKILLS` tuple of four; `EXPECTED_VERSION = "0.1.0"`. Neither `rankzero-architecture-discovery` nor `rankzero-threat-model-generator` appears in the file | VERIFIED-HERE |
| R-D005-09 | No policy engine, graph implementation, or regression suite existed in the repository | S1 `git ls-tree -r --name-only 54976fd` → one Python file (`scripts/validate_phase2_skills.py`), no `.rego`, no test directory outside skill fixture folders, no runtime code of any kind | VERIFIED-HERE (absence within corpus) |
| R-D005-10 | Secret-screen key list, as implemented | S1 `scripts/validate_phase2_skills.py` @ `54976fd`, `detect_literal_secrets`: `sensitive_keys = {"token", "secret", "password", "api_key", "private_key", "cookie", "credential_value"}` plus regex `secret_patterns` | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| Evidence for the premise that LLMs are unreliable schema validators | Asserted; no citation, benchmark, or trial in the corpus |
| A recorded run of the validator at this commit | The change note lists `python3 scripts/validate_phase2_skills.py` under "Tests"; no output or log exists — VAULT-ASSERTED |
| Any case where a model output conflicted with a deterministic result, before this decision | None exists. The boundary is set prospectively |
| Whether the ADR's authority list was drawn from a source | No source is cited |
