---
name: grill-with-docs
description: "Interviews the user while updating project context and writes a complete issue spec when the decisions are settled."
argument-hint: "<issue or change>"
disable-model-invocation: true
---

# Grill With Docs

Read `CONTEXT.md`, relevant `.workspace/` docs, and [SPEC-FORMAT.md](../to-spec/SPEC-FORMAT.md). Call `grilling` to resolve behavior, scope, technical contract, and test decisions. Call `domain-modeling` when terminology, invariants, or durable decisions change; update the relevant shared document as each decision settles. Do not create the issue spec while a decision that changes behavior or testing remains open.

Write `.workspace/issues/<issue-slug>/spec.md` in the user's input language using the shared spec format. The issue must represent one small observable part of a module. For GitHub, create or update the parent issue and record its URL in the spec; for a local tracker, the folder is the issue. Preserve existing issue content when resuming rather than replacing it.

Done when the spec's criteria, technical details, and scenarios are independently checkable and every backend unit-test or frontend browser-test choice has an explicit answer. For UI whose layout needs a requested prototype, offer `to-design-brief`; otherwise offer `to-tickets`.
