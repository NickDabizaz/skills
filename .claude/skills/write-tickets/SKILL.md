---
name: write-tickets
description: "Split an agreed spec, the findings of investigate, or the findings of audit into tickets: one per unit of work, each with acceptance criteria, a checklist, and what blocks it."
argument-hint: "[path to .issues/<issue-name>/spec.md or report.md]"
disable-model-invocation: true
---

Own projects, plus an audit or research spec in a legacy repo ([MODES.md](../implementing/MODES.md)). Any other spec in a legacy repo: stop, tickets there come from the user's tracker.

## Input

In order:

1. The spec path passed, else the one `.issues/*/spec.md` matching the work. `.issues/audit/spec.md` is the spec `audit` wrote; its findings are the units below.
2. The report path passed, else the one `.issues/*/report.md` matching the work, written by `investigate`: write `spec.md` beside it first, in the spec format (goal, decisions, plan, criteria, out of scope from the report) with the report linked from its goal, then split it below. Its tickets are type `bug`.
3. The research path passed, else the one `.issues/*/research.md` matching the work, written by `research` ([RESEARCH-FORMAT.md](../research/RESEARCH-FORMAT.md)): treat it as 2 treats the report, linked from the spec's goal. Its tickets are type `feature` when the research chose a technology, `bug` when it chased a problem.

None: stop and tell the user to run `/discuss-with-docs`, `/investigate`, `/research`, or `/audit`.

## Split

- One ticket per unit that can be built, tested, reviewed, and merged on its own: one or a few acceptance criteria, in one area of the code where possible. Audit findings in one area with one cause become one ticket; the ticket names the finding ids it covers.
- Every acceptance criterion of the spec lands in exactly one ticket; the ticket's checklist carries the spec's steps that serve it, each with its done-condition.
- `blocked-by` lists the tickets whose output this one needs. A cycle is a split error: re-split until none remains.
- Number in dependency order from 01 within the spec's `tickets/` folder.

Present the split as a list (id, title, type, blocked-by) and ask which to write: all, or the ids the user names. Renumber the chosen ones from 01; a `blocked-by` pointing at an unchosen ticket goes to the user as one question (drop the dependency, or include that ticket). Nothing is written before the answer.

## Write

Backend as `CONTEXT.md` says; without `CONTEXT.md` (an audit or research spec in a legacy repo) ask one question, local or github, and with local add `.issues/` to `.git/info/exclude` when it is not ignored. Body per [TICKET-FORMAT.md](TICKET-FORMAT.md):

- **local**: one file `.issues/<issue-name>/tickets/<nn>-<slug>.md` per ticket, beside the spec.
- **github**: `gh issue create` per ticket, title from the ticket, labels `type` and `issue:<issue-name>`, the ticket body as the issue body. The issue number becomes the id; rewrite `blocked-by` with the numbers once all issues exist. The spec folder stays as the local reference.

Leave the spec in place.

## Done when

Every chosen unit is one ticket, no `blocked-by` cycle exists, and each ticket is written in the backend. Then tell the user the two ways on: `/implement .issues/<issue-name>/tickets/01-<slug>.md` (or `/implement <issue number>`) for one ticket, `/implement-all .issues/<issue-name>/spec.md` for all of them. Stop.
