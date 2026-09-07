---
name: brainstorm
description: "Widen a raw idea into three concrete directions a round until one is clear enough to plan, and write them to .issues/<issue-name>/ideas.md."
argument-hint: "<the raw idea, however vague>"
disable-model-invocation: true
---

Brainstorming produces a direction, not a plan; it never designs and never diagnoses. `discuss` narrows a direction the user already has; this widens when there is none. The ideas are the question: the user cannot answer what they have not seen, so nothing is asked before the first three exist.

## Ground

Facts are your job. Read what the user wrote, then whatever the repo can say: `CLAUDE.md` / `AGENTS.md`, `CONTEXT.md`, `README`, the code around the idea's subject. No repo, an empty one, or one with nothing to say about the idea leaves the idea itself as the whole ground. Mode per [MODES.md](../implementing/MODES.md).

Ask nothing here. When the idea rests on a bug whose cause is not yet known, tell the user to run `/investigate` and stop: a cause is proven, never brainstormed.

Done when you can name what already exists near the idea's subject and who it touches today, or say that nothing does.

## Spread

Three ideas per round. Each carries:

- **Who it is for**, and the problem it solves for them.
- **What it is**: the shape of the thing, concrete enough to react to.
- **Cost**: what it takes to build, and what it takes to keep.
- **The bet**: what has to be true for it to be worth doing.

The three differ in who they serve or which problem they solve, never in feature detail on one idea. They sit at different ambition levels: one small enough to finish in a sitting, one middling, one that changes the direction of the thing. An idea ruled out in an earlier round never returns.

## Narrow

Close every round with one question, discuss-style ([discussing](../discussing/SKILL.md) format): go deeper on one idea, so the next round is three concrete versions of it, or spread again from an angle not yet used. Going deeper sets the other two aside, and the choice itself is their reason; ruling one out explicitly records the user's own words, and those words bound the next round.

A direction is ready when three fields are filled: who it is for, the problem it solves, and the smallest version already worth using. One of them empty is another round, not a hand-off; say which one is missing.

## Write

Folder `.issues/<issue-name>/ideas.md`, `<issue-name>` a short kebab-case name for the chosen direction, or for the idea itself when none was chosen, named at the end because at the start there is none. Create the folder if it is missing; a file there already: read it before the first round and continue from it instead of starting over. This file is the only thing written to disk, and `spec.md` and `tickets/` land beside it later. Legacy: when `.issues/` is not ignored, add it to `.git/info/exclude`, which stays local, so nothing reaches the remote.

1. The idea as the user gave it.
2. Every idea offered, by round, with its four fields.
3. Every idea set aside or ruled out, with its reason.
4. The chosen direction with its three fields, and the questions it leaves open for `/discuss`.

## Done when

`ideas.md` holds a direction whose three fields are filled, and every idea offered is in the file, each set aside, ruled out, or chosen. Then name the next step with the path of `ideas.md`, and say the spec belongs in that same folder: `/discuss` when the direction is small enough to build straight away, `/discuss-with-docs` when it spans sessions or should leave a spec.

The other ending is no direction at all: the user closes a round having decided none of this is worth building. That is a result, not a failure. Write `ideas.md` with the reason in place of a direction, and name no next step.

Stop.
