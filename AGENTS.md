# Skills package

This repository is the source for the engineering skills distributed with `npx skills add NickDabizaz/skills`. There is no runtime or build step. Read [README.md](README.md) for the public workflow and `skills/ask-me/SKILL.md` for user-facing routing.

The workflow merges three open, MIT licensed sources into one package: planning and workflow ideas from Matt Pocock (`mattpocock/skills`), execution and verification ideas from pstack by Lauren Tan (`cursor/plugins`), and design and motion craft from Emil Kowalski (`emilkowalski/skills`). Each source keeps its copyright notice.

The only source tree is `skills/<skill-name>/`. Each skill has a `SKILL.md` and `agents/openai.yaml`; substantial conditional formats live beside their owning skill. The execution mode `head-chef` keeps its playbooks under `playbooks/` and its scripts under `scripts/`. Do not recreate `.claude/` or `.agents/` source trees. The installer chooses agent-specific target folders in consumer projects.

When editing a skill, read `skills/<skill-name>/SKILL.md`, its linked references, and its callers. Keep names, metadata, routing, and README examples in sync. Skill instructions and identifiers are English. Consumer issue/ticket/brief/evaluation prose follows the user's input language. Keep skill text free of long dashes.

Some content was ported from harness-specific sources and still needs adapting to be fully agent-agnostic, especially the `head-chef` playbooks and scripts. Prefer plain, portable instructions (a subagent, a worktree, a tracker) over any single product's tooling.

Never commit or push unless asked. This repository is a published package.
