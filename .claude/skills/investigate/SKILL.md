---
name: investigate
description: "Find the root cause of a bug with evidence before anything is fixed, then route the fix to a ticket or straight to implement."
argument-hint: "<the bug: symptom, where it shows, how to trigger it>"
disable-model-invocation: true
---

Investigating produces a proven cause and a fix plan; it never fixes. Facts are yours to find; the user answers only what the repo cannot.

## Reproduce

Read what the user wrote, `CLAUDE.md` / `AGENTS.md` and `CONTEXT.md` where present, then the code on the symptom's path. Trigger the bug yourself: a test, a script, a command. When it will not trigger, ask one question, discuss-style, for the missing piece (input, environment, steps). Done when the failure reproduces on demand.

## Find the cause

Trace from the symptom to the line that produces it: read the path, add logs or asserts, bisect inputs or commits. A hypothesis is confirmed only when changing that one thing changes the symptom; candidates ruled out are kept with the reason. Done when one cause is confirmed by evidence, not by plausibility. Every candidate ruled out and none confirmed: the evidence inside this repo is spent, so tell the user to run `/research` and stop.

Own project ([MODES.md](../implementing/MODES.md)): keep the reproduction as a failing test that names the cause. It is the first acceptance test of the fix.

## Report

- Symptom, reproduction steps, root cause (file, line, why), evidence, candidates ruled out.
- Every caller and path that goes through the same cause.
- Fix plan: steps with done-conditions, acceptance criteria as Given/When/Then, out of scope.

The report lives in the conversation; Route decides whether it is also written. Written, it is Markdown at `.workspace/<issue-name>/report.md`, and you name `<issue-name>` from the symptom; ask nothing. A folder of that name already there: reuse it when the report belongs to that work, otherwise extend the slug until the name is free. Legacy: add `.workspace/` to `.git/info/exclude` when it is not ignored.

## Route

One question, two options, discuss-style. The user's time decides; the size of the fix only sets the recommendation.

- **Fix it now**: the fix plan above is the plan in the conversation. Tell the user to run `/implement`. Recommended when the fix is one clear change.
- **Track it for later**: write the report. Own project: tell the user to run `/write-tickets`, which splits it into tickets. Legacy: the report is theirs to paste into their tracker, and `/discuss` settles the fix when they come back. Recommended when the cause spans several areas, carries a design decision, or is worth tracking.

Nothing is written before the answer.

Stop.
