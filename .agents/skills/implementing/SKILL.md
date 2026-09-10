---
name: implementing
description: "The build loop shared by implement and implement-all: find the plan, build it step by step with the verification the mode demands, tick the ticket, hand off to review. Reached by those two skills; not a starting point on its own."
---

Build the plan exactly as agreed. The plan is the contract: nothing is added, dropped, or reinterpreted without the user. Mode per [MODES.md](MODES.md).

## Find the plan

In order:

1. The ticket passed: a `.issues/<issue-name>/tickets/` path or a GitHub issue number, in the format of [TICKET-FORMAT.md](../write-tickets/TICKET-FORMAT.md). Read the `spec.md` beside it (GitHub: the folder its `issue:` label names) too.
2. A spec path passed, or the `.issues/<issue-name>/spec.md` the user named. Own project: a spec is built through its tickets; stop and tell the user to run `/write-tickets`.
3. A plan agreed in this conversation by `discuss`, `discuss-with-docs`, `investigate`, or `research`.

Legacy: a `.issues/audit/tickets/` path or an issue labelled `issue:audit` is a ticket like any other.

None: stop and tell the user to run `/discuss`, `/discuss-with-docs`, `/investigate`, or `/research`. There is no plan to invent.

## Before writing code

Read `CLAUDE.md` / `AGENTS.md` and `CONTEXT.md` where present, `DESIGN.md` and the plan's UX flow when the work touches UI, then the code around what you will change.

- **Callers**: for every function, type, endpoint, or schema the plan changes, search for every caller. Callers the change affects join the plan's steps. Done when the search is exhaustive; memory does not count.
- **Standards**: in the mode's priority. New code takes the shape of its neighbours: naming, structure, error handling, test style. A neighbour that is clearly flawed (a bug, a pattern the documented conventions forbid, a dead idiom) is put to the user as one question with options and a recommendation, discuss-style, before it is copied.
- **Reuse**: before creating any UI component, read the Patterns and Components of `DESIGN.md` (legacy: the components already in the code) and search the codebase for one serving the same purpose. One that fits behind a new prop is extended, never copied; one entity's create and edit are one component in two modes. A near-duplicate you judge unavoidable is a deviation: put it to the user as one question with options and a recommendation, discuss-style.
- **Legacy verification** (also an own project whose `CONTEXT.md` says `tests: none`): ask one question before the first change: A. lint and typecheck plus a traced logic check of the changed path (recommended, the default); B. the existing tests nearest the change; C. characterization tests written first for the code touched. The answer is the verification for this run.

## Build

A ticket goes to `in-progress` first (GitHub: the label).

**Own project** (`tests: acceptance`):

1. From each acceptance criterion, write an acceptance test. Run it: it fails, for the reason the criterion names, before any code exists.
2. Per checklist step: a failing test (the acceptance test, or a smaller one), the smallest code that passes it, then tidy without changing behaviour. Tick the step's box when its done-condition holds.
3. The full suite is green at the end.

**Legacy** (and `tests: none`): work the steps in order. A step is done when its done-condition holds under the verification the user chose. Run the repo's lint, typecheck, and existing suite once at the end.

When the plan turns out to be wrong or blocked (a step cannot be done as written, or a decision it rests on is false), stop and put the conflict to the user as one question with options and a recommendation, discuss-style. Deviation is the user's call.

## Hand off to review

When every step's done-condition holds and verification passes, call the Skill tool with "review", pointing it at the diff, the ticket, and the spec.

- Findings: fix them, then call the Skill tool with "review" again. Three rounds at most; findings still open after the third go to the user as-is.
- PASS: ticket to `done` (GitHub: close the issue). When it was the spec's last open ticket and no `implement-all` run owns the cleanup, delete `.issues/<issue-name>/` (the ideas, the spec, and its tickets).
- Report done: what was built, how it was verified, and anything the user should know.

Commit only when the user or the calling skill asks.
