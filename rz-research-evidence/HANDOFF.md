# HANDOFF — RankZero historical reconstruction

Prepared 2026-08-15 for an independent Codex auditor.

This file is **metadata only**. It adds no historical claim and modifies no
reconstruction content. The 43 reconstruction files are unchanged from the
commit that introduced them.

---

## 1. Absolute local repository path

```
/home/user/jayhaving
```

> **This path is not reachable by the auditor.** It is inside an ephemeral
> cloud container that is reclaimed after the session ends. It is recorded for
> completeness only. **Use the remote in §9 as the source of truth.**

## 2. Git remote URL

```
origin  https://github.com/jayhaving/jayhaving  (fetch)
origin  https://github.com/jayhaving/jayhaving  (push)
```

Note the repository name: the reconstruction lives in the **profile repository**
`jayhaving/jayhaving`, **not** in `jayhaving/rankzero-security-os`. This is the
reason an earlier audit attempt reported MISSING — it searched the RankZero
repository, where these files have never existed.

## 3. Current branch

```
claude/research-evidence-docs-xcvi41
```

Tracking `origin/claude/research-evidence-docs-xcvi41`.

## 4. Exact commit SHA containing `rz-research-evidence/`

```
49fd3f123c41899d4c9a127d8a513601f1e78b84
```

Short form `49fd3f1`. This is both the current `HEAD` and the commit that first
added the directory (`git log --diff-filter=A -- rz-research-evidence/`), so the
directory has exactly one commit of history and has not been amended.

Tree object for the directory at that commit:

```
5f8ff2ef07be9d16568db2cf0390f83bfb87c67f
```

Working tree is clean — `git status --porcelain` returns empty as of this
handoff, before `HANDOFF.md` itself was added.

## 5. Exact path to `rz-research-evidence/`

| Context | Path |
|---|---|
| Repository-relative | `rz-research-evidence/` |
| Absolute, in the origin container | `/home/user/jayhaving/rz-research-evidence/` |
| Episode root, repository-relative | `rz-research-evidence/02_episodes/` |

After the auditor clones per §9, the episode root becomes
`<clone>/rz-research-evidence/02_episodes/`.

## 6. D001–D009 existence — CONFIRMED

All nine episode directories exist, each containing exactly four files.

| Episode | Files | `PRE_DECISION` | `RECEIPTS` | `OUTCOME_SEALED` | `TECHNICAL_STATE` |
|---|---|---|---|---|---|
| D001 | 4 | ✔ | ✔ | ✔ | ✔ |
| D002 | 4 | ✔ | ✔ | ✔ | ✔ |
| D003 | 4 | ✔ | ✔ | ✔ | ✔ |
| D004 | 4 | ✔ | ✔ | ✔ | ✔ |
| D005 | 4 | ✔ | ✔ | ✔ | ✔ |
| D006 | 4 | ✔ | ✔ | ✔ | ✔ |
| D007 | 4 | ✔ | ✔ | ✔ | ✔ |
| D008 | 4 | ✔ | ✔ | ✔ | ✔ |
| D009 | 4 | ✔ | ✔ | ✔ | ✔ |

No `D010` or higher exists. No episode directory is partial.

## 7. File count inside `rz-research-evidence/`

| Scope | Count |
|---|---|
| At commit `49fd3f1` (the reconstruction as delivered) | **43** |
| Episode files (9 × 4) | 36 |
| Method files (`00_method/`) | 3 |
| Timeline (`01_timeline/`) | 1 |
| Index (`03_index/`) | 2 |
| Root `README.md` | 1 |
| `HANDOFF.md` (this file, added after `49fd3f1`) | +1 |

`git ls-files` and `find -type f` both return 43 at `49fd3f1` — no untracked or
ignored files are present in the directory.

## 8. Push status

**Already pushed.** The reconstruction is on GitHub and was pushed at the time
of its creation. Local `HEAD` and the remote branch tip are identical:

