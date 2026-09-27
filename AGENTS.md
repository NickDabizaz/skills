# Skills package

This repository is the source for 17 English-language engineering skills distributed with `npx skills add NickDabizaz/skills`. There is no runtime or build step. Read [README.md](README.md) for the public workflow and `skills/engineering/ask-me/SKILL.md` for user-facing routing.

The only source tree is `skills/engineering/<skill-name>/`. Each skill has a `SKILL.md` and `agents/openai.yaml`; substantial conditional formats live beside their owning skill. Do not recreate `.claude/` or `.agents/` source trees. The installer chooses agent-specific target folders in consumer projects.

When editing a skill, read `skills/engineering/<skill-name>/SKILL.md`, its linked references, and its callers. Keep names, metadata, routing, and README examples in sync. Skill instructions and identifiers are English. Consumer issue/ticket/brief/evaluation prose follows the user's input language.

Never commit or push unless asked. This repository is a published package.
