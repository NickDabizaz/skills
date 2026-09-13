---
name: setup-project
description: "Make a repo an own project for this skill set: read whatever code already exists for stack, commands, conventions, domain, and tests; interview for the rest — a full interview on an empty repo, with an optional PRD-driven kickoff first, or only what the code cannot say on one with code already in it. Writes CONTEXT.md, DESIGN.md, and CLAUDE.md / AGENTS.md and keeps them out of git. Run again to add whatever is missing."
argument-hint: "[what the project is]"
disable-model-invocation: true
---

Writes documents only; existing code is not touched. The first code for an empty repo goes through `/discuss-with-docs` and `/implement`, so it is reviewed like everything after it.

Run on a repo that already has some of the files: read them, keep them, and produce only what is missing.

## Read

An empty repo has nothing to read: skip to Kickoff. Otherwise fill each section of [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md) from the repo before asking anything:

- **Purpose**: `README` and other docs, when they state it.
- **Domain**: models, entities, schemas, migrations, types. Invariants only where the code enforces them (constraints, validators, guards).
- **Stack** and **Commands**: manifests, lockfiles, configs, CI files. Commands only when no config states them.
- **Conventions**: what the code does consistently and no tool enforces: naming, layout, error handling, test style. Three or more occurrences make a convention; one is an accident.
- **Tests**: `acceptance` when a runner is configured and a suite exists, `none` otherwise.

Done when every section is filled from evidence or marked unknown.

## Kickoff

Only for an empty repo, and only while `CONTEXT.md` does not exist yet: one question first, full PRD-driven kickoff or the quick setup below — recommended for a brand-new product with real UI/UX and an API surface; skip it for a script or small tool. Declining changes nothing below.

Accepting: call the Skill tool with "discussing" for [PRD-FORMAT.md](PRD-FORMAT.md) (vision, users, features, success criteria, out of scope) and write `.workspace/PRD.md`. Then continue below as usual.

## Interview

Call the Skill tool with "discussing". The plan being settled is the content of [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md); decisions the user already stated, `.workspace/PRD.md` already answers, or the repo already shows are not asked. An empty repo opens with nothing settled: purpose and users; domain entities, relations, invariants; stack; conventions no tool enforces; ticket backend; instruction file. A repo with code opens with the Read draft as one message and asks only what is unknown: purpose and users, invariants the code does not enforce, ticket backend (local `.workspace/<issue-name>/tickets/`, or GitHub Issues with `gh` authenticated), instruction file (`CLAUDE.md`, `AGENTS.md`, or both).

The next step discussing names once the plan is confirmed: `/discuss-with-docs` for the first feature on an empty repo; `/audit` to see where the codebase stands, or `/discuss` for the first change, on a repo with code.

## Write

1. `CONTEXT.md` per [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md), `tests` as read above, or `acceptance` on an empty repo.
2. `DESIGN.md`: call the Skill tool with "designing" ([DESIGN-FORMAT.md](DESIGN-FORMAT.md)) — interview path for an empty repo, extract path for a repo with code. Skipped only when the project has no user interface.
3. The instruction file(s): one line pointing at `CONTEXT.md` and when to read it, one at `DESIGN.md` for UI work, plus only what no config file states (commands, the conventions no tool enforces).
4. `git init` when the folder is not a repo yet. `.gitignore`: `.workspace/`, `CONTEXT.md`, `DESIGN.md`, `CLAUDE.md`, `AGENTS.md`, each appended when missing.

## Done when

The chosen files exist, `git check-ignore` lists each of them, and the user has confirmed `CONTEXT.md` and `DESIGN.md`. `.workspace/PRD.md` was written this run: also name `/write-design-brief` (optional), then `/prototype` or an outsourced UI/UX handoff, before `/discuss-with-docs`. Stop.
