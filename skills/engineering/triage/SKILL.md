---
name: triage
description: "Classifies an incoming issue, verifies its claim against the repository, and decides what information is needed before specification."
argument-hint: "<issue path or URL>"
disable-model-invocation: true
---

# Triage

Read `CONTEXT.md` for the tracker backend, then the full issue and relevant repository code. Identify whether it is a bug, enhancement, or already delivered behavior. For a bug, call `diagnosing-bugs` when reproduction or cause is uncertain. Record evidence and missing decisions; do not infer a feature from a vague report.

Use `needs-info` when the reporter must answer a specific question, `ready` when the issue can be specified, and `done` only when the requested outcome was verified. Keep blocking dependencies separate from state. For GitHub, update the issue's native status and labels; for local, update its Markdown frontmatter. Avoid posting to external contributors without the user's authorization.

Done when category, evidence, state, and next action are clear. Offer `grill-with-docs` if decisions remain, `to-spec` if the request is already clear, or `diagnosing-bugs` if the failure still needs a cause.
