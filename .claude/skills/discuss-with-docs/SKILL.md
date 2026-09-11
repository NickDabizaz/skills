---
name: discuss-with-docs
description: "Interview the user one question at a time until the intent and context behind a task are settled, then write the plan to .workspace/<issue-name>/spec.md. When .workspace/PRD.md exists, offers an API requirement step first and covers the PRD's full scope."
argument-hint: "<what you want to build or change>"
disable-model-invocation: true
---

`.workspace/PRD.md` ([PRD-FORMAT.md](../setup-new-project/PRD-FORMAT.md)) exists and no `.workspace/*/spec.md` yet links it: this is the PRD-driven kickoff's first run, and the interview below covers the PRD's full scope rather than one narrow feature. `.workspace/API_REQUIREMENT.md` not written yet: one question first, skippable, to write it (endpoints, auth, data contracts, in [API_REQUIREMENT-FORMAT.md](API_REQUIREMENT-FORMAT.md)) from `.workspace/PRD.md`, `.workspace/DESIGN_BRIEF.md` ([DESIGN_BRIEF-FORMAT.md](../write-design-brief/DESIGN_BRIEF-FORMAT.md)) when it exists, and whatever UI/UX now exists. A later run, once some spec already links `.workspace/PRD.md`: this is an unrelated feature, not the kickoff — skip this paragraph entirely, even while `.workspace/PRD.md` still exists.

Call the Skill tool with "discussing".

Once the user confirms the plan, write it to `.workspace/<issue-name>/spec.md` in the format in [SPEC-FORMAT.md](SPEC-FORMAT.md). `<issue-name>` is a short kebab-case name for the work. Create the folder if it is missing; if the file already exists, read it before the first question and continue from it instead of starting over. This is the kickoff spec (the case above): the goal links `.workspace/PRD.md`, and `.workspace/DESIGN_BRIEF.md` / `.workspace/API_REQUIREMENT.md` when they exist too — completing it deletes all three. This file is the only thing written to disk. Legacy ([MODES.md](../implementing/MODES.md)): when `.workspace/` is not ignored, add it to `.git/info/exclude`, which stays local, so the spec never reaches the remote.

The next step to name, with the spec path: own project, `/write-tickets`; legacy, `/implement`.
