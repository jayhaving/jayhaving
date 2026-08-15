# Provenance notes

Observations about the record itself, recorded because they bound what the
timestamps and authorship fields can support. None of these are criticisms;
they are limits on inference.

## Authorship identities in S1

| Commits | `author.name` | `author.email` |
|---|---|---|
| `b8638a1`, `39283a6` | `jayhaving` | `jasonawuah@icloud.com` |
| `17a50b7` … `ba9d042` (6 commits) | `Jason Awuah` | `YOUR_GITHUB_EMAIL` |

The email on the last six commits is the literal string `YOUR_GITHUB_EMAIL`, an
unsubstituted placeholder. Committer and author fields match on every commit,
and no commit carries a signature.

Consequences for reconstruction:

- The identity change at `17a50b7` reflects a **git configuration change**, not
  evidence of a second person. Whether one or more people were involved in any
  episode is **UNKNOWN**.
- No `Co-Authored-By` trailer, review record, issue, or pull request exists in
  either repository. There is no evidence of a second reviewer for any decision,
  and equally no evidence excluding one.

All S2 commits carry `jayhaving <jasonawuah@icloud.com>`.

## What the timestamps support

All S1 commits are authored in `−0400` (EDT). Author time and commit time are
identical on seven of eight commits; `b2fa397` shows a 31-second gap. There is
no rebase, amend, or cherry-pick signature in the history — the eight commits
form a linear chain.

This supports treating commit order as **work order**. It does not support
treating commit timestamps as decision timestamps; see METHOD.md on bounding.

## Tooling traces

S2 contains commit `4eaee8d` "chore: add Codex session instructions" and
`5028104` "chore: add current scoped task handoff" on the `v4-session13` branch,
both dated 2026-07-20 ~01:16 EDT. The gateway repository also tracks a
`NEXT_TASK.md` whose content the vault quotes.

This establishes that the gateway work used AI-assistant session handoffs. The
degree of AI involvement in the **vault** work of 2026-07-20 evening is
**UNKNOWN**: the vault contains Agent Skill packages and a `skills-lock.json`,
but no session transcript, tool log, or authorship trailer that would settle who
or what drafted any given document.

## Time gap between the two repositories

The gateway tip `13e79c8` is authored 2026-07-20 01:39:22 −0400. The vault's
first commit is 2026-07-20 19:20:25 −0400. The intervening 17h 41m contains no
commit in either repository. What occurred in that window is **UNKNOWN**.

## Density of the record

Eight commits in 3h 56m produced five ADRs, six risk records, six research and
change notes, twelve skill packages with schemas and fixtures, a validator
script, and a 274-line baseline report. Episodes state this density where it
bears on how tightly a decision moment can be bounded — several ADRs were
committed in the same commit as the evidence they cite, which is why those
episodes rely on category-2 information under METHOD.md and say so.
