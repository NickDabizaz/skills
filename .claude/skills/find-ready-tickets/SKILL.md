---
name: find-ready-tickets
description: "Scan every spec's tickets, or GitHub Issues, for the ones open with every blocker already done, and recommend /implement or /implement-all for what it finds."
argument-hint: "[issue-name]"
disable-model-invocation: true
---

Own projects, plus GitHub Issues in a legacy repo carrying an `issue:` label. Reports only; nothing is built or edited.

## Scan

Backend: `CONTEXT.md`'s `backend` line in an own project; legacy has only `audit` tickets, backend whichever evidence exists (`.workspace/audit/tickets/` locally, or an open issue labelled `issue:audit`).

- **local**: `.workspace/<issue-name>/tickets/*.md` for the issue-name the argument names, else every one under `.workspace/`. Read each ticket's `status` and `blocked-by`.
- **github**: `gh issue list --state open --label issue:<issue-name>` for the argument's issue-name, else `gh issue list --state open` grouped by each issue's `issue:` label. Read each one's body for its `blocked-by`.

Ready = `status: todo` (GitHub: open, not `in-progress`) and every id in `blocked-by` is `done` (GitHub: closed) — `blocked-by` ids are scoped to their own issue-name; one pointing outside it is a split error `write-tickets` would have caught, not this skill's job.

## Report

One line per ready ticket, grouped by issue-name: id, title, type. Nothing ready anywhere: say so, plainly.

Then, for what is ready: one ticket, `/implement <path or issue number>`; more than one ready ticket in the same issue-name, `/implement-all .workspace/<issue-name>/spec.md`.

## Done when

Every open ticket in scope is accounted for as ready, or blocked and by what, and the recommendation is one command the user can paste as-is. Stop.
