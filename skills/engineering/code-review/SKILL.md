---
name: code-review
description: "Reviews an implementation ticket or completed issue against its spec, design baseline, tests, and repository conventions."
---

# Code Review

At ticket scope, read the parent spec, ticket, relevant project and design docs, and the full diff including affected callers. Check: spec coverage and acceptance evidence; consistency with existing code; logic, security, data and error paths; simplicity and unnecessary dependencies; test choice and scenario coverage. For UI, check each agreed state and viewport against the approved prototype when one exists, plus accessibility and visible feedback. Report actionable findings with location, impact, and a concrete correction; distinguish unverified behavior from a confirmed bug. A pass requires evidence, not absence of findings.

At issue scope, check cross-ticket integration, migration/infra consistency, every spec criterion and scenario, and that all ticket reviews passed. For frontend, prepare the final step-by-step manual evaluation guide: route/page, setup, action, expected result, and prototype comparison. Keep the issue `awaiting-user` until the user reports acceptance; record failures as work to repair and re-review. For backend-only issues, finish when the agreed checks and review pass.

Done when findings are resolved or explicitly reported and the review state is recorded in the configured tracker. Offer `implement` for fixes, `find-ready-tickets` for remaining tickets, or the manual evaluation step when user sign-off is due.
