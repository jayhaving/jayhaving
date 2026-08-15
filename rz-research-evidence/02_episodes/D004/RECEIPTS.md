# D004 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D004-01 | Decision moment bound; author | S1 `54976fd2cc62c218652a7390b52f7d67fefb06c2`, `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 21:03:10 −0400 | VERIFIED-HERE |
| R-D004-02 | Only one ordered pair existed before this commit | S1 `04-Decisions/` @ `b2fa397` contains `ADR-001` only; `02-Architecture/Current Architecture.md` @ `b2fa397` "Security Review Workflow" section | VERIFIED-HERE |
| R-D004-03 | Phase 2 at 1 of 9 | S1 `09-Roadmap/Roadmap.md` @ `b2fa397`: `Architecture Discovery` `[x]`, eight items `[ ]` | VERIFIED-HERE |
| R-D004-04 | No schema, fixture, or script existed before this commit | S1 `git ls-tree -r --name-only b2fa397` → zero paths matching `schema.json`; `scripts/` absent | VERIFIED-HERE (absence within corpus) |
| R-D004-05 | ADR-002 content: context, decision, pipeline diagram, three alternatives, security impact, four consequences, validation, two follow-ups | S1 `04-Decisions/ADR-002-Phase-2-Evidence-Pipeline.md` @ `54976fd` — whole file, created in this commit; frontmatter `status: accepted`, `decision_date: 2026-07-20`, `related_risks: []` | VERIFIED-HERE (as the project's own record) |
| R-D004-06 | No artifact demonstrates the three anticipated failure modes | S1 at `54976fd`: `05-Research/` holds only `Research Index.md`; `07-Risks/` holds only the register stub; no evaluation output exists | VERIFIED-HERE (absence within corpus) |
| R-D004-07 | The four ordered specialists are introduced by this same commit; nothing had run through the pipeline | S1 `git show --name-status 54976fd` → `A` entries for all four `.agents/skills/rankzero-{asset-discovery,attack-surface-mapper,authentication-review,authorization-review}/` packages. `05-Research/evaluations/` does not exist at this commit | VERIFIED-HERE |
| R-D004-08 | No external target referenced | S1 `git grep -il 'agentic-iam\|13e79c8\|gateway' 54976fd` → no match outside generic architecture prose; `05-Research/evaluations/` absent | VERIFIED-HERE |
| R-D004-09 | Four schemas, four valid fixtures, four invalid fixtures added | S1 @ `54976fd`: `schemas/output.schema.json`, `examples/valid-output.json`, `tests/invalid-output.json` under each of the four new packages — 12 files plus 4 `SKILL.md` and 4 `agents/openai.yaml` | VERIFIED-HERE |
| R-D004-10 | Validator is dependency-free and 345 lines at this commit | S1 `scripts/validate_phase2_skills.py` @ `54976fd` → imports `json`, `re`, `sys`, `pathlib`, `typing` only; `git show 54976fd:scripts/validate_phase2_skills.py \| wc -l` → 345. (It grows to 426 at `6cb5ef0`; see D007) | VERIFIED-HERE |
| R-D004-11 | Cross-reference checking is implemented, not merely promised | S1 `scripts/validate_phase2_skills.py` @ `54976fd`: `def validate_cross_references(skill_name, instance)` at line 284; `def unique_ids(items, path)` at line 263; `def validate_confidence_values` at line 270 | VERIFIED-HERE |
| R-D004-12 | Identifier ownership recorded per stage | S1 `02-Architecture/Current Architecture.md` @ `54976fd`, "Phase 2 Evidence Contracts" section | VERIFIED-HERE |
| R-D004-13 | Commit scope: 35 paths | S1 `git show --name-status 54976fd` → 20 additions under `.agents/skills/`, 4 skill notes, 2 ADRs, 1 change note, 1 script, 7 modifications | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| Any recorded run of the validator at this commit | No output, log, or CI record. The change note lists `python3 scripts/validate_phase2_skills.py` under "Tests" — VAULT-ASSERTED |
| Evidence that independent specialists would in fact diverge | Stated prospectively; no trial |
| The "representative target" the follow-up waits for | Not identified at this commit |
| Reason the four specialists were batched rather than added one at a time | Not recorded; note that it departs from D002's "upload specialist skills individually" rule without comment |