```
local  HEAD                                          49fd3f123c41899d4c9a127d8a513601f1e78b84
git ls-remote origin claude/research-evidence-docs-xcvi41  49fd3f123c41899d4c9a127d8a513601f1e78b84
```

Item 10 of the handoff request ("if not pushed, do not push") is therefore not
triggered.

## 9. Exact remote and branch

| Field | Value |
|---|---|
| Remote | `https://github.com/jayhaving/jayhaving` |
| Branch | `claude/research-evidence-docs-xcvi41` |
| Commit | `49fd3f123c41899d4c9a127d8a513601f1e78b84` |

Retrieval:

```bash
git clone --branch claude/research-evidence-docs-xcvi41 \
  https://github.com/jayhaving/jayhaving rz-evidence-src
cd rz-evidence-src
git rev-parse HEAD          # expect 49fd3f123c41899d4c9a127d8a513601f1e78b84
ls rz-research-evidence/02_episodes/   # expect D001 … D009
```

## 10. Integrity manifest

Git blob object IDs at commit `49fd3f1`. Verify any file with
`git hash-object <path>`, or the whole set with
`git ls-tree -r 49fd3f1 -- rz-research-evidence/`.

```
365d917cc40604f05cc492c90a3704c22ad36e59  00_method/EVIDENCE_SOURCES.md
e39be5e192679582ec489d42332afb4e1c8562be  00_method/METHOD.md
2502c0e3ac5fc47a477434485cc66f153b1d7601  00_method/PROVENANCE_NOTES.md
edffba0f1481779d6a7eec6ea09796d180f12f19  01_timeline/TIMELINE.md
78840f0410134709226325d84b70a63a980e657e  02_episodes/D001/OUTCOME_SEALED.md
4e29145da25a3a753e00eb154e133fd3759a7613  02_episodes/D001/PRE_DECISION.md
7f11b04b51044c91d367284d96e8b2d51f21103a  02_episodes/D001/RECEIPTS.md
5dc809cc9942d985843c2fc635b19981cb91d38d  02_episodes/D001/TECHNICAL_STATE.md
6de24c85086e22abc24a903332737b7f1818db3b  02_episodes/D002/OUTCOME_SEALED.md
96968381b8d8b83e04bd5e5e94e12766d1cc96c8  02_episodes/D002/PRE_DECISION.md
a3dd0fe6a8d84279cb845a28af850b8548c8e37b  02_episodes/D002/RECEIPTS.md
9e3226e18e3c9301e607ac950584597cc3acafdb  02_episodes/D002/TECHNICAL_STATE.md
f8abc1256d8f59ff04a43757104cd5c9533d435a  02_episodes/D003/OUTCOME_SEALED.md
5a9123ea80fc7ff6b6b20fc16db3a348f5359888  02_episodes/D003/PRE_DECISION.md
d13a633ddadd6d3dc154e24d0b1886f1b14f953f  02_episodes/D003/RECEIPTS.md
10b86e270412041a346c1b0f731adda5818eb33e  02_episodes/D003/TECHNICAL_STATE.md
92461810120ff28cd3182a2e4f977ba946fd54bf  02_episodes/D004/OUTCOME_SEALED.md
d69b7aa83a9ecd8198f26b5b527663466076e304  02_episodes/D004/PRE_DECISION.md
4006e19caf1373f874ba55783adec6dea03304af  02_episodes/D004/RECEIPTS.md
6e8d19dd2382bbd2f67d12045188981bc74d54ad  02_episodes/D004/TECHNICAL_STATE.md
cee9b399276eff9c81fcc12774a4159383d10e2d  02_episodes/D005/OUTCOME_SEALED.md
61e73e6a3f7a17f51938ba7ee63b76af0c29e5a8  02_episodes/D005/PRE_DECISION.md
134f8a75e5a07018f31169f10e1b10a7db1bc465  02_episodes/D005/RECEIPTS.md
4f07e0fc3563427e718899b4c16051f7c5029097  02_episodes/D005/TECHNICAL_STATE.md
2c8a7781f2c49814d69a27439b6b84789a292ce2  02_episodes/D006/OUTCOME_SEALED.md
2b36dd0e7c4c4bdab3fe5d111de42d321a8f99bc  02_episodes/D006/PRE_DECISION.md
4fa705cb2ddc27aa1c63d390cd53ee2d771e5367  02_episodes/D006/RECEIPTS.md
292658781c8229a2794fee4b5ce41abfdad64e2d  02_episodes/D006/TECHNICAL_STATE.md
129f267b0b2bc7363fdc9684cb1cd8b6a6b6f95e  02_episodes/D007/OUTCOME_SEALED.md
07407a648ee7df4378c2c3307632b2310a174f49  02_episodes/D007/PRE_DECISION.md
e55881cc928ed8cd11a50cb17725bcff6ab02345  02_episodes/D007/RECEIPTS.md
fa27773af99976749e93ccc871cbbf93c22cb37f  02_episodes/D007/TECHNICAL_STATE.md
47f31cc76d0f3b6a62e2c133c3399f31baa720d0  02_episodes/D008/OUTCOME_SEALED.md
c3e9846504e97403198d8e3e425eda3352c5f0d4  02_episodes/D008/PRE_DECISION.md
2d1e45ef165742db5ec31506a37c415a7326a2a9  02_episodes/D008/RECEIPTS.md
e7b58dd3235317a10c0913652efb22e122df045b  02_episodes/D008/TECHNICAL_STATE.md
bd8538f2dcb4bba7a311a3894cbe2a47ad89de85  02_episodes/D009/OUTCOME_SEALED.md
3b78bd50ee0032073997a0d0d62dd18e3fd89527  02_episodes/D009/PRE_DECISION.md
ba0cc40aa4ab500f6133cdcc50c70ddff6cb95bb  02_episodes/D009/RECEIPTS.md
8b22b6ccd1e47bbba287960440f2237ab71198b4  02_episodes/D009/TECHNICAL_STATE.md
8b203428eb954635e290d1ad8b905ed8bad97008  03_index/EPISODE_INDEX.md
2e8c24333b36edea01dccf04c1c4b6798603be8f  03_index/OPEN_QUESTIONS.md
d6b4e3a85159d76244cacdfa1d48db65eac610da  README.md
```

