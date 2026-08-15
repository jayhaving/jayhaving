# D001 — RECEIPTS

Source identifiers (S1, S2, S4) are defined in `00_method/EVIDENCE_SOURCES.md`.

| ID | Claim supported | Locator | Status |
|---|---|---|---|
| R-D001-01 | Decision moment bound; author identity | S1 commit `b8638a18ab2f152b83d31667d123ffc62be0dedb` → `git log b8638a1 --format='%H %an %ae %ad'` → `jayhaving <jasonawuah@icloud.com>`, `2026-07-20 19:20:25 -0400`. Root commit — no parent | VERIFIED-HERE |
| R-D001-02 | A vault practice existed in the product repo before this episode | S2 `git ls-tree -r --name-only 13e79c8 -- docs/vault/` → 15 paths: `00-Architecture-Overview.md` … `10-Test-Quality-Audit.md`, `NEXT_TASK.md`, `README.md`, `status.json`. Commit `13e79c8` authored `2026-07-20 01:39:22 -0400` | VERIFIED-HERE |
| R-D001-03 | Prior vault self-description and non-accumulating handoff | S2 `docs/vault/README.md` @ `13e79c8`, lines 1–13: "This file is a MAP, not content"; "Total vault: 13 documents + status.json … ~3500 lines"; NEXT_TASK "is overwritten, never appended, when a new task is assigned" | VERIFIED-HERE |
| R-D001-04 | Prior decision-log and evidence-rule practice | S2 @ `13e79c8`: `docs/vault/01-Decision-Log.md` headings `DEC-001` … `DEC-013` dated 2026-07-16/17; `docs/vault/04-Known-Gaps-and-Honesty-Log.md` contains `GAP-001` … `GAP-016` and no higher identifier; `docs/vault/status.json` `_meta.rule` quoted in full | VERIFIED-HERE |
| R-D001-05 | Vision, north star, engines, quality standard | S1 `01-Vision/Vision and North Star.md` @ `b8638a1`, whole file (created in this commit) | VERIFIED-HERE |
| R-D001-06 | Seven foundation skills recorded as existing | S1 `12-Memory/Project Memory.md` @ `b8638a1`, "Current Skill Set"; S1 `03-Skills/` @ `b8638a1` contains 8 skill notes | VERIFIED-HERE |
| R-D001-07 | Roadmap state at decision moment | S1 `09-Roadmap/Roadmap.md` @ `b8638a1`: Phase 1 eight items `[x]`; Phase 2 nine items `[ ]` | VERIFIED-HERE |
| R-D001-08 | Change-log wording of the decision | S1 `11-Change-Log/Change Log.md` @ `b8638a1`, Decisions section: "Preserve durable memory in a Git-versioned Obsidian vault"; "Treat skills as versioned software assets, not static prompts" | VERIFIED-HERE |
| R-D001-09 | Three-layer memory model and setup sequence | S1 `README.md` @ `b8638a1`, "Memory model" and "Recommended setup" sections; step 5 directs adding `kepano/obsidian-skills` separately | VERIFIED-HERE |
| R-D001-10 | 33-file scope; empty decision log and risk register; no Known Gaps file | S1 `git show --name-status b8638a1` → 33 additions. `04-Decisions/Decision Log.md` and `07-Risks/Risk Register.md` at that commit contain frontmatter plus one embed each. `07-Risks/Known Gaps.md` absent from the commit's file list | VERIFIED-HERE |
| R-D001-11 | The eight memory rules | S1 `12-Memory/Project Memory.md` @ `b8638a1`, "Memory Rules" section, quoted verbatim | VERIFIED-HERE |
| R-D001-12 | Third-party skills pinned by hash | S1 commit `39283a6` @ `2026-07-20 19:24:14 -0400` adds 9 skill files plus `skills-lock.json`; lockfile records `source: kepano/obsidian-skills`, `sourceType: github`, and a `computedHash` for each of four skills | VERIFIED-HERE |
| R-D001-13 | No second participant evidenced | S1 `git log --format='%an %ae %cn %ce'` — author equals committer on all 8 commits; no `Co-Authored-By` trailer in any message; S1 and S2 contain no PR or issue artifacts | VERIFIED-HERE (absence within corpus) |
| R-D001-14 | Architecture note created as draft | S1 `02-Architecture/Current Architecture.md` @ `b8638a1`, frontmatter `status: draft` | VERIFIED-HERE |

## Receipts NOT available for this episode

| Wanted | Why unavailable |
|---|---|
| Any record of alternatives considered for the memory substrate | No ADR, note, or message addresses it. The corpus is silent |
| Location of the seven foundation skill packages at 19:20:25 | Vault notes describe them; packages enter the repo only at D002. Source location is a local path (S4) |
| Motivation for separating the vault from the product repository | Not stated in any reachable artifact |
| Anything dated between 2026-07-20 01:39 and 19:20 | No commit exists in either repository in that window |
