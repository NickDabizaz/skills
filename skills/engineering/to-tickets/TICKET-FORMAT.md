# Ticket contract

Split one approved issue spec into work-owned tickets: backend, frontend, infrastructure, testing, or another necessary work type. Do not create a type with no work. Each ticket has a checkable outcome and fits one focused execution run. Dependencies are a directed acyclic graph; do not list a convenient ordering as a blocker unless the output is actually required.

Local path: `.workspace/issues/<issue-slug>/tickets/<nn>-<slug>.md`, one ticket per file. With GitHub, each ticket is a child or linked issue on GitHub; `.workspace/issues/<issue-slug>/tickets/README.md` contains links only.

```md
---
id: <local number or GitHub issue number>
title: <imperative outcome>
kind: backend | frontend | infrastructure | testing | other
status: ready | in-progress | review | awaiting-user | done
blocked-by: []
owner: <person or agent, if assigned>
---

## Outcome
<What this work delivers and how it serves the parent spec.>

## Contract
<Relevant API/data/UI/infra details from the spec, or a direct link to their authoritative section. For frontend include the approved prototype baseline, screen states, and viewports when applicable.>

## Acceptance criteria
- [ ] Given <state>, when <action>, then <observable result>.

## Work and checks
- [ ] <Concrete step>. Done when <verifiable condition>.

## Test scenarios
<The spec scenarios this ticket owns, including data, action, expected result, level, and evidence. State the user's automation choice.>

## Dependencies and handoff
<Blocked-by ids; outputs the next ticket needs; any manual action or permission required.>
```

Every spec criterion has an owner ticket; one criterion can appear in several tickets only when each owns a distinct layer-specific check. A testing ticket covers cross-layer or chosen automation work that implementation tickets do not own. A frontend ticket carries its own functional checks even if browser automation was declined. Mark blockers complete only on evidence, and leave a ticket open while user manual acceptance is pending.
