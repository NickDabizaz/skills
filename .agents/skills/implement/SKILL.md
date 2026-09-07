---
name: implement
description: "Build one ticket, a spec, or the plan agreed in the conversation on the current branch, then hand the result to review."
argument-hint: "[ticket path or issue number, or path to .issues/<issue-name>/spec.md]"
disable-model-invocation: true
---

Call the Skill tool with "implementing", passing what the user passed. Work on the current branch. Commit only when the user asks.
