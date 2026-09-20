# Spec format

Path: `.workspace/<issue-name>/spec.md`; its tickets sit in `.workspace/<issue-name>/tickets/`. Discuss-with-docs writes it once the plan is confirmed, audit writes one from its findings, write-tickets writes one from an investigate or research report and splits any of them into tickets in an own project; implement builds from it or from its tickets; review checks the diff against it.

```md
# <Title>

## Goal

One paragraph: the problem and the outcome, in the user's words where possible.

## Actors & activities

- **<Actor>** (person or third-party system): <what it does>. Rules: <the constraints that govern it>.

## Decisions

- **<Decision>**: <choice>. Why: <reason>.

## Non-functional requirements

- <Target>: <measurable threshold>. Verified by: <how it's checked>.

## UX flow

- Baseline per screen: <approved reference/prototype path and version when one applies; viewports, states, and agreed deviations>
- Screen contract: <reconciled field/action inventory per FIDELITY.md; extract from the brief and approved prototype when present>
- **<Screen>**: entered from <where>. <Action> → <what the user sees on success> / <on failure>. Empty: <...>. Loading: <...>. Error: <...>. Success: <...>.

## Plan

1. <Step>. Done when: <checkable condition>.
2. ...

## Acceptance criteria

- [ ] Given <starting state>, when <action>, then <observable result>.

## Out of scope

- <What this work will not do>
```

Rules:

- Actors & activities only when the work defines a new application or feature (per `discussing`); otherwise the section is absent, same condition as UX flow's UI-only one.
- Non-functional requirements only when `discussing` settled at least one target; "none" leaves the section absent, same condition as Actors & activities and UX flow. Each line is also a line in Acceptance criteria, phrased as Given/When/Then like any other.
- One decision per settled question, each with its reason. A decision without a reason cannot be revisited later. Own project with `tests: acceptance`: one decision named **Test seam** names the boundary every acceptance criterion below runs against.
- No code snippets and no file paths, unless the decision is about that file, the path is the investigate report the goal links, or it identifies the approved UI baseline, its assets, or verification evidence. All three go stale fast otherwise.
- A spec written from an `investigate` or `research` report ends its goal with a link to the `report.md` or `research.md` beside it. The evidence, the ruled-out candidates, the reproduction steps and the sources stay there; the spec never copies them.
- The PRD-driven kickoff's spec — the first one written while `.workspace/PRD.md` exists and before any spec links it — ends its goal with a link to it too, and to `.workspace/DESIGN_BRIEF.md` / `.workspace/API_REQUIREMENT.md` when they exist. A later spec written while `.workspace/PRD.md` still exists (whether its tickets are open or complete) is not the kickoff spec and never links it. Keep these linked records after completion ([MODES.md](../implementing/MODES.md)).
- UX flow only when the work touches UI; otherwise the section is absent. Each state it names is also an acceptance criterion.
- Acceptance criteria are checkable by someone who did not attend the discussion, and each one becomes a test in an own project: one state, one action, one observable result per line.
- There is no "Open questions" section. An open question means discuss is not done.
- The spec is the reference for its tickets, retained with them after completion per [MODES.md](../implementing/MODES.md).

UI with a reference follows [FIDELITY.md](../prototype/FIDELITY.md): acceptance criteria include the screen contract and verified render parity at the agreed viewports/states. A baseline is required whenever the user supplied or approved one, including images or HTML/CSS without a `/prototype` run. Revisions reconcile affected criteria and open tickets before the new baseline is used.
