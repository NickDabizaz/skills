---
name: triage
description: "Move an issue or PR that arrived from outside through triage: categorise it, verify it holds up, ask back when information is missing, then route it to /investigate, /discuss, /write-tickets, or reject it with a reason."
argument-hint: "<the issue number, PR number, or pasted report>"
disable-model-invocation: true
---

Triaging decides whether an incoming report is real, ready, and in scope — it never fixes and never writes tickets itself. Facts are yours to find; the reporter answers only what the repo cannot.

## Read

Resolve what was given: a bare `#42` against the ticket backend `CONTEXT.md` names (`gh issue view` / `gh pr view` when `backend: github`), or the pasted text itself. A PR is an issue with attached code: read the diff too, and whether it matches what it claims to fix.

## Categorise

One of: **bug** (the code already behaves differently from what is claimed), **feature** (something new), **question** (answerable without a change), **duplicate** (an existing ticket, issue, or PR already covers it), **out of scope** (declared out of scope elsewhere, or not this project's problem).

## Verify

Bug: reproduce it the way `/investigate` does, or say plainly why it would not reproduce. Feature: check it is not already possible some other way. Missing the piece needed to decide either way: ask the reporter one question, discuss-style, for the smallest missing piece, then stop and wait — never guess at what only the reporter knows.

## Route

- **Ready for a ticket**: categorised, verified, in scope. Own project: tell the user to run `/write-tickets`. Legacy: say it is ready for their tracker.
- **Needs a deeper look**: a bug not yet explained. Tell the user to run `/investigate`.
- **Needs a decision first**: a feature whose shape is still open. Tell the user to run `/discuss` or `/discuss-with-docs`.
- **Rejected**: duplicate or out of scope. State the reason, and the issue, ticket, or PR it duplicates when there is one.

Posting the route back onto the issue or PR is visible to whoever else watches it: state the comment you would post and ask before running `gh issue comment` or `gh pr comment`.

Nothing is written before the route is chosen.

Stop.
