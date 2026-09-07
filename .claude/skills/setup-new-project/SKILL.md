---
name: setup-new-project
description: "Make a repo an own project for this skill set: interview about domain, stack, conventions, design, and ticket backend, then write CONTEXT.md, DESIGN.md, and CLAUDE.md / AGENTS.md and keep them out of git. Run again to add whatever is missing."
argument-hint: "<what the project is>"
disable-model-invocation: true
---

Writes documents only. The first code goes through `/discuss-with-docs` and `/implement`, so it is reviewed like everything after it.

Run on a repo that already has some of the files: read them, keep them, and produce only what is missing. A repo that already has code is `/setup-project`'s job.

## Interview

Call the Skill tool with "discussing". The plan being settled is the content of [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md); decisions the user already stated or the repo already shows are not asked:

- Purpose and users.
- Domain: the main entities, their relations, the invariants that must never break.
- Stack: language, framework, package manager, test runner, linter and formatter.
- Conventions no tool enforces: naming, layout, error handling, test style.
- Ticket backend: local `.issues/<issue-name>/tickets/`, or GitHub Issues (needs `gh` authenticated).
- Instruction file: `CLAUDE.md`, `AGENTS.md`, or both.

The next step discussing names once the plan is confirmed is `/discuss-with-docs` for the first feature.

## Write

1. `CONTEXT.md` per [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md), `tests: acceptance`.
2. `DESIGN.md`: call the Skill tool with "designing" ([DESIGN-FORMAT.md](DESIGN-FORMAT.md)). Skipped only when the project has no user interface.
3. The instruction file(s): one line pointing at `CONTEXT.md` and when to read it, one at `DESIGN.md` for UI work, plus only what no config file states (commands, the conventions no tool enforces).
4. `git init` when the folder is not a repo yet. `.gitignore`: `.issues/`, `CONTEXT.md`, `DESIGN.md`, `CLAUDE.md`, `AGENTS.md`, each appended when missing.

## Done when

The chosen files exist, `git check-ignore` lists each of them, and the user has confirmed `CONTEXT.md` and `DESIGN.md`. Stop.
