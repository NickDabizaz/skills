---
name: implementing
description: "The build loop shared by implement and implement-all: find the plan, build it step by step with the verification the mode demands, tick the ticket, hand off to review. Reached by those two skills; not a starting point on its own."
---

Build the plan exactly as agreed. The plan is the contract: nothing is added, dropped, or reinterpreted without the user. Mode per [MODES.md](MODES.md).

## Find the plan

In order:

1. The ticket passed: a `.workspace/<issue-name>/tickets/` path or a GitHub issue number, in the format of [TICKET-FORMAT.md](../write-tickets/TICKET-FORMAT.md). Read the `spec.md` beside it (GitHub: the folder its `issue:` label names) too.
2. A spec path passed, or the `.workspace/<issue-name>/spec.md` the user named. Own project: a spec is built through its tickets; stop and tell the user to run `/write-tickets`.
3. A plan agreed in this conversation by `discuss`, `discuss-with-docs`, `investigate`, or `research`.

Legacy: a `.workspace/audit/tickets/` path or an issue labelled `issue:audit` is a ticket like any other.

None: stop and tell the user to run `/discuss`, `/discuss-with-docs`, `/investigate`, or `/research`. There is no plan to invent.

## Before writing code

Read `CLAUDE.md` / `AGENTS.md` and `CONTEXT.md` where present, `DESIGN.md` and the plan's UX flow when the work touches UI, then the code around what you will change.

- **Callers**: for every function, type, endpoint, or schema the plan changes, search for every caller. Callers the change affects join the plan's steps. Done when the search is exhaustive; memory does not count.
- **Standards**: in the mode's priority. New code takes the shape of its neighbours: naming, structure, error handling, test style. A neighbour that is clearly flawed (a bug, a pattern the documented conventions forbid, a dead idiom) is put to the user as one question with options and a recommendation, discuss-style, before it is copied. Identifiers follow `CONTEXT.md`'s Conventions and each Domain entity's identifier even when the ticket or spec prose is in another language.
- **Smallest fix**: before adding anything, check in order — does the ticket actually call for it (a step nobody asked for stays undone, not built ahead of time); does this codebase, the language's standard library, or the platform already do it; does an already-installed dependency cover it. Take the first yes. When a real constraint forces a corner cut anyway, mark it at the cut — `shortcut: <what was cut short>, revisit when <the trigger>` ([SHORTCUT-FORMAT.md](SHORTCUT-FORMAT.md)) — never leave one unmarked.
- **Reuse**: before creating any UI component, read the Patterns and Components of `DESIGN.md` (legacy: the components already in the code) and search the codebase for one serving the same purpose. One that fits behind a new prop is extended, never copied; one entity's create and edit are one component in two modes. A near-duplicate you judge unavoidable is a deviation: put it to the user as one question with options and a recommendation, discuss-style.
- **Visual parity**: read [FIDELITY.md](../prototype/FIDELITY.md) whenever the ticket, spec, or conversation supplies a reference. Open the approved baseline and its assets, reconcile its screen contract, then preserve the presentation while adapting the code to the stack. A missing ticket link does not waive a known baseline. Library defaults and component reuse must meet the same contract; conflicts follow FIDELITY.md before implementation.
- **Legacy verification** (also an own project whose `CONTEXT.md` says `tests: none`): ask one question before the first change: A. lint and typecheck plus a traced logic check of the changed path (recommended, the default); B. the existing tests nearest the change; C. characterization tests written first for the code touched; D. TDD — a failing test per checklist step before any code for it. The answer is the verification for this run.

## Build

A ticket goes to `in-progress` first (GitHub: the label).

**Own project** (`tests: acceptance`):

1. From each acceptance criterion, write an acceptance test. Run it: it fails, for the reason the criterion names, before any code exists.
2. Per checklist step: a failing test (the acceptance test, or a smaller one), the smallest code that passes it, then tidy without changing behaviour. Tick the step's box when its done-condition holds.
3. The full suite is green at the end.

**Legacy** (and `tests: none`), verification chosen is D: per checklist step, a failing test first, the smallest code that passes it, then tidy without changing behaviour — the same rhythm as the own-project steps above, sourced from the checklist instead of an acceptance criterion. Tick the step's box when its done-condition holds; the full suite is green at the end.

**Legacy** (and `tests: none`), any other verification: work the steps in order. A step is done when its done-condition holds under the verification the user chose. Run the repo's lint, typecheck, and existing suite once at the end.

When the plan turns out to be wrong or blocked (a step cannot be done as written, or a decision it rests on is false), stop and put the conflict to the user as one question with options and a recommendation, discuss-style. Deviation is the user's call.

## Hand off to review

For UI with a baseline, run FIDELITY.md verification and retain its evidence before handoff; functional tests alone do not close the UI criteria.

When every step's done-condition holds and verification passes, call the Skill tool with "review", pointing it at the diff, the ticket, and the spec.

- UNVERIFIED: obtain the missing evidence and re-review; keep the ticket open.
- Findings: fix them, then call the Skill tool with "review" again. Three rounds at most; findings still open after the third go to the user as-is.
- PASS, run from `/implement`: ask one question, discuss-style — close the ticket now, or try it manually first. Manual: give a short guide for the remaining checks and wait for the user's result; keep the ticket `in-progress`. Fix reported failures and re-review. Close only after the user confirms the manual result, or chooses closure after the required verification has passed. Ticket to `done` (GitHub: close the issue); retain the spec, tickets, kickoff documents, baselines, and evidence per MODES.md.
- PASS, run from `/implement-all`: close the same way, without asking; the batch isn't interrupted per ticket. Count it towards the batch's final report.
- Report done: what was built, how it was verified, and anything the user should know. `implement-all`'s final report additionally states how many tickets in the batch closed without a manual sign-off.

Commit only when the user or the calling skill asks.
