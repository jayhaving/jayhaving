# D002 — RECEIPTS

Source identifiers (S1, S4) are defined in `00_method/EVIDENCE_SOURCES.md`.

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D002-01 | The three installation rules were recorded at vault init, before any package existed | S1 `11-Change-Log/Change Log.md` @ `b8638a18ab2f152b83d31667d123ffc62be0dedb` (2026-07-20 19:20:25 −0400), "Decisions" section — contains "Upload specialist skills individually", "Upload the security orchestrator last", "Treat skills as versioned software assets, not static prompts". Verified by `git show b8638a1:'11-Change-Log/Change Log.md'` | VERIFIED-HERE |
| R-D002-02 | Execution scope and timestamp; no prose accompanied it | S1 `git show --name-status 17a50b7d7babbe6de10fdc0353fbfa5e510adf00` → exactly 14 additions, all under `.agents/skills/rankzero-*/`, 7 × (`README.md`, `SKILL.md`). No `M` entries. Authored 2026-07-20 20:33:36 −0400 | VERIFIED-HERE |
| R-D002-03 | No specialist package existed at 19:20:25 | S1 `git ls-tree -r --name-only b8638a1 -- .agents/skills/` → only `rankzero-project-memory/SKILL.md` and its `references/vault-conventions.md` | VERIFIED-HERE |
| R-D002-04 | Seven foundation skills declared complete | S1 `09-Roadmap/Roadmap.md` @ `b8638a1`, "Phase 1 — Foundation", 8 items `[x]` | VERIFIED-HERE |
| R-D002-05 | Packages sourced from a local `~/Downloads` path | S1 `12-Memory/Project Memory.md` @ `b2fa397`, "Skill Installation Audit": "All seven specialist packages found in `~/Downloads`" | VAULT-ASSERTED — the path is S4, unreachable |
| R-D002-06 | Orchestrator's declared routing role | S1 `.agents/skills/rankzero-security-orchestrator/SKILL.md` @ `17a50b7`, description field and "## Purpose": "entry point"; "should route work rather than duplicate specialist instructions" | VERIFIED-HERE |
| R-D002-07 | Orchestrator installed at 0.1.0 | S1 same file @ `17a50b7`, frontmatter `metadata.version: "0.1.0"`, `license: Apache-2.0` | VERIFIED-HERE |
| R-D002-08 | Installation audit text, including the unmodified claim and the CyberForge decline | S1 `12-Memory/Project Memory.md` @ `b2fa3976e29534303df5bcc5750a3c2bdac90a6b` (2026-07-20 20:42:10 −0400), "## Skill Installation Audit", four bullets quoted verbatim in PRE_DECISION. **First appearance:** absent at `b8638a1`, present from `b2fa397` onward (`git show <c>:'12-Memory/Project Memory.md' \| grep -c 'Skill Installation Audit'` → 0 at `b8638a1`, 1 at `b2fa397` and later) | VAULT-ASSERTED for the byte-comparison and the CyberForge file's properties; VERIFIED-HERE for the text's existence and first-appearance commit |
| R-D002-09 | Skill Registry was still an embed-only stub at execution | S1 `03-Skills/Skill Registry.md` @ `17a50b7` — frontmatter plus `![[Skills.base]]`, no per-skill entries | VERIFIED-HERE |
| R-D002-10 | CyberForge decline also recorded as a rejected ADR alternative | S1 `04-Decisions/ADR-001-Architecture-Discovery-Precedes-Threat-Modeling.md` @ `b2fa397`, "## Alternatives Considered", second bullet | VERIFIED-HERE |
| R-D002-11 | The CyberForge file cannot be examined | Not present in S1 at any commit (`git log --all --diff-filter=A -- '*cyberforge*'` → empty); referenced only by local path. Identity of "CyberForge" not established anywhere in S1 or S2 | UNAVAILABLE |
| R-D002-12 | No validation tooling existed at this episode | S1 `git ls-tree -r --name-only 17a50b7 -- scripts/` → empty; no `*.schema.json` and no fixture files anywhere in the tree at `17a50b7` or `b2fa397` | VERIFIED-HERE (absence within corpus) |
| R-D002-13 | Installed packages carry documentation only | S1 `git ls-tree -r --name-only 17a50b7 -- .agents/skills/` → 14 paths, all `SKILL.md` or `README.md` | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| Contents of the seven `~/Downloads` packages as downloaded | Local path, S4. The vault's byte-for-byte claim cannot be independently checked |
| The `cyberforge-security-review` file | Never entered any reachable repository |
| Origin of the seven specialist packages — who produced them, from where | No source URL, lockfile entry, or provenance record. `skills-lock.json` covers only the four `kepano/obsidian-skills` packages, never the RankZero ones |
| Rationale for "individually" and "orchestrator last" | Recorded as bare imperatives with no accompanying reasoning |
| Timestamp of the CyberForge evaluation itself | Only the record at 20:42:10 is datable |
| Any output of the "audit" | No diff, checksum list, or comparison log exists |
