# Project workspace

`AGENTS.md` and `CLAUDE.md` at the project root contain a short overview and tell agents to read `CONTEXT.md`. `CONTEXT.md` is a navigation map: project purpose, tracker choice, prose language rule, and links into `.workspace/`. Keep detailed decisions in `.workspace/`.

```text
.workspace/
  ARCHITECTURE.md
  DOMAIN.md
  DESIGN.md                 # when the project has UI
  apps/<app-slug>.md         # only when an app differs from shared rules
  issues/README.md           # small issue outcomes and dependencies
  issues/<issue-slug>/
    spec.md
    design-brief.md         # only when a prototype is requested
    prototype/              # approved baseline and assets, if any
    tickets/                # local ticket files, or GitHub link index
```

`ARCHITECTURE.md` records purpose and users; application inventory and boundaries; mono- or multi-repo decision; stack and libraries with reasons; infrastructure and deployment target; module boundaries and dependency rules; directory plan; database entities, relationships and constraints; migration conventions; commands or links to configured scripts; and unresolved decisions. Existing code and configuration are evidence, not automatically a desired future state. Avoid duplicating facts already expressed in configuration; link to them instead.

`DOMAIN.md` records a glossary with stable English identifiers, relationships, invariants, and decisions whose reasons matter later. For a multi-app project, shared rules live here and differing app details live under `apps/`.

`issues/README.md` is the project issue map: one line per small, observable outcome with its app/module, dependency, and link to its issue folder or GitHub parent issue. It is a planning index, not a duplicate ticket tracker. Expand an entry into `spec.md` only when its details are ready.

Setup asks for the ticket backend: `local` or `github`. With `local`, ignore `.workspace/` in Git and store issue and ticket state in Markdown. With `github`, track `.workspace/` in Git, use GitHub Issues as the only source of ticket content and status, and keep only links in the local `tickets/` directory. Do not store secrets in tracked workspace files. Record the backend in `CONTEXT.md`.

All paths, slugs, code identifiers, and skill instructions are English. Issue specs, ticket prose, design briefs, and manual evaluation guides use the user's input language. Continue in that language unless the user switches or asks otherwise.

For local issues and tickets use `needs-info`, `ready`, `in-progress`, `review`, `awaiting-user`, or `done` where applicable. `blocked-by` is a separate dependency field; an item is ready only when all blockers are done. GitHub uses its native open/closed state and the equivalent labels or fields available in that repository. Do not invent a second local status copy for GitHub tickets.
