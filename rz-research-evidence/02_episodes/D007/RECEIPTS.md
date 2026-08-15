# D007 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D007-01 | Decision moment bound; author | S1 `6cb5ef0fd59367d41cc689cd0310cd87d2357748`, `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 22:07:24 −0400 | VERIFIED-HERE |
| R-D007-02 | API Security Review was a roadmap item from vault initialization | S1 `09-Roadmap/Roadmap.md` @ `b8638a1` (19:20:25), "Phase 2 — Engineering", sixth entry, unchecked | VERIFIED-HERE |
| R-D007-03 | ADR-004 content: context, decision, four consequences, validation basis | S1 `04-Decisions/ADR-004-API-Review-Requires-Observed-Surface.md` @ `6cb5ef0` — whole file, created in this commit; frontmatter `status: accepted`, `decision_date: 2026-07-20` | VERIFIED-HERE (as the project's own record) |
| R-D007-04 | The reconciliation completed 34 minutes earlier | S1 `05-Research/2026-07-20-Rust-Prototype-Reconciliation.md` @ `df3cace`, authored 2026-07-20 21:33:10 −0400 | VERIFIED-HERE |
| R-D007-05 | The precondition this episode acts on | Same file, "## RankZero Implications", item 6: "Keep API Security Review and new feature work out of scope until this reconciliation commit is accepted" | VERIFIED-HERE |
| R-D007-06 | The observed route surface, independently re-verified | S2 @ `13e79c8`: `grep -rn 'route(\|fallback(' v4-single-binary/src/` → `gateway.rs:204–211` (8 routes), `telemetry.rs:20`, `proxy.rs:97` (wildcard), `proxy.rs:98`, `web.rs:17` (fallback). Direct count: 10 named + 1 wildcard + 1 fallback | VERIFIED-HERE |
| R-D007-07 | ADR-004 is structurally unlike the first three ADRs | S1 `04-Decisions/`: ADR-001, ADR-002, ADR-003 each contain an "## Alternatives Considered" section with three entries and `related_risks: []`. ADR-004 contains no such section and lists three risks | VERIFIED-HERE |
| R-D007-08 | Deployment-surface contradiction was known before the decision | S1 `05-Research/2026-07-20-Rust-Prototype-Reconciliation.md` @ `df3cace`, "Unknowns" and the later review's "Architectural Limitations": "Rust, Docker/Compose, DaemonSet, and installer assets disagree about executable surface and port … Which surface is deployed was not observed" | VERIFIED-HERE (as the project's own record) |
| R-D007-09 | ADR-004 links three risks | S1 ADR-004 frontmatter: `related_risks: [RISK-001, RISK-002, RISK-003]` | VERIFIED-HERE |
| R-D007-10 | Six risk records and the gaps taxonomy are created in this commit | S1 `git show --name-status 6cb5ef0` → `A 07-Risks/RISK-001…` through `RISK-006…`, `A 07-Risks/Known Gaps.md`, `M 07-Risks/Risk Register.md` | VERIFIED-HERE |
| R-D007-11 | Validator extended to cover real-code output | S1 `scripts/validate_phase2_skills.py`: 345 lines @ `54976fd` → 426 lines @ `6cb5ef0`; gains `def validate_evaluation_outputs(evaluation_dir)` at line 341 and adds `"rankzero-api-security-review"` to `PHASE2_SKILLS` | VERIFIED-HERE |
| R-D007-12 | Commit scope: 41 paths | S1 `git show --name-status 6cb5ef0 \| wc -l` → 41. Includes 6 API-skill files, 8 evaluation JSON files, 2 ADRs, 7 risk files, 1 research note, 1 change note, 1 skill note, and modifications to the orchestrator, 7 skill notes, registry, architecture, roadmap, change log, memory, and validator | VERIFIED-HERE |
| R-D007-13 | Tracked file count and orchestrator version at the boundary | S1 `git ls-tree -r --name-only 6cb5ef0 \| wc -l` → 118; orchestrator SKILL.md frontmatter `version: "0.4.0"` | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| A recorded run of `scripts/validate_phase2_skills.py` on the real-code outputs | The ADR and change note assert it passes; no output, log, or CI record exists — VAULT-ASSERTED |
| The reasoning that produced the finding content in the eight evaluation JSON files | The specialists are prompts executed by an agent; no transcript exists at any commit |
| A separate "acceptance" artifact for the reconciliation commit | None. Acceptance is evidenced only by this commit proceeding |
| Why ADR-004 omits an "Alternatives Considered" section | Not recorded |
| Which deployment surface was actually active | Explicitly not observed; recorded as an architectural limitation |
