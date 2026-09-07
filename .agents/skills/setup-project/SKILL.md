---
name: setup-project
description: "Make a repo that already has code an own project for this skill set: read the code for stack, commands, conventions, domain, and tests, ask only what the code cannot say, then write CONTEXT.md, DESIGN.md, and CLAUDE.md / AGENTS.md and keep them out of git. Run again to add whatever is missing."
argument-hint: "[what the project is]"
disable-model-invocation: true
---

Writes documents only; the code is not touched. An empty repo is `/setup-new-project`'s job. Run on a repo that already has some of the files: read them, keep them, and produce only what is missing.

## Read

Fill each section of [CONTEXT-FORMAT.md](../setup-new-project/CONTEXT-FORMAT.md) from the repo before asking anything:

- **Purpose**: `README` and other docs, when they state it.
- **Domain**: models, entities, schemas, migrations, types. Invariants only where the code enforces them (constraints, validators, guards).
- **Stack** and **Commands**: manifests, lockfiles, configs, CI files. Commands only when no config states them.
- **Conventions**: what the code does consistently and no tool enforces: naming, layout, error handling, test style. Three or more occurrences make a convention; one is an accident.
- **Tests**: `acceptance` when a runner is configured and a suite exists, `none` otherwise.

Done when every section is filled from evidence or marked unknown.

## Interview

Call the Skill tool with "discussing". Open with the draft as one message, then ask only what is unknown: purpose and users, invariants the code does not enforce, ticket backend (local `.issues/<issue-name>/tickets/`, or GitHub Issues with `gh` authenticated), instruction file (`CLAUDE.md`, `AGENTS.md`, or both). The next step discussing names once the plan is confirmed: `/audit` to see where the codebase stands, or `/discuss` for the first change.

## Write

As the Write section of [setup-new-project](../setup-new-project/SKILL.md), with `tests` as read above and `DESIGN.md` on `designing`'s extract path.

## Done when

The chosen files exist, `git check-ignore` lists each of them, and the user has confirmed `CONTEXT.md` and `DESIGN.md`. Stop.
