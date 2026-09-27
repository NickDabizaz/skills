# Issue spec

Path: `.workspace/issues/<issue-slug>/spec.md`. One issue describes a small, observable part of a module, not an entire large module. Write prose in the user's input language; keep identifiers and paths in English.

```md
---
title: <outcome>
status: needs-info | ready | in-progress | review | awaiting-user | done
blocked-by: []
tracker: local | github
tracker-url: <GitHub parent issue URL, if applicable>
---

# <Outcome>

## Goal and scope
<Who needs what, why, what the completed issue visibly or technically delivers, and what is excluded.>

## Domain and decisions
<Actors, entities, invariants, changed rules, and the reason for each consequential choice. Link to shared DOMAIN.md.>

## Behavior and flows
<Trigger, preconditions, success, failure, permissions, edge cases, and recovery. For UI: route, entry point, navigation, fields, actions, feedback, empty/loading/error/success states, accessibility and responsive expectations.>

## Technical contract
<Affected apps and modules, data/schema/migration changes, API endpoint method/path/auth/request/response/errors, integration points, infra, and compatibility. Mark a section not applicable instead of inventing work.>

## Design reference
<DESIGN.md, approved design brief/prototype path and version if one exists, screens/viewports/states to match, agreed deviations.>

## Test decision and scenarios
<Record the user's explicit yes/no answer to backend unit tests when backend work exists, and frontend browser automation when frontend work exists. Offer browser automation with concrete use cases; Playwright is a recommendation, not a requirement. For every scenario list setup/data, action, expected observable result, test level (unit/browser/integration/manual), owner, and evidence. Record any chosen automated-test seam and what will remain manual.>

## Manual acceptance
<For frontend, draft the steps the user will perform: page, input/action, expected result, and what to compare with the approved prototype if present. Final guide is refined after implementation.>

## Acceptance criteria
- [ ] Given <state>, when <one action>, then <one observable result>.

## Dependencies and out of scope
<Blocking issues and exclusions.>
```

Resolve decisions that affect behavior or the test plan before setting `ready`. Each acceptance criterion must map to at least one test scenario or manual check. The spec is authoritative over its tickets; when an approved prototype changes it, reconcile the spec and open tickets before implementation. Retain the spec and evidence after completion.
