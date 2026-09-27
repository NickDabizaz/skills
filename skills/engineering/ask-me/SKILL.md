---
name: ask-me
description: "Routes a user's engineering situation to the next skill in this package. Use when they are unsure where to start or what follows."
argument-hint: "<your situation>"
disable-model-invocation: true
---

# Ask Me

Read `CONTEXT.md` and the relevant `.workspace/` issue state when present. Recommend one next action and why; do not run it on the user's behalf. If there is no decision to make, name the direct next skill.

| Situation | Next skill |
| --- | --- |
| New project, existing repo without project context, or architecture change | `plan-project` |
| Unclear need, no document requested | `grill-me` |
| Unclear issue that should be documented while discussing | `grill-with-docs` |
| Incoming issue needs classification or more information | `triage` |
| Clear conversation or plan needs an issue spec | `to-spec` |
| Approved UI spec needs a requested prototype | `to-design-brief` |
| Approved spec needs work items | `to-tickets` |
| Need to see unblocked work | `find-ready-tickets` |
| Ready ticket needs execution | `implement` |
| Suspected bug lacks a verified cause | `diagnosing-bugs` |
| Existing change needs a review | `code-review` |

`design-system` creates UI rules before a design brief; `prototype` uses an approved brief; `domain-modeling`, `grilling`, and `tdd` are supporting skills reached from the main flow. End by offering the selected next skill with its exact input (issue, spec, or ticket). When no next action exists, say what is complete.
