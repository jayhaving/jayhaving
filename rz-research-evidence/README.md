# rz-research-evidence

Historical reconstruction of consequential decision episodes in the RankZero
project, assembled 2026-08-15.

This workspace is **reconstruction only**. It does not judge whether any
historical decision was good or bad, and it does not evaluate Saddle
Engineering.

## Layout

```
rz-research-evidence/
├── README.md                  this file
├── 00_method/
│   ├── METHOD.md              reconstruction rules and separation discipline
│   ├── EVIDENCE_SOURCES.md    every source, its access status, its limits
│   └── PROVENANCE_NOTES.md    authorship, timestamps, and what they do not prove
├── 01_timeline/
│   └── TIMELINE.md            observed event sequence
├── 02_episodes/
│   └── D001 … D009/           one directory per decision episode
│       ├── PRE_DECISION.md    information demonstrably available at decision time
│       ├── RECEIPTS.md        the receipt for every material claim
│       ├── OUTCOME_SEALED.md  later outcomes and later discoveries
│       └── TECHNICAL_STATE.md system state at the episode boundary
└── 03_index/
    ├── EPISODE_INDEX.md       the episode set and why each was selected
    └── OPEN_QUESTIONS.md      what remains UNKNOWN and what would resolve it
```

## Episode set

| ID | Decision episode | Decision moment (bounded) |
|---|---|---|
| D001 | Adopt a Git-versioned Obsidian vault as the durable memory substrate | ≤ 2026-07-20 19:20 EDT |
| D002 | Install downloaded specialist skills unmodified; version the orchestrator; decline the non-RankZero review file | ≤ 2026-07-20 20:33 EDT |
| D003 | Insert Architecture Discovery ahead of threat modeling (ADR-001) | ≤ 2026-07-20 20:42 EDT |
| D004 | Fix a linear evidence pipeline for Phase 2 review (ADR-002) | ≤ 2026-07-20 21:03 EDT |
| D005 | Make deterministic checks authoritative over LLM reasoning (ADR-003) | ≤ 2026-07-20 21:03 EDT |
| D006 | Reconcile the recovered Rust prototype before building on its claims | ≤ 2026-07-20 21:33 EDT |
| D007 | Build API Security Review only from an observed executable surface (ADR-004) | ≤ 2026-07-20 22:07 EDT |
| D008 | Prohibit LLM output from mutating enforcement state (ADR-005) | ≤ 2026-07-20 22:07 EDT |
| D009 | Publish Baseline Report v0.1 without a production-readiness claim | ≤ 2026-07-20 23:16 EDT |

Nine episodes were selected from fourteen source commits across two
repositories. Selection criteria are in `03_index/EPISODE_INDEX.md`.

## On Saddle Engineering

The instruction set for this reconstruction directs that Saddle Engineering not
be evaluated. No artifact naming "Saddle Engineering" was found anywhere in the
evidence corpus reachable from this workspace: a case-insensitive search for
`saddle` across the full RankZero vault returned zero files. Its relationship to
these episodes is therefore **UNKNOWN**, and it is not documented, characterized,
or assessed anywhere in this workspace.

## Reading order

Start with `00_method/METHOD.md`, which defines the separation rule that governs
every episode directory. Then `01_timeline/TIMELINE.md` for sequence, then
individual episodes.
