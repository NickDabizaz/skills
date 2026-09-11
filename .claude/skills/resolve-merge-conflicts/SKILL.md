---
name: resolve-merge-conflicts
description: "Resolve merge conflicts with the spec and the tickets on both sides as the reference. Use when a merge or rebase stops on conflicts, from implement-all or on the user's request."
---

The spec and the two tickets decide; nothing is guessed.

## Read

1. `git status`: every conflicted file.
2. Each side's ticket, from the branch name and commit messages; open both tickets and the spec.
3. Each side's full diff against the merge base for every conflicted file, not only the marked hunks.

## Resolve, per file

- Both sides' acceptance criteria hold after resolution. Different behaviour touched: keep both changes.
- The same behaviour changed two ways: the spec or ticket line that names it decides; quote it.
- No line decides: stop and put it to the user as one question, options being each side and a combination, with a recommendation.
- Remove the markers, then run lint, typecheck, and the tests of both tickets.

## Done when

No conflict marker remains, both tickets' tests pass, and the resolution is committed with a message naming the two tickets and the reference line behind each decision. Report each decision.
