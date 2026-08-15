# D003 — RECEIPTS

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D003-01 | Decision moment bound; author | S1 `b2fa3976e29534303df5bcc5750a3c2bdac90a6b`, author `Jason Awuah <YOUR_GITHUB_EMAIL>`, authored 2026-07-20 20:42:10 −0400 (committed 20:42:41 — the only commit in S1 with a nonzero author/commit gap) | VERIFIED-HERE |
| R-D003-02 | No ADR, risk, or research record existed before this commit | S1 `git ls-tree -r --name-only 17a50b7 -- 04-Decisions/ 07-Risks/ 05-Research/` → three index/register stubs only, no `ADR-*`, no `RISK-*`, no dated research note | VERIFIED-HERE |
| R-D003-03 | Architecture Discovery was already first on the Phase 2 roadmap | S1 `09-Roadmap/Roadmap.md` @ `b8638a1` (2026-07-20 19:20:25), "Phase 2 — Engineering": nine unchecked items, `Architecture Discovery` first | VERIFIED-HERE |
| R-D003-04 | ADR-001 content: context, decision, three alternatives, security impact, three consequences, validation, follow-up | S1 `04-Decisions/ADR-001-Architecture-Discovery-Precedes-Threat-Modeling.md` @ `b2fa397` — whole file, created in this commit; frontmatter `status: accepted`, `decision_date: 2026-07-20`, `owner: RankZero`, `related_risks: []` | VERIFIED-HERE (as the project's own record) |
| R-D003-05 | Threat-model generator installed 9 minutes earlier at 0.1.0 | S1 `.agents/skills/rankzero-threat-model-generator/SKILL.md` added at `17a50b7` (20:33:36); frontmatter version `0.1.0` | VERIFIED-HERE |
| R-D003-06 | No independent evidence for the stated motivation | S1 at `b2fa397` contains no research note, incident record, prior review, or external-system reference. `05-Research/` holds only `Research Index.md`. The three named failure modes are asserted in ADR prose only | VERIFIED-HERE (absence within corpus) |
| R-D003-07 | No external target system referenced yet | S1 at `b2fa397`: no occurrence of `agentic-iam-gateway`, `13e79c8`, or any gateway commit hash (`git grep -il 'agentic-iam\|13e79c8' b2fa397` → empty) | VERIFIED-HERE |
| R-D003-08 | The skill's seven operating rules as shipped | S1 `.agents/skills/rankzero-architecture-discovery/SKILL.md` @ `b2fa397`, "## Operating Rules", quoted verbatim | VERIFIED-HERE |
| R-D003-09 | The planned validation fixture did not exist | S1 `git ls-tree -r --name-only b2fa397` → no fixture, no `examples/`, no `tests/`, no `schemas/` anywhere in the tree; the new package contains `SKILL.md` and `agents/openai.yaml` only | VERIFIED-HERE (absence within corpus) |
| R-D003-10 | Recorded tests are named but not scripted | S1 `11-Change-Log/2026-07-20-Architecture-Discovery.md` @ `b2fa397`, "## Tests": three bullets. S1 `scripts/` does not exist at this commit (`git ls-tree -r --name-only b2fa397 -- scripts/` → empty) | VERIFIED-HERE for the absence; VAULT-ASSERTED for the tests having been run |
| R-D003-11 | Commit scope | S1 `git show --name-status b2fa397` → 12 paths: 4 additions (`rankzero-architecture-discovery/SKILL.md`, `agents/openai.yaml`, `03-Skills/rankzero-architecture-discovery.md`, `ADR-001…md`, `11-Change-Log/2026-07-20-Architecture-Discovery.md`) and modifications to orchestrator SKILL.md, `00-Home`, `02-Architecture`, `03-Skills/rankzero-security-orchestrator.md`, `09-Roadmap`, `11-Change-Log/Change Log.md`, `12-Memory` | VERIFIED-HERE |
| R-D003-12 | Orchestrator version bump and diff size | S1 `git diff 17a50b7 b2fa397 -- .agents/skills/rankzero-security-orchestrator/SKILL.md --stat` → 15 insertions, 1 deletion; frontmatter `version` `"0.1.0"` → `"0.2.0"` | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| Evidence that the threat-model skill's architecture inventory was insufficient | Asserted in ADR Context; no comparison, output, or trial exists |
| Any instance of the three named failure modes | No incident or artifact in the corpus |
| The tool that performed "YAML and JSON syntax checks" and "placeholder checks" | Not in the repository; no script, config, or log |
| The validation fixture described in the ADR | Never created — absent at every commit in S1 |
| Whether the ordering was debated | No discussion artifact of any kind exists |
