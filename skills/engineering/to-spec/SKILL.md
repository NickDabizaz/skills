---
name: to-spec
description: "Turns an already settled conversation or plan into a detailed spec for one small issue without repeating the interview."
argument-hint: "<agreed change or source>"
disable-model-invocation: true
---

# To Spec

Read [SPEC-FORMAT.md](SPEC-FORMAT.md), `CONTEXT.md`, and the relevant project, domain, design, and existing issue material. Use only decisions established by the conversation or source; if a choice would change behavior, ask for it rather than fabricate it. A single issue should have an observable outcome and fit a small part of a module; split an oversized proposal into linked issues before writing deep specs.

For backend work always offer unit tests and record the user's yes/no answer. For frontend work always offer browser automation with concrete use cases and record the answer; Playwright may be recommended. Define scenario setup, action, expected result, level, and evidence before tickets. Include detailed UI pages/states and API endpoints only where the issue touches them. Write the spec in the user's input language under `.workspace/issues/<issue-slug>/spec.md`. If GitHub is the configured tracker, create or update the parent issue and link it from the spec.

Done when each acceptance criterion has a scenario or manual check, the technical contract is detailed enough to split work, and test choices are explicit. Offer `to-design-brief` for a requested UI prototype; otherwise offer `to-tickets`.
