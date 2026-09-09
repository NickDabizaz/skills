# Spec format

Path: `.issues/<issue-name>/spec.md`; its tickets sit in `.issues/<issue-name>/tickets/`. Discuss-with-docs writes it once the plan is confirmed, audit writes one from its findings, write-tickets writes one from an investigate report and splits any of them into tickets in an own project; implement builds from it or from its tickets; review checks the diff against it.

```md
# <Title>

## Goal

One paragraph: the problem and the outcome, in the user's words where possible.

## Decisions

- **<Decision>**: <choice>. Why: <reason>.

## UX flow

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

- One decision per settled question, each with its reason. A decision without a reason cannot be revisited later.
- No code snippets and no file paths, unless the decision is about that file or the path is the investigate report the goal links. Both go stale fast.
- A spec written from an `investigate` report ends its goal with a link to the `report.md` beside it. The evidence, the ruled-out candidates and the reproduction steps stay in the report; the spec never copies them.
- UX flow only when the work touches UI; otherwise the section is absent. Each state it names is also an acceptance criterion.
- Acceptance criteria are checkable by someone who did not attend the discussion, and each one becomes a test in an own project: one state, one action, one observable result per line.
- There is no "Open questions" section. An open question means discuss is not done.
- The spec is the reference for its tickets. It stays until every ticket is done; implement deletes the whole `.issues/<issue-name>/` folder then.
