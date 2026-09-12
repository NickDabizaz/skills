This repo is the source of the **Skills** package: a set of coding-agent skills (`brainstorm`, `discuss`, `implement`, `review`, ...) distributed via `npx skills add NickDabizaz/skills`. There is no build step and no runtime — every skill is a `SKILL.md` prompt plus optional reference files, read directly by an agent.

## Layout

```
.claude/skills/<name>/SKILL.md           Claude Code
.claude/skills/<name>/agents/openai.yaml Codex metadata
.agents/skills/<name>/                   the same tree, for Codex and other agents
```

Both trees must carry the **same** skill content — the `skills` CLI reads either one depending on which agents the user picks at install time. Edit a skill in one tree, mirror the edit in the other, in the same change.

Shared reference files (`MODES.md`, `TICKET-FORMAT.md`, `SPEC-FORMAT.md`, `REPORT-FORMAT.md`, `RESEARCH-FORMAT.md`, `DESIGN-FORMAT.md`, `CONTEXT-FORMAT.md`, `PRD-FORMAT.md`, `DESIGN_BRIEF-FORMAT.md`, `API_REQUIREMENT-FORMAT.md`) live beside the skill that owns them; other skills point at them rather than restating them.

## Writing or editing a skill

Call the `writing-for-agents` skill before touching any `SKILL.md` — it carries the naming rules, the information-hierarchy ladder, and the pruning pass every document in this set has been through. Do not redesign a skill's structure from first principles; that skill is the single source of truth for it.

Checklist for a new skill, all in the same change:
- Naming follows the convention: a core skill is one bare verb (`discuss`), a variant adds a suffix (`discuss-with-docs`), a shared loop several skills call is a gerund (`discussing`), a supporting skill is verb plus object (`resolve-merge-conflicts`).
- Ships `agents/openai.yaml` so it works outside Claude Code.
- Gets a row in `.claude/skills/ask-me/SKILL.md` (mirrored in `.agents/skills/ask-me/`).
- Gets a row in the README's skill reference table and, if it changes the chain, in the `## The system` diagram.

## Git

Never commit or push without being asked, even mid-task — this repo is a published package other people install from.
