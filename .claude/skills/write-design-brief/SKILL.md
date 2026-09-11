---
name: write-design-brief
description: "Interview the user about pages, features per page, components, and typography direction from .workspace/PRD.md, then write .workspace/DESIGN_BRIEF.md — the reference for /prototype or an outsourced UI/UX team."
disable-model-invocation: true
---

No `.workspace/PRD.md` ([PRD-FORMAT.md](../setup-new-project/PRD-FORMAT.md)): stop and tell the user to run `/setup-new-project` (the PRD-driven kickoff option) first. There is no product to brief without it.

## Interview

Call the Skill tool with "discussing". The plan being settled is the content of [DESIGN_BRIEF-FORMAT.md](DESIGN_BRIEF-FORMAT.md), read against `.workspace/PRD.md`'s features; decisions the PRD already states are not asked:

- Pages: one per distinct screen the user reaches, each with the PRD features it carries.
- Components: what each page needs, named once even when several pages share it.
- Typography direction: a mood or a reference product, not a full type scale — `DESIGN.md`'s style preset covers that.

## Write

`.workspace/DESIGN_BRIEF.md` per [DESIGN_BRIEF-FORMAT.md](DESIGN_BRIEF-FORMAT.md). If the file exists, read it first and continue from it instead of starting over.

## Done when

Every page in the brief traces to a PRD feature and the user has confirmed it. Then tell the user the two ways on: `/prototype` for each page, to build the UI/UX in this session, or hand `.workspace/DESIGN_BRIEF.md` to an outsourced UI/UX team and come back to `/discuss-with-docs` once the design exists. Stop.