Paths above are relative to `rz-research-evidence/`.

---

## Notes for the auditor

**Read `00_method/METHOD.md` first.** It defines the separation rule the
episodes were written under, the meaning of the bounded decision moment, and the
three verification statuses (`VERIFIED-HERE`, `VAULT-ASSERTED`, `UNAVAILABLE`).
Auditing a `PRE_DECISION.md` without it will misread the receipt conventions.

**Audit direction.** `PRE_DECISION.md` should be checked against `RECEIPTS.md`
alone and a verdict reached **before** `OUTCOME_SEALED.md` is opened; the sealed
file is then used only to confirm the separation held. One direction, two
passes. Reading both halves together risks laundering hindsight into the earlier
document.

**Receipt reference integrity** was checked at authoring time: every
`[R-Dxxx-nn]` marker in all nine `PRE_DECISION.md` files resolves to a row in
the same episode's `RECEIPTS.md`. Three episodes (D005, D007, D009) define one
receipt each that `PRE_DECISION.md` does not cite; those support claims in
`TECHNICAL_STATE.md`.

**Source repositories examined by the reconstruction**, for independent
re-verification:

| Source | Location | State when read |
|---|---|---|
| S1 — RankZero vault | `https://github.com/jayhaving/rankzero-security-os` | `main` @ `ba9d042fb83f67c0622f38dc85c0408f80524aec` |
| S2 — Agentic IAM Gateway | `https://github.com/jayhaving/agentic-iam-gateway` | `main` @ `38ca81f431dd20056def093dc5f6f0a9a1ee8199`; `v4-session13` @ `13e79c8b2e607e07cfc0629f89cb8654edc5383e` |

Neither source repository was modified. RankZero's separate local development
working tree was not inspected for this handoff.
