# Episode index

## Selection criteria

A commit becomes a decision episode when it satisfies all three:

1. **A choice was made.** The artifact records a selection among alternatives,
   a scope boundary, or a rule constraining later work — not merely an addition
   of content.
2. **It constrained subsequent work.** Later artifacts in the corpus depend on
   it, cite it, or are shaped by it.
3. **It is separately receiptable.** The choice has its own durable artifact,
   so its receipts do not collapse into another episode's.

Two commits sharing a timestamp can still be two episodes when they introduce
two separately documented decisions (D004/D005 and D007/D008). Conversely, two
commits can be one episode when they complete a single decision (D001).

## Accepted

| ID | Decision | Receipt commit(s) | Why it qualifies |
|---|---|---|---|
| D001 | Durable memory substrate: Obsidian readable layer, Git authoritative, skills executable | `b8638a1`, `39283a6` | Establishes the evidence regime every later episode is recorded in |
| D002 | Install specialist packages unmodified; version the orchestrator; decline the non-RankZero file | `17a50b7` | An admission decision plus the "skills as versioned assets" rule |
| D003 | Discovery precedes threat modeling (ADR-001) | `b2fa397` | Reorders the review workflow; three alternatives explicitly rejected |
| D004 | Linear evidence pipeline with preserved identifiers (ADR-002) | `54976fd` | Fixes handoff order for all Phase 2 work; three alternatives rejected |
| D005 | Deterministic checks authoritative, LLM interpretive (ADR-003) | `54976fd` | The load-bearing constraint later invoked to classify RZ-005 |
| D006 | Reconcile the recovered prototype before building on its claims | `df3cace` | Scope boundary that withheld remediation and the API skill pending verification |
| D007 | Build API Security Review only from observed surface (ADR-004) | `6cb5ef0` | Gates a product artifact on executable evidence |
| D008 | LLM output cannot mutate enforcement state (ADR-005) | `6cb5ef0` | Converts D005's principle into a product-level prohibition and reclassifies observed code |
| D009 | Publish a baseline with explicit non-readiness disclosures | `ba9d042` | A publication-scope decision; the corpus's terminal state |

## Rejected, with reason

| Candidate | Reason not an episode |
|---|---|
| S2 `1a648f3`, `38ca81f`, `1ced058` (2026-07-13) | Predate the corpus under reconstruction; retained as background in TIMELINE.md |
| S2 `fb44b19` … `13e79c8` (2026-07-20 00:53–01:39) | Gateway construction and documentation. Consequential to the project, but the decisions behind them are not documented in reachable evidence — reconstructing them would be invention. Their **output** is documented as technical state in D006–D008 |
| S1 `39283a6` as a separate episode | Completes D001's substrate rather than deciding anything new; four third-party skills added under a lockfile |
| Orchestrator version bumps (v0.1.0 → v0.4.0) | Consequences of D002–D007, not independent decisions. Tracked in each episode's TECHNICAL_STATE.md |
| Individual risk records RISK-001 … RISK-006 | Findings recorded by D007/D008's commit, not decisions |
| The gateway remediation itself (`285c748`, between 22:07 and 23:16) | Consequential — it is the corpus's only product-code response to the findings — but **not reconstructible as an episode**. It produced no reachable artifact: the commit is absent from the public remote, and it is described only from the outside by the vault. Every fact about it would be VAULT-ASSERTED, so no PRE_DECISION could be receipted. It is recorded as an input to D009 and as an unresolved gap in OPEN_QUESTIONS.md |
| S3 profile-repo commits | Unrelated to RankZero |

## Coverage statement

Nine episodes cover all eight vault commits. Six of fourteen gateway commits are
background rather than episodes, for the stated reason. No commit in either
repository was skipped without an entry above.

## Known asymmetry in the episode set

D001–D005 are decisions about **method** and are receiptable almost entirely
from artifacts reachable here. D006–D009 are decisions about **an external
executable system**, and their factual basis rests substantially on builds,
test runs, and filesystem searches performed on an unreachable workstation.
Episodes D006–D009 therefore carry a higher proportion of VAULT-ASSERTED
receipts. This is a property of the corpus, not of the decisions.
