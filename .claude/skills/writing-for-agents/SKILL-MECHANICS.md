# Skill mechanics

The skill branch of [writing-for-agents](SKILL.md): what changes when the document is a skill. Everything about the writing itself is in `SKILL.md`.

## Layout

```
<skill-name>/
  SKILL.md             required
  agents/openai.yaml   required in this set: Codex metadata
  <REFERENCE>.md       optional; pointed at from SKILL.md, one level deep; may be shared across skills
  scripts/             optional; executed, never read into context
```

Forward slashes in every path. `SKILL.md` body under 500 lines; reference that only some branches need moves into a sibling file.

## Frontmatter

```yaml
---
name: <skill-name>
description: "<What it does>. <When to use it>."
argument-hint: "<what to type after the name>"
disable-model-invocation: true
---
```

- `name` equals the folder name: lowercase letters, digits, hyphens; at most 64 characters; never contains "anthropic" or "claude".
- `description`: at most 1024 characters, third person, no XML tags. It is the skill's top-level context pointer.
- `argument-hint`: optional; only for user-invoked skills that take input.
- `disable-model-invocation`: present and `true` only on user-invoked skills.

## Invocation

- **Model-invoked** (default): the agent, other skills, and the user can all fire it. The description is model-facing and carries the trigger branches ("Use when ..."). It costs context load every turn.
- **User-invoked**: only the human typing its name. Set `disable-model-invocation: true` (Claude Code) and `policy.allow_implicit_invocation: false` in `agents/openai.yaml` (Codex). The description is human-facing: one line, no trigger list. Zero context load; it spends cognitive load instead.

A user-invoked skill can call model-invoked skills; nothing can call a user-invoked skill. So `implement` calls `review` (model-invoked) and tells the user to run `/discuss` (user-invoked). Two user-invoked skills that share a body share it through one model-invoked skill they both call: `discuss` and `discuss-with-docs` over `discussing`, `implement` and `implement-all` over `implementing`.

A dependency is written as `call the Skill tool with "<name>"`, one skill per call. A `/name` in prose is a label for a human, not an invocation.

## agents/openai.yaml

```yaml
interface:
  display_name: "<Title Case>"
  short_description: "<under 60 characters>"
policy:
  allow_implicit_invocation: false
```

The `policy` block appears only on user-invoked skills. Keep it in sync with the frontmatter: a skill is user-invoked in both harnesses or in neither.

## Harness-neutral writing

Name the capability, then the tool as an example: "if the harness offers a question tool with selectable options (Claude Code: `AskUserQuestion`), use it; otherwise ...". Paths, commands, and formats are the same on every harness; the tool that runs them is not.

## Done when

- `name`, `description`, invocation, and `agents/openai.yaml` agree.
- The description says what and when in one or two sentences.
- Every reference file is pointed at from its skill's `SKILL.md`; a file several skills share is pointed at from each of theirs, and lives in one of them.
- The body passed the no-op test sentence by sentence.
