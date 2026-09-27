---
name: diagnosing-bugs
description: "Reproduces a reported bug, traces the shared cause and affected callers, and supplies evidence for a small corrective issue."
---

# Diagnosing Bugs

Read the report, project context, and relevant code. Reproduce the failure or record exactly why reproduction is unavailable. Trace the failing path and all callers of the likely shared function, endpoint, or schema. Form a falsifiable cause, check it against evidence, and distinguish cause from symptom. Identify the narrowest safe correction and a regression scenario, respecting the user's chosen test level.

Do not implement unless the user asked for a fix or the calling workflow includes it. Done when the cause is supported by a reproduction or clear code evidence, affected paths are named, and a scenario would fail before the correction. Offer `grill-with-docs` if behavior is still ambiguous, or `to-spec` to capture the verified fix.
