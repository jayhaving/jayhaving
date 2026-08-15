# D001 — OUTCOME_SEALED

Everything below became visible **after** the decision moment
(2026-07-20 19:20:25 −0400). None of it appears in PRE_DECISION.md.

---

## Immediate consequences, same session (2026-07-20)

The substrate was used for every subsequent episode in the corpus. Within
3h 52m of the second commit, the vault accumulated:

| Artifact type | Count at S1 HEAD | First appearance |
|---|---|---|
| ADRs | 5 | `b2fa397` (D003) |
| Risk records | 6 | `6cb5ef0` (D007/D008) |
| Research notes (excluding the index) | 3 | `df3cace` (D006) |
| Dated change-log entries | 5 | `b2fa397` (D003) |
| Machine-readable evaluations | 8 JSON | `6cb5ef0` (D007/D008) |
| RankZero skill packages under `.agents/skills/` | 14 — one at this episode's boundary, 13 added later | `17a50b7` (D002) |
| Validator scripts | 1 | `54976fd` (D004/D005) |

Memory rules 1, 2, 3, 4, 6, 7 and 8 were exercised. **Memory rule 5 — "Record
failed experiments and rejected approaches" — has no dedicated artifact
anywhere in the corpus.** Rejected approaches appear only inside ADR
"Alternatives Considered" sections (D003, D004, D005) and in one installation
note (D002). No experiment record exists, and `14-Templates/Experiment
Template.md` is never instantiated.

## The three-layer model in practice

| Layer as declared | What the corpus shows |
|---|---|
| Obsidian = readable knowledge layer | Held. All 8 commits write markdown with Obsidian frontmatter, wikilinks, Bases embeds, and callouts |
| Git = authoritative version history | Held within S1. It did **not** extend to the product repository — see below |
| RankZero skills = executable procedural layer | Partially held. Skill packages carry JSON Schemas and fixtures; a validator script exists. The "execution" of the specialists against real code is recorded as prose and JSON output, with no run log |

## Later discovery — the authority boundary did not reach the product

The vault's own baseline report, written at the corpus's final commit, records
that the gateway remediation lived on a local branch
`remediation/security-boundaries` at `285c748065a014a202b66a2638e5b86c8361daa3`
that "was not pushed or merged into the gateway's default branch."

**Discovered in this reconstruction, 2026-08-15:** that state never changed.

```
$ git ls-remote https://github.com/jayhaving/agentic-iam-gateway
38ca81f431dd20056def093dc5f6f0a9a1ee8199   HEAD
38ca81f431dd20056def093dc5f6f0a9a1ee8199   refs/heads/main
13e79c8b2e607e07cfc0629f89cb8654edc5383e   refs/heads/v4-session13
```

`285c748` is not reachable in S2 — `git cat-file -t` on it fails with "could not
get object info" against a full clone. Two branches, no tags.

The consequence for D001 specifically: the decision made Git authoritative **for
the vault**, and the vault's most consequential downstream artifact — the
remediation of the reviewed prototype — exists in the reachable record only as a
40-character hash and a set of prose claims about it. Whether that work survives
on the workstation that produced it is UNKNOWN from here.

Additionally, `main` in S2 remains at `38ca81f`, a commit titled "Initial commit:
RankZero Agentic IAM Gateway" dated 2026-07-13 19:49 — meaning the default
branch never received the V4 single-binary gateway (`fb44b19`, 2026-07-20 00:53)
either. All V4 work sits on `v4-session13`.

## Substrate durability

| Observation (2026-08-15) | Value |
|---|---|
| S1 HEAD | `ba9d042` — unchanged since 2026-07-20 23:16:05 |
| Last push to S1 (GitHub metadata) | 2026-07-21 03:21 |
| S1 commits in the 26 days since | 0 |
| S2 commits in the 26 days since | 0 |

The vault was created, filled in a single four-hour session, pushed the
following morning, and has not been written to since. Whether work continued
elsewhere is UNKNOWN.

## Related repository observed later

`jayhaving/agentic-iam-getway` — a second repository whose name differs from
`agentic-iam-gateway` by one transposition — exists, is public, was last pushed
2026-07-13, and advertises **zero refs** (`git ls-remote` returns empty). It is
not referenced anywhere in the vault. Its relationship to this work is UNKNOWN.

## Not an evaluation

This file records what happened after the decision. It takes no position on
whether the substrate choice was correct, and none of the above is offered as a
judgment of the decision-maker.
