---
name: design-review
description: Review UI and motion against a high craft bar, find missing motion, audit a whole codebase and plan fixes, or stress-test a component with worst-case data. Use when reviewing a brief, a prototype, or shipped UI, or when asked to improve how something feels. Read-only unless asked to fix.
---

# Design Review

Use to assess design quality: motion, craft, and robustness. Read-only by default; fix only when asked. The bar comes from the design principles in this package; the precise values live in [references/standards.md](references/standards.md).

Pick a mode from the request, or ask when it is ambiguous.

## Mode: review (default)

Review the motion and UI craft of a diff, a prototype, or a component against `principle-motion-decision`, `principle-ui-craft`, and `principle-fluid-interfaces`. Bias toward flagging; approval is earned.

Output two parts, in order.

**Findings table.** One row per issue, never a Before/After list.

| Before | After | Why |
| --- | --- | --- |

**Verdict.** Group the rest by impact, highest first: feel-breaking regressions; motion that should be removed; performance; interruptibility and timing; origin and cohesion; accessibility. Close with an explicit **Block** or **Approve**. Cite `file:line`.

## Mode: opportunities

Search a UI for places that do not animate but should, and reject everything that should not. Restraint is the point: expect to reject most candidates. Cap at five to seven suggestions for a whole app.

Every candidate must pass four questions, in order: **frequency** (keyboard or 100+ per day actions never animate), **purpose** (name it: feedback, spatial consistency, state indication, preventing a jarring change, explanation, or delight at the rare tier only), **speed** (fits the budget, UI under 300ms), and **function** (motion that aids, not decorates). Record each answer.

Output: an opportunities table ordered by leverage with exact values, a **rejected candidates** list with the gate question that killed each, and a one-paragraph verdict. If nothing survives, say so; that is a good result.

## Mode: audit

Survey a codebase's motion as a senior advisor, then produce a prioritized audit and self-contained plans for other agents to execute. Recon first (stack, motion libraries, tokens, personality, frequency map), audit in parallel across categories, vet every finding at its `file:line`, then stop and let the user choose which become plans. Write one plan per choice, with exact values and a feel-check step. Read-only on source; plans live in a plans directory.

## Mode: stress

Try to break a piece of UI with the realistic worst case of every value it renders, then show both datasets behind a **Demo data / Worst case** toggle and report what broke. Change the data, not the component. Values must be plausible or schema-backed, never random noise. Cover empty, one, and huge as separate toggle states. Read [references/catalog.md](references/catalog.md) for the failure catalog.

Output: **What broke** (one row per break, worst first, severity Broken / Ugly / Fragile), **Decisions for you** (breaks with more than one right answer), and **What held up**. Leave the toggle running, dev-only. Say `fix all` or `fix 1, 3` to apply fixes.

Done when the findings are specific, cited, and honest about what could not be judged from code alone.
