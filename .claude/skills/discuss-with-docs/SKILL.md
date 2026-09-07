---
name: discuss-with-docs
description: "Interview the user one question at a time until the intent and context behind a task are settled, then write the plan to .issues/<issue-name>/spec.md."
argument-hint: "<what you want to build or change>"
disable-model-invocation: true
---

Call the Skill tool with "discussing".

Once the user confirms the plan, write it to `.issues/<issue-name>/spec.md` in the format in [SPEC-FORMAT.md](SPEC-FORMAT.md). `<issue-name>` is a short kebab-case name for the work. Create the folder if it is missing; if the file already exists, read it before the first question and continue from it instead of starting over. This file is the only thing written to disk. Legacy ([MODES.md](../implementing/MODES.md)): when `.issues/` is not ignored, add it to `.git/info/exclude`, which stays local, so the spec never reaches the remote.

The next step to name, with the spec path: own project, `/write-tickets`; legacy, `/implement`.
