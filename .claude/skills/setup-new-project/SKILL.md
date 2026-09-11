---
name: setup-new-project
description: "Make a repo an own project for this skill set: interview about domain, stack, conventions, design, and ticket backend, then write CONTEXT.md, DESIGN.md, and CLAUDE.md / AGENTS.md and keep them out of git. Offers a PRD-driven kickoff first for a brand-new product. Run again to add whatever is missing."
argument-hint: "<what the project is>"
disable-model-invocation: true
---

Writes documents only. The first code goes through `/discuss-with-docs` and `/implement`, so it is reviewed like everything after it.

Run on a repo that already has some of the files: read them, keep them, and produce only what is missing. A repo that already has code is `/setup-project`'s job.

## Kickoff

No `CONTEXT.md` yet: one question first, full PRD-driven kickoff or the quick setup below — recommended for a brand-new product with real UI/UX and an API surface; skip it for a script or small tool. Declining changes nothing below.

Accepting: call the Skill tool with "discussing" for [PRD-FORMAT.md](PRD-FORMAT.md) (vision, users, features, success criteria, out of scope) and write `.workspace/PRD.md`. Then continue below as usual.

## Interview

Call the Skill tool with "discussing". The plan being settled is the content of [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md); decisions the user already stated or the repo already shows are not asked:

- Purpose and users.
- Domain: the main entities, their relations, the invariants that must never break.
- Stack: language, framework, package manager, test runner, linter and formatter.
- Conventions no tool enforces: naming, layout, error handling, test style.
- Ticket backend: local `.workspace/<issue-name>/tickets/`, or GitHub Issues (needs `gh` authenticated).
- Instruction file: `CLAUDE.md`, `AGENTS.md`, or both.

The next step discussing names once the plan is confirmed is `/discuss-with-docs` for the first feature.

## Write

1. `CONTEXT.md` per [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md), `tests: acceptance`.
2. `DESIGN.md`: call the Skill tool with "designing" ([DESIGN-FORMAT.md](DESIGN-FORMAT.md)). Skipped only when the project has no user interface.
3. The instruction file(s): one line pointing at `CONTEXT.md` and when to read it, one at `DESIGN.md` for UI work, plus only what no config file states (commands, the conventions no tool enforces).
4. `git init` when the folder is not a repo yet. `.gitignore`: `.workspace/`, `CONTEXT.md`, `DESIGN.md`, `CLAUDE.md`, `AGENTS.md`, each appended when missing.

## Done when

The chosen files exist, `git check-ignore` lists each of them, and the user has confirmed `CONTEXT.md` and `DESIGN.md`. `.workspace/PRD.md` was written this run: also name `/write-design-brief` (optional), then `/prototype` or an outsourced UI/UX handoff, before `/discuss-with-docs`. Stop.
