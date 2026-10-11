---
name: setup
description: Configure a repository for this skill set: its issue/detail trackers, triage vocabulary, domain doc layout, and the model or role choices the execution skills use. Run once before first use.
---

# Setup

Run once per project, before the other skills. Inspect first, ask only what the repository cannot answer, and write the configuration the rest of the package reads.

## 1. Inspect the repository

Look at what already exists and report it as observed facts before proposing anything:

- Git remote and host, if any.
- Instruction files (AGENTS.md, CLAUDE.md, and similar) and any existing agent notes.
- Existing glossaries, ADRs, docs, or a specs directory.
- Manifests, source tree, and whether it is a monorepo.
- Any scratch or workspace directory.

Separate what you observed from what you propose to change.

## 2. Choose the trackers

Ask which backend, unless the repo clearly states one:

- **Local Markdown.** Specs and tickets are files in the workspace. Private to the checkout, not shared.
- **A hosted tracker (for example GitHub Issues).** Issues are the source of truth; local files hold links.

Record the choice where the other skills will find it.

## 3. Settle triage vocabulary

If `triage` will be used, agree on the categories and states (for example bug, enhancement; needs-triage, needs-info, ready, waiting, done) and where they live.

## 4. Settle the domain doc layout

Single context or multiple contexts. Where the glossary and decision records live. Create them lazily, not all up front.

## 5. Settle the execution defaults

Record, in one place the execution skills read:

- The models or roles to prefer per task kind (code, judgment, prose), if the harness allows model selection.
- The verification surfaces available for this project (how an agent drives the app and captures evidence).
- Any standing preferences: branch naming, commit style, forbidden paths.

## 6. Write the configuration

Create the small set of pointer files the package expects, keep them short, and link to detail rather than duplicating it. Do not build apps, migrations, or infrastructure here; that is later, ticketed work.

## Done

Done when the trackers, vocabulary, and domain layout are recorded, the execution defaults are written down, and the user can point at the next skill (usually `grilling` or `to-spec`).
