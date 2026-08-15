# Method

## Purpose

Reconstruct what was decided, when, and on what visible basis. Nothing here
assesses decision quality, and nothing here evaluates Saddle Engineering.

## The separation rule

Each episode directory enforces one hard boundary:

- **PRE_DECISION.md** contains only information demonstrably available at or
  before the decision moment. If a fact first becomes visible in a later
  artifact, it does not appear in PRE_DECISION.md in any form — not as a hint,
  not as foreshadowing, not as a rhetorical question.
- **OUTCOME_SEALED.md** contains everything that came later: consequences,
  subsequent findings, and discoveries made during this 2026-08-15
  reconstruction.

Writing to OUTCOME_SEALED.md never licenses editing PRE_DECISION.md.

## Bounding the decision moment

A decision is not observable directly; only its durable artifact is. For every
episode the decision moment is therefore recorded as an **upper bound**: the
authored timestamp of the first commit containing the decision's artifact. The
decision was taken at or before that instant. How long before is **UNKNOWN**
unless an earlier dated artifact narrows it.

"Information available at decision time" is consequently defined as:

1. the state of the repository at the parent commit, plus
2. the artifacts introduced by the decision commit itself that describe inputs
   rather than conclusions (for example, an ADR's Context section), plus
3. any external artifact independently datable to before that instant.

Where category 2 is used, the episode says so explicitly, because an ADR's
Context section is the decision-maker's own account of their inputs and is not
independent corroboration.

## Claim discipline

Every material factual claim in PRE_DECISION.md carries a receipt reference of
the form `[R-Dxxx-nn]` resolving to an entry in the same episode's RECEIPTS.md.

Three labels are used throughout:

- **UNKNOWN** — the evidence needed does not exist in the reachable corpus. Used
  in preference to a plausible reconstruction.
- **INFERENCE** — a conclusion drawn from evidence rather than stated by it. The
  supporting evidence and the reasoning step are both named.
- **VAULT-ASSERTED** — recorded in the RankZero vault at a known commit, where
  the underlying artifact (a local filesystem path, a test run, a machine that
  no longer answers) is not reachable from this reconstruction. A
  VAULT-ASSERTED claim is evidence that the project *recorded* something at a
  known time. It is not independent confirmation that the recorded thing was so.

Receipts additionally carry a verification status:

| Status | Meaning |
|---|---|
| VERIFIED-HERE | Re-checked in this reconstruction against a primary artifact |
| VAULT-ASSERTED | Present in the vault at a stated commit; underlying artifact unreachable |
| UNAVAILABLE | Referenced by the record but not locatable from this workspace |

## What is primary evidence

Primary evidence for this reconstruction is:

- Git objects and their metadata in the two reachable repositories.
- File contents at specific commits in those repositories.
- Remote ref advertisements observed on 2026-08-15.

Vault prose is primary evidence **of the project's own record-keeping** at a
timestamp. It is secondary evidence for the external facts it describes. This
distinction is applied consistently and is the reason many claims below are
labeled VAULT-ASSERTED rather than verified.

## Non-modification

No primary evidence was altered. The two source repositories were cloned to
scratch locations and read. One scratch clone had a branch checked out to read
file contents at a historical ref; no commit, push, or write to any source
repository occurred. All output is new files under `rz-research-evidence/`.

## Selection

Nine episodes were reconstructed from fourteen commits across two repositories.
Commits that only add files without resolving a question — the two
initialization commits are treated as a single episode, and the gateway repo's
documentation commits are treated as background — are not given episodes of
their own. Criteria and the full accept/reject list are in
`03_index/EPISODE_INDEX.md`.
