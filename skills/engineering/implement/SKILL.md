---
name: implement
description: "Implements one ready ticket or a sequence of ready tickets, verifies the agreed scenarios, and reviews each ticket before closure."
argument-hint: "<ticket or issue>"
disable-model-invocation: true
---

# Implement

Read `CONTEXT.md`, the parent spec, ticket contract, relevant project/design/domain docs, and existing code. Accept one ticket or all ready tickets in an issue; follow actual blockers and keep each ticket's state current. On a mismatch between plan and code, surface the decision rather than quietly widening scope. Implement the smallest change that satisfies the ticket, reusing existing code and native features first.

Use `tdd` when automated tests were selected for the ticket, at the seam agreed in the spec. If automation was declined, perform the manual or traced checks the spec names. Run relevant project checks. For UI with an approved prototype, compare the agreed screen states and viewports against its baseline; record deviations only when the user requests them. Call `code-review` for every implementation ticket; repair actionable findings and rerun affected checks before marking it done.

When all tickets in an issue are done, call `code-review` at issue scope. For frontend, provide a step-by-step manual evaluation guide with page, action, expected result, and prototype comparison, then keep the issue `awaiting-user` until the user approves. Record evidence and completion in the configured tracker. Do not commit or push unless the user asks.

Done when accepted tickets satisfy their checks and review, and the issue's manual gate has the required user result. Offer `find-ready-tickets` for remaining work or `to-spec` for the next clear issue.
