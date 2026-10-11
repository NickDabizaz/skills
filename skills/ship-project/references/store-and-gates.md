# Store and gates

## The store

Create `.workspace/project/<slug>/`. Slug is lower kebab-case English. One writer per file.

| File | Writer | Holds |
| --- | --- | --- |
| `brief.md` | the conductor, Phase 0 | the description, the goal, the out-of-scope, the done predicate, the scope count |
| `assumptions.tsv` | the conductor, any phase | one row per recorded bet |
| `decisions.tsv` | `show-me-your-work` | the decision trail, that skill's format |
| `spec.md` | `to-spec`, Phase 2 | the approved spec |
| `tickets/` | `to-tickets`, Phase 3 | one file per ticket |
| `units.tsv` | the conductor, Phase 5 | ticket, state, branch, PR, head SHA, verdict |
| `ledger.tsv` | the verifier or the conductor | one verdict row per ticket, PR, and head SHA |
| `gates.md` | the conductor | the open human gates |
| `status.md` | derived | regenerated from `units.tsv` and `ledger.tsv`, never hand-written |

`assumptions.tsv` columns:

```
id	phase	assumption	why	confidence	impact_if_wrong	status
```

One row per decision the conductor had to make without a human. `status` is `open`, `confirmed`, or `superseded`. An assumption confirmed at a gate becomes a settled decision. It is not a deleted row.

`units.tsv` columns:

```
ticket	track	state	branch	pr	head_sha	verdict
```

`track` is `design` or `dev`. `state` is `blocked`, `ready`, `in-flight`, `merged`, or `abandoned`.

`status.md` is derived. Regenerate it from the tables at each drain. Do not narrate events into it.

## The gate format

A gate is the only place the conductor stops for a human. Park it in `gates.md` before asking, then ask.

```
GATE <n>: <title>

Question      one line
Options       each option, with its recommended default marked
Evidence      the artifact paths and the ledger rows that ground the options
If no answer  the default is taken and recorded; name it
Blocks        what waits, and what still proceeds in parallel
```

**Gate 1 is the spec.** It asks the human to confirm or correct the assumption ledger and the open decisions. Work that does not depend on the answer continues.

**Gate 2 is the deploy.** It offers the summary and the exact command the human runs.

## The summary format

Write the summary at close, from the store.

```
# <Project name>

## What it is
One paragraph a stranger understands, in the user's language.

## Features
One line each: what it does for the user, with its ticket and PR.

## How it works
The shape: the main surfaces, the data flow, the seams. Enough to navigate the code.

## What was verified
The predicate, how it was checked on the real artifact, the ledger rows, and any measured number with its evidence.

## Assumptions you should check first
The open and high-impact rows from `assumptions.tsv`, highest impact first.

## Decisions still open
Anything carried to this gate, each with its recommended default.

## Design direction
The chosen variant and the reason, so the human can override it.

## How to run and deploy
The exact commands. The deploy is `ship`, run by the human.
```
