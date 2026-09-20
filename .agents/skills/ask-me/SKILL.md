---
name: ask-me
description: "Which skill fits the situation. Describe what you are facing and get pointed at the right skill, with the reason."
argument-hint: "<what you are facing right now>"
disable-model-invocation: true
---

Route the user to the one skill that fits their situation. Point, never fire: the skills below are the user's to type.

## Routes

| Situation | Skill | Why |
| --- | --- | --- |
| An empty repo, or one that already has code (an old personal project), that should become an own project; or an own project missing `CONTEXT.md`, `DESIGN.md`, `CLAUDE.md` / `AGENTS.md`, or a ticket backend | `/setup-project` | Empty repo: interviews once, with an optional PRD-driven kickoff first for a brand-new product. Existing code: reads stack, commands, conventions, domain, and tests from it, asks only what the code cannot say. Either way, writes the same documents and keeps them out of git; run again, it adds only what is missing. |
| A whole codebase, or one area, should be looked at for what to improve: readability, architecture, efficiency, current practice | `/audit` | Reads it all, writes an HTML report in your language with code, options, and trade-offs per finding, plus a spec `/write-tickets` can split. Reports; never edits. |
| A raw idea with no shape yet: you do not know whether it should be a feature, something else, or worth doing at all | `/brainstorm` | Widens instead of narrowing: three concrete directions a round until one has who it is for, the problem, and a smallest useful version. Lands in `.workspace/<issue-name>/ideas.md`. |
| A change you already know you want, whose requirements are not yet clear; a ticket pasted from a tracker | `/discuss` | Narrows what you already have, one question at a time, before anything is built. |
| Same, but the work is large, spans sessions, or should leave a written spec | `/discuss-with-docs` | Same interview; the plan lands in `.workspace/<issue-name>/spec.md` for tickets, later sessions, and review. |
| `.workspace/PRD.md` exists and its pages, features, components, and typography direction should be written down — to build UI/UX yourself or hand off to an outsourced team | `/write-design-brief` | Interviews the PRD's features into `.workspace/DESIGN_BRIEF.md`: pages, components, typography direction. `/prototype` and `designing` read it. |
| A supplied HTML/CSS or JPG/PNG design to reproduce, a page or flow to explore, or an existing page to refine | `/prototype` | Reproduces supplied designs 1:1 by default; offers alternatives or redesign only when requested. Keeps an approved baseline and render evidence for implementation. |
| A bug whose cause is not yet known | `/investigate` | Reproduces it, proves the cause with evidence, then routes the fix to a ticket or to implement. |
| An issue or PR that arrived from outside and needs sorting before anyone builds anything | `/triage` | Categorises it, verifies it holds up, asks the reporter when information is missing, then routes it to investigate, discuss, write-tickets, or rejects it with a reason. |
| A library or technology to choose or adopt, whose answer is outside the repo: what it is, what supports it, where the docs are, how it is best used | `/research` | Sweeps the docs, the issue tracker, the community, and your own code at once, narrows to candidates you approve, digs into each, and proves the claim the recommendation rests on with a real spike. Lands in `.workspace/<issue-name>/research.md`. |
| A bug still unexplained after `/investigate`, or a problem someone outside has almost certainly hit already | `/research` | The same sweep in problem mode: candidate causes and fixes from outside, each checked against your symptom and the versions you actually pin before any of them is recommended. |
| A spec exists in an own project, or an audit spec anywhere, and should become tickets | `/write-tickets` | One ticket per unit of work, with criteria, checklist, and what blocks it; you pick all or some; beside the spec or as GitHub Issues. |
| Tickets already exist somewhere (or in GitHub Issues) and you want to know what is ready to build right now, without opening each one | `/find-ready-tickets` | Scans every spec's tickets, reports which are open with every blocker done, and gives the exact `/implement` or `/implement-all` command. |
| One ticket (`.workspace/<issue-name>/tickets/<nn>-<slug>.md` or an issue number), or a plan in the conversation, should now be built | `/implement` | Builds it on the current branch with the mode's verification, and hands off to review by itself. |
| Every open ticket of a spec should be built | `/implement-all` | Parallel where nothing blocks, one branch each, merged into a target branch, reviewed as a whole against the spec. |
| A merge or rebase stopped on conflicts | `resolve-merge-conflicts` | Resolves by the spec and both tickets; asks when neither decides. Called by implement-all, or by you. |
| Code has changed and should be checked against the plan, the codebase's conventions, for bugs or security holes, and for unneeded complexity | `review` | Reports on Spec, Standards, Logic & Security, Simplicity; touches nothing. |
| Curious what got deliberately simplified along the way, whether any of it is at risk of being forgotten, or want a check before a release | `find-shortcuts` | Greps every `shortcut:` marker `implement` left in the code into a ledger, flags the ones with no revisit trigger. Reads and reports only; callable directly. |
| `DESIGN.md` should be written or completed for an own project | `designing` | Interviews a new project or extracts tokens, patterns, and components from existing code. Called by setup-project and discussing. |
| A domain term is fuzzy, or a decision just made is hard to reverse and worth recording | `domain-modeling` | Sharpens the term into `CONTEXT.md`'s Domain section, or records the decision to `DECISIONS.md`. Called by discussing, implementing, investigate, and prototype; callable directly. |
| Writing or editing a skill, `CLAUDE.md`, `AGENTS.md`, `CONTEXT.md`, or `DESIGN.md` | `writing-for-agents` | The pruning and structure rules every document here follows. |

Every new skill added to the set gets a row here.

## How to answer

1. If the user described their situation, match it to one row. Reply with the skill, the reason, and the exact thing to type. When two rows fit, name both and say what decides between them.
2. If the description does not match a row, say so plainly. Then say whether ordinary prompting covers it, or whether it is a recurring situation worth a supporting skill; for the latter, point at `writing-for-agents`.
3. If nothing was described, ask one question with two to four options and a recommendation, discuss-style, then route.

Reply in the user's language. One short answer; the user came here to be pointed somewhere, not briefed.
