---
name: ask-me
description: Routes your situation to the right skill in this package, and answers setup and troubleshooting questions. Use when you are unsure where to start, what comes next, or how a skill fits.
---

# Ask Me

Read the project context and any workspace state that exists, then recommend one next action and why. Do not run it on the user's behalf. When there is no decision to make, name the direct next skill.

## Route by situation

| Situation | Next skill |
| --- | --- |
| A new project, or a repo with no project context, or a change to the project foundation | `setup` |
| A complete project description you want run end to end, with the agent as PM and the human at only the spec and deploy gates | `ship-project` |
| An unclear idea or change, no document requested | `grilling` (or `grill-me` for a quick pass) |
| An unclear issue that should be documented while you talk | `grill-with-docs` |
| An incoming issue that needs classification or more information | `triage` |
| A clear plan or a settled conversation that needs a spec | `to-spec` |
| An approved spec that needs work items | `to-tickets` |
| An approved UI spec that needs a design brief | `design-brief` |
| A design brief or spec that needs a prototype | `prototype` |
| A ready ticket that needs execution | `head-chef` |
| A suspected bug without a verified cause | `diagnosing-bugs` |
| You want to understand how something works, or why it is built that way | `how` / `why` |
| You want to be taught until you understand | `teach` |
| An existing change needs a review | `code-review` |
| A UI or its motion needs a craft review | `design-review` |
| You want to resume or pick up earlier work | `recall` |
| No clear next step | start with `grilling` and settle the goal first |

## How to answer

- Recommend one next skill, with its exact input (an issue, a spec, a ticket, a path).
- Name the reason in one line. If there is a blocker, name the blocker instead of a skill.
- Do not run a user-invoked skill for the user. Offer it and stop.

Done when the user knows the single next action.
