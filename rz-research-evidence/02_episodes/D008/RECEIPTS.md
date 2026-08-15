# D008 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D008-01 | Decision moment bound; author | S1 `6cb5ef0fd59367d41cc689cd0310cd87d2357748`, `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 22:07:24 −0400 | VERIFIED-HERE |
| R-D008-02 | The review-system principle predates this product rule by 64 minutes | S1 `04-Decisions/ADR-003-Deterministic-Checks-Are-Authoritative.md` @ `54976fd` (21:03:10), "## Decision", four prohibitions including "override a deny decision" | VERIFIED-HERE |
| R-D008-03 | The product-level split predates both | S1 `12-Memory/Project Memory.md` @ `b8638a1`, "Core Product Ideas" | VERIFIED-HERE |
| R-D008-04 | No prior rule governed model-to-enforcement writes in the product | S1 `04-Decisions/` @ `df3cace` contains ADR-001 … ADR-003 only; none names quarantine, revocation, or enforcement mutation | VERIFIED-HERE (absence within corpus) |
| R-D008-05 | ADR-005 content: context, decision, seven state categories, three consequences, validation obligation | S1 `04-Decisions/ADR-005-LLM-Output-Cannot-Mutate-Enforcement.md` @ `6cb5ef0` — whole file, created in this commit; frontmatter `status: accepted`, `related_risks: [RISK-004]`, tag `deterministic-enforcement` | VERIFIED-HERE (as the project's own record) |
| R-D008-06 | The code path, independently confirmed at source level | S2 `v4-single-binary/src/llm.rs` @ `13e79c8b2e607e07cfc0629f89cb8654edc5383e`: line 91 `let mut is_malicious = false;`; line 97 reads `json_resp["candidates"][0]["content"]["parts"][0]["text"].as_str()`; line 99 `if text.contains("DECISION: MALICIOUS")`; line 100 `is_malicious = true;`; line 126 comment "3. Auto-Quarantine if malicious"; line 127 `if is_malicious {`; line 128 `tracing::warn!("Auto-Quarantining Agent {} based on LLM analysis!", agent_id);`; line 138 `INSERT OR IGNORE INTO quarantine (agent_id, timestamp) VALUES (?1, ?2)`. All within one async block | VERIFIED-HERE — CONFIRMED |
| R-D008-07 | Prior characterization of the LLM stage | S2 `docs/CONTEXT_BUNDLE.md` @ `13e79c8` describes LLM triage and behavioral detection; `docs/vault/status.json` lists the triage capability. S1 `12-Memory/Project Memory.md` @ `b8638a1` lists "LLM analysis in the intelligence path" | VERIFIED-HERE |
| R-D008-08 | The labeling correction was recorded alongside the decision | S1 `05-Research/2026-07-20-Rust-Gateway-Security-Review.md` @ `6cb5ef0`, "## False or Stale Claims": "Regex/subsequence behavior matching is not ML or AI-powered detection" | VERIFIED-HERE |
| R-D008-09 | RZ-005 and RZ-004 as recorded | S1 same review note, "## Verified Vulnerabilities": RZ-005 (high, 0.98) and RZ-004 (high, 0.99) | VERIFIED-HERE (as the project's own record); RZ-005's mechanism additionally CONFIRMED at source via R-D008-06 |
| R-D008-10 | No test proving the required property existed | S1 `git ls-tree -r --name-only 6cb5ef0` → the only Python file is `scripts/validate_phase2_skills.py`, which validates JSON documents, not runtime behavior. S2 @ `13e79c8`: `cargo test` target count zero; `v4-single-binary/Cargo.toml` declares no `[[test]]` section and no `[dev-dependencies]` | VERIFIED-HERE (absence within corpus) |
| R-D008-11 | Risk record opened in the same commit | S1 `07-Risks/RISK-004-LLM-Controlled-Enforcement.md` @ `6cb5ef0`: `risk_id: RISK-004`, `severity: high`, `status: open`, created 2026-07-20 | VERIFIED-HERE |
| R-D008-12 | No prototype source was changed | S1 `git show --name-status 6cb5ef0` contains no path outside the vault. S2 has no commit dated 2026-07-20 after 01:39:22 on any advertised ref | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| A record stating that auto-quarantine-from-LLM was an intended feature | The affirmative source comment and log message are the only evidence; intent is INFERENCE |
| Any test exercising the model-to-enforcement path before this decision | None exists in either repository |
| Whether the path was reachable in a deployed configuration | Deployment activation was explicitly not observed (RISK-005) |
| The model service's behavior | The path calls an external Gemini endpoint; no recorded interaction exists |
