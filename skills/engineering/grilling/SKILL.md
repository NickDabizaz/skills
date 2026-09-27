---
name: grilling
description: "Runs the shared one-decision-at-a-time interview for unclear project plans, issue behavior, design, and test choices."
---

# Grilling

Read the user's request, `CONTEXT.md`, relevant `.workspace/` documents, and the code before the first question. Facts found there are not questions. Settle actors, activities, rules, and observable outcome before architecture or UI details. Ask one decision per turn in the user's language; offer two or three concrete options, mark a recommendation with its reason, and allow another answer. Stop and wait after each question. Recompute open decisions after each answer.

For UI, settle each page's entry point, content, actions, navigation, feedback, validation, empty/loading/error/success states, responsive behavior, and approved references. Offer a prototype when a new layout would benefit from one; never require it for a small visual adjustment. For backend, settle data invariants, endpoint contract, permissions, failures, and compatibility. Ask whether backend unit tests should be created whenever backend work exists. Ask whether frontend browser automation should be created whenever frontend work exists; recommend concrete use cases and a tool such as Playwright without making it compulsory. Resolve the test level, data, expected result, and manual fallback before ticketing.

End when no unanswered choice would change the spec, design brief, or test plan. Return a concise decision record with reasons and out-of-scope items to the calling skill. That skill writes documents if it owns them. Suggest its next user-facing skill rather than invoking another user-invoked skill.
