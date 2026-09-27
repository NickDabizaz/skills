---
name: plan-project
description: "Plans a new or existing software project: application boundaries, architecture, stack, infrastructure, data, design, and ticket tracker."
argument-hint: "<project or repository>"
disable-model-invocation: true
---

# Plan Project

Read [PROJECT-FORMAT.md](PROJECT-FORMAT.md). Inspect the existing repository first: instructions, documentation, manifests, source tree, schemas, migrations, CI, and UI theme. Report evidence and separate observed choices from proposed changes. For an empty project, interview for the purpose and users first. Use `grilling` for decisions the repository cannot answer and `domain-modeling` for domain terms or invariants.

Settle purpose and application inventory; mono- or multi-repo; stack and libraries; infrastructure and deployment; module boundaries and design pattern; folder plan; schema, relationships, constraints, and migration approach. Explain tradeoffs and recommend the simplest option that meets the stated need. Ask which ticket backend to use: local Markdown or GitHub Issues. For GitHub verify the repository and access before promising publication. Also ask for the project's prose language if the user's input does not establish it.

Create root `AGENTS.md`, `CLAUDE.md`, and `CONTEXT.md` using concise pointers, then `.workspace/ARCHITECTURE.md`, `.workspace/DOMAIN.md`, and `issues/README.md` with small issue outcomes and real dependencies. For UI projects call `design-system` before a design brief or prototype. Keep `.workspace/` ignored by Git for a local tracker and tracked for GitHub. Preserve existing user documentation and code. Planning records decisions; creating apps, migrations, and infra is later ticketed work.

Done when every agreed planning decision has a documented home, open decisions are explicit, the tracker choice is recorded, and the user can locate the next issue. Offer `grill-me` for an unclear first issue or `to-spec` for a clear one; offer `to-tickets` only after a spec exists.
