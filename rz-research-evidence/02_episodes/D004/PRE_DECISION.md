# D004 — PRE_DECISION

**Episode:** Fix a linear evidence pipeline for Phase 2 review (ADR-002)
**Decision moment:** at or before 2026-07-20 21:03:10 −0400 `[R-D004-01]`
**Decision maker of record:** `Jason Awuah` `[R-D004-01]`
**Participants beyond the commit author:** UNKNOWN

D004 and D005 share a receipt commit. They are separate episodes because ADR-002
decides *ordering and handoff*, ADR-003 decides *authority between deterministic
checks and model reasoning*, and each is separately documented and separately
cited by later work.

---

## Situation as visible at the decision moment

### What existed 21 minutes earlier

One ordered pair of stages — Architecture Discovery then Threat Modeling —
established by ADR-001 `[R-D004-02]`. Phase 2 stood at 1 of 9 complete
`[R-D004-03]`. No JSON Schema, fixture, or validation script existed anywhere in
the repository `[R-D004-04]`.

### The stated problem

ADR-002's Context, committed with the decision (category-2 information under
`00_method/METHOD.md`) `[R-D004-05]`:

> The first Phase 2 batch introduces asset, attack-surface, authentication, and
> authorization specialists. Without stable handoffs, each skill could
> rediscover topology, rename entities, or draw conclusions from different
> evidence.

Three anticipated failure modes: rediscovered topology, renamed entities,
divergent evidence bases. As at D003, no artifact demonstrating any of them
exists in the corpus at this moment `[R-D004-06]`. The problem is stated
prospectively — the four specialists being ordered are introduced by this same
commit, so no run had yet produced a conflicting inventory `[R-D004-07]`.

### Alternatives on the table

Three, with recorded rejection grounds `[R-D004-05]`:

| Alternative | Recorded rejection ground |
|---|---|
| Run all specialists independently | "creates inconsistent inventories and duplicated evidence work" |
| Run authentication and authorization in parallel | rejected **as the default** because "authorization depends on explicit principal guarantees" |
| Run attack-surface mapping before asset discovery | "privileged paths need stable asset identities and classifications" |

The second alternative is rejected conditionally rather than absolutely — the
ADR's Consequences allow "Authorization waits for Authentication Review unless
equivalent principal guarantees already exist" `[R-D004-05]`.

### No target system

No external repository, commit, or executable system is referenced anywhere in
S1 at this moment `[R-D004-08]`. The pipeline is designed before it is applied
to anything.

---

## The decision

A default six-stage pipeline `[R-D004-05]`:

```text
Architecture Discovery
        ↓
Asset Discovery
        ↓
Threat Model Generator
        ↓
Attack Surface Mapper
        ↓
Authentication Review
        ↓
Authorization Review
```

With two preservation requirements `[R-D004-05]`:

1. Preserve component, boundary, asset, entry-point, operation, identity-path,
   and decision-path **identifiers** across handoffs.
2. Preserve evidence locators, contradictions, unknowns, and scope limits
   "rather than flattening them."

### Consequences accepted

Four, as recorded `[R-D004-05]`:

- the orchestrator enforces prerequisites and handoffs;
- threat hypotheses may guide mapping, but Attack Surface Mapping **recomputes**
  reachability rather than inheriting it;
- authorization waits for authentication unless equivalent principal guarantees
  exist;
- **missing prerequisites produce partial or blocked outputs rather than
  inferred facts.**

### Mechanism shipped with the decision

Identifier stability was made enforceable rather than advisory. The commit adds
four JSON Schema Draft 2020-12 output contracts, four valid fixtures, four
deliberately invalid fixtures, and a 345-line dependency-free validator
`[R-D004-09]` `[R-D004-10]`. The validator includes a
`validate_cross_references` function that checks identifier agreement between
specialist outputs `[R-D004-11]`.

Ownership of identifier namespaces was recorded in the architecture note
`[R-D004-12]`:

- Architecture Discovery owns component, interface, flow, boundary, environment identifiers
- Asset Discovery owns `AST-###` identifiers
- Attack Surface Mapping owns entry-point, operation, and path identifiers

### Validation status at the decision moment

The ADR distinguishes what was done from what was not `[R-D004-05]`:

> The batch validator checks package contracts, schemas, fixtures, and internal
> references. **A later forward test must pass one repository evidence set
> through the complete chain** without renaming identifiers or losing
> contradictions.

So at the decision moment the pipeline is verified only against fixtures the
project authored for itself. No real evidence set had traversed it
`[R-D004-07]`.

### Scope of the commit

35 files `[R-D004-13]`: four skill packages (SKILL.md, `agents/openai.yaml`,
`schemas/output.schema.json`, `examples/valid-output.json`,
`tests/invalid-output.json` each), four vault notes, ADR-002, ADR-003, the
validator script, a dated change-log entry, and modifications to the
orchestrator (0.2.0 → 0.3.0), registry, home, architecture, roadmap, change log,
and project memory.

### Follow-up recorded

- "Use the pipeline for API, MCP, RAG, and infrastructure review skills."
- "Add cross-skill end-to-end fixtures **when a representative target is
  available**." `[R-D004-05]`

The second acknowledges that no representative target was available at the
decision moment.
