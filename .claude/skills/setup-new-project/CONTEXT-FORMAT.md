# CONTEXT.md format

Path: repo root, gitignored. Its presence marks the repo as an own project ([MODES.md](../implementing/MODES.md)). `setup-new-project` or `setup-project` writes it; `discuss`, `implement`, `review`, `write-tickets`, `investigate`, `research`, and `audit` read it. Design rules live beside it in `DESIGN.md` ([DESIGN-FORMAT.md](DESIGN-FORMAT.md)).

```md
# <Project>

## Purpose

One paragraph: what it is for and who uses it.

## Domain

- **<Entity>**: what it is; how it relates to the others; the invariants that must hold.

## Stack

- <language, framework, package manager, test runner, linter and formatter>

## Conventions

- <A rule no tool enforces: naming, layout, error handling, test style. One line each, with the reason when it is not obvious.>

## Commands

- test: `<command>`
- lint: `<command>`
- run: `<command>`

## Tests

tests: acceptance | none

## Tickets

backend: local | github
```

Rules:

- Domain lines are the model `discuss` reasons with; keep them current when a feature changes the model.
- Commands only when no config file states them; otherwise the config is the source of truth.
- `tests` is the one line `implement` and `review` read for the test discipline (MODES.md). `setup-new-project` writes `acceptance`; `setup-project` writes `acceptance` when a runner and a suite exist, `none` otherwise. Change it to `acceptance` by hand once a suite exists.
- `backend` is the one line `write-tickets` and `implement` read to find tickets.
