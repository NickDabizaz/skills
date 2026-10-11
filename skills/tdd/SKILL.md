---
name: tdd
description: Test-driven development done well. A red-green loop for features at agreed seams, and a regression-first loop for bugs. Use when the user asks for TDD, a failing test, or a regression test, or when the change has an obvious cheap local test target.
---

# TDD

Build behavior test-first. The goal is a test that fails before the change and passes after it, at a seam that survives refactoring.

## Two loops

**Feature loop (red, green, tidy).**

1. Agree the seams first. A seam is where a test calls the code through its public interface. Prefer existing seams, the highest one that still isolates the behavior, and ideally one seam for the change. Confirm the seam with the user in one line before writing a test.
2. Write the smallest failing test for the next behavior slice. The test encodes intended behavior, not the current implementation.
3. Run it and confirm it fails for the intended reason.
4. Write the smallest production change that makes it pass.
5. Tidy without changing behavior. Refactoring for its own sake belongs to review, not the loop.
6. Repeat for the next slice, one vertical slice at a time.

**Bug loop (regression first).**

1. Understand the bug: intended behavior, current behavior, affected path, smallest observable reproduction.
2. Choose the narrowest executable check already used for that code path.
3. Write the failing test first, encoding intended behavior.
4. Run it before fixing and confirm it fails for the intended reason. If it passes or fails for an unrelated reason, fix the test first.
5. Make the smallest production fix.
6. Rerun to green.

## When a failing test is impractical

If the only test would need broad harness setup, brittle mocks, slow end-to-end infrastructure, production-only state, a vague reproduction, or large unrelated fixture churn, skip the new test and use the closest executable regression check instead: a targeted script, a manual reproduction command, browser automation, a snapshot comparison, a log assertion, or a focused integration check. Prefer no new test over a bad test.

## Guardrails

- Test behavior through public interfaces. The `undefined` check: would the test still pass if every imported function returned `undefined`? If so, rewrite it.
- Do not change tests to match a wrong implementation.
- Do not weaken assertions unless the expected behavior genuinely changed, and say why.
- Keep the test focused on the change. No broad fixture churn.
- If the bug is flaky, make the test deterministic where possible and name the signal being locked down.
- If the bug exposes a broader class of failures, land the focused regression path first, then consider sibling coverage separately.

## Final response

Report the evidence, not just the outcome:

- The failing-before test or check, and the failure it produced.
- The passing-after run, and any nearby validation.
- If failing-before could not be shown, say why and name the closest check used instead.
