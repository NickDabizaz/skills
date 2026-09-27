---
name: grill-me
description: "Interviews the user until a project change or issue is clear enough to specify, keeping the result in the conversation."
argument-hint: "<idea or change>"
disable-model-invocation: true
---

# Grill Me

Call `grilling` on the supplied idea and current project context. Keep decisions and their reasons in the conversation; do not write files. Present the settled behavior, boundaries, test choices, and remaining out-of-scope work in the user's language.

Done when no open decision would change the issue spec. Offer `to-spec` with the settled conversation as input. If the user wants decisions captured during the interview, offer `grill-with-docs` for the next issue rather than duplicating this interview.
