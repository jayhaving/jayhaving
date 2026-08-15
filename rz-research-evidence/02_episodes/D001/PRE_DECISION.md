# D001 — PRE_DECISION

**Episode:** Adopt a Git-versioned Obsidian vault as the durable memory substrate
**Decision moment:** at or before 2026-07-20 19:20:25 −0400 `[R-D001-01]`
**Decision maker of record:** `jayhaving <jasonawuah@icloud.com>` `[R-D001-01]`
**Participants beyond the commit author:** UNKNOWN — no review record, trailer, issue, or PR exists in the corpus `[R-D001-13]`

---

## Situation as visible at the decision moment

### A knowledge-vault practice already existed, inside the product repository

As of 2026-07-20 01:39:22 −0400 — 17h 41m before this episode — the
`agentic-iam-gateway` repository tracked a documentation vault at `docs/vault/`
containing 13 markdown documents plus a machine-readable `status.json`
`[R-D001-02]`. Its own README describes it as "a MAP, not content" totaling
"~3500 lines" `[R-D001-03]`.

That prior vault already contained the structural elements that reappear in this
episode's decision `[R-D001-02]` `[R-D001-04]`:

| Prior artifact (`docs/vault/`) | Function |
|---|---|
| `01-Decision-Log.md` | 13 dated decisions, `DEC-001` … `DEC-013`, recording *why* rather than *what* |
| `04-Known-Gaps-and-Honesty-Log.md` | Gap taxonomy `GAP-001` … `GAP-016`, OPEN/CLOSED with test IDs |
| `03-Test-Status.md`, `status.json` | Capability-to-test-ID mapping |
| `02-Session-Notes.md` | One entry per working session |
| `NEXT_TASK.md` | Single current scoped task, "overwritten, never appended" |

`status.json` carries an explicit editing rule: it "may ONLY be edited by
changing 'tested' status based on actual verified test runs this session. Never
mark 'tested: true' without a corresponding real, currently-passing test ID"
`[R-D001-04]`.

**INFERENCE:** the practice of separating claims from evidence, and of recording
gaps as first-class tracked objects, predates this episode and was carried into
it rather than invented at it. Basis: the prior vault's decision log, honesty
log, and status-rule text all exist at `13e79c8` (2026-07-20 01:39), and the
same three functions appear in the new vault's `04-Decisions`, `07-Risks`, and
`12-Memory` structure created at 19:20:25. The reasoning step is structural
correspondence plus temporal order; no document states the carry-over
explicitly.

### The prior vault's known limits, as visible at the decision moment

The prior vault was scoped to one executable prototype, lived inside that
prototype's repository, and its session-handoff file was explicitly
non-accumulating `[R-D001-03]`. Whether these limits motivated the new substrate
is **UNKNOWN** — no document in the corpus states a motivation.

### Product intent at the decision moment

The vision recorded in this episode states RankZero is "an AI Security Operating
System" with a lifecycle north star of `Design → Build → Admit → Run → Observe →
Detect → Respond → Learn`, eight named engines including "Security Memory", and
a five-point quality standard for a skill, the fifth of which is "improves
future work" `[R-D001-05]`.

Seven foundation skills were recorded as already existing at this moment
`[R-D001-06]`: Threat Model Generator, Agent Call Lifecycle, Context Isolation,
Security Plugin Builder, Runtime Debug, Skill Admission Review, and Security
Orchestrator. Where their packages resided at 19:20:25 is **UNKNOWN**; they are
present as *vault notes* in this commit, and their executable packages do not
enter the repository until D002 `[R-D001-07]`.

### Available alternatives

The corpus records no alternatives considered for this decision. No ADR was
written for it; the choice is recorded only as a change-log line and as the
README's setup instructions `[R-D001-08]` `[R-D001-09]`. Whether alternatives
were weighed is **UNKNOWN**.

---

## The decision

A three-layer memory model, stated in the README committed at the decision
moment `[R-D001-09]`:

> - Obsidian is the readable knowledge layer.
> - Git is the authoritative version history.
> - RankZero skills are the executable procedural layer.

Committed as a standalone vault repository separate from the product repository
`[R-D001-01]` `[R-D001-10]`, with eight memory rules governing what must be
recorded `[R-D001-11]`:

1. Record major decisions as ADR-style decision notes.
2. Record each skill as a versioned note.
3. Record meaningful research with source and implications.
4. Record every architecture change in the change log.
5. Record failed experiments and rejected approaches.
6. Link findings to skills, decisions, risks, and sources.
7. Never store raw credentials or secrets.
8. Git history remains the authoritative record of file changes.

The change log records the decision in two lines: "Preserve durable memory in a
Git-versioned Obsidian vault" and "Treat skills as versioned software assets, not
static prompts" `[R-D001-08]`.

### Scope committed at the decision moment

33 files in one commit `[R-D001-10]`: vision, current architecture, a skill
registry with eight skill notes, an empty decision log, research index, risk
register, roadmap, change log, project memory, six templates, four Obsidian
Bases dashboards, one canvas, `.gitignore`, README, and the
`rankzero-project-memory` Agent Skill with its vault-conventions reference.

Four minutes later, four third-party Obsidian skills were added from
`kepano/obsidian-skills` — `json-canvas`, `obsidian-bases`, `obsidian-cli`,
`obsidian-markdown` — each pinned by SHA-256 in `skills-lock.json` `[R-D001-12]`.
The README had already directed that these be added separately `[R-D001-09]`,
so the second commit completes the substrate rather than revising it.

### Roadmap position declared at the decision moment

Phase 1 (Foundation) all eight items checked; Phase 2 (Engineering) nine items
open; Phases 3 and 4 fully open `[R-D001-07]`.

---

## What was not known at the decision moment

Recorded here to bound the reconstruction, not to foreshadow:

- No ADR existed. `04-Decisions/Decision Log.md` was created empty, containing
  only an embedded dashboard view `[R-D001-10]`.
- No risk record existed. `07-Risks/Risk Register.md` was created with only an
  embedded dashboard view `[R-D001-10]`.
- The `07-Risks/Known Gaps.md` file did not exist at this commit `[R-D001-10]`.
- `02-Architecture/Current Architecture.md` was created with `status: draft`
  `[R-D001-14]`.
