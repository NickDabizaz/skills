---
name: tdd
description: "Applies a failing-test, passing-code, tidy loop to automated scenarios the user selected in an issue spec."
---

# TDD

Read the selected automated scenarios and their agreed test seam in `spec.md` and the owning ticket. Use existing test tools; add a dependency only when the chosen browser or unit scenario cannot be verified with what the project already has. For a backend unit or frontend browser scenario, write the smallest test that fails for the intended behavior, confirm that failure, implement until it passes, then tidy without changing behavior. Keep browser tests tied to user-visible use cases and stable selectors; do not assert incidental markup.

Record what was run and the result on the ticket. If the user declined automated tests for that work type, return control to `implement` without creating them. Done when every selected scenario assigned to this ticket passes and failures elsewhere are reported. Offer `code-review` after implementation checks are complete.
