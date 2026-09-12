---
name: discussing
description: "The interview loop shared by discuss, discuss-with-docs, and setup-new-project: one question per turn, options with a recommendation, until the plan is settled. Reached by those skills; not a starting point on its own."
---

Interview the user, one question per turn, until the plan is settled. Discussing produces understanding and a plan; it never produces code. The only exit is the user running what the calling skill names next.

## Before the first question

Facts are your job; decisions are the user's. Read what the user wrote, then look things up yourself: the codebase, `CLAUDE.md` / `AGENTS.md`, `CONTEXT.md`, configs, existing patterns. A question whose answer is already in the conversation or findable in the repo is never asked.

Mode per [MODES.md](../implementing/MODES.md). Own project: `CONTEXT.md`'s domain and conventions are the ground the plan stands on; when the work touches UI, `DESIGN.md` ([DESIGN-FORMAT.md](../setup-new-project/DESIGN-FORMAT.md)) is too, and when it is missing, call the Skill tool with "designing" before the first UI question. Legacy: a ticket the user pasted is the starting statement of intent; the interview fills what it leaves open and adds nothing it does not ask for; design rules come from the components and theme already in the code.

## The loop

Ask, stop, wait for the answer, then ask the next. Each question:

- Targets one decision the plan depends on and you cannot settle yourself.
- Offers two to four options (A, B, C, ...), each with a one-line reason it might be right.
- Marks one option as recommended, with why.
- Leaves the user free to answer outside the options.
- Is written in the user's language: short, direct, to the point.

The user's language stops at the conversation. Anything that becomes a filename, slug, or identifier stays English regardless — own project: [CONTEXT-FORMAT.md](../setup-new-project/CONTEXT-FORMAT.md)'s Conventions carries the rule.

If the harness offers a question tool with selectable options (Claude Code: `AskUserQuestion`), use it: recommended option first, labelled "(Recommended)". Otherwise use this format:

```
❓ **<question>**

A. <option> — <why this might be right>
B. <option> — <why>
C. <option> — <why>

➡️ Recommended: **B** — <reason>. Answer with a letter, or describe something else.
```

Ask in dependency order: a question whose answer depends on another still-open question waits for its turn.

Work that touches UI settles its **UX flow** as well: each screen, where the user enters it, what each action shows the user when it succeeds and when it fails, and how the screen looks empty, loading, in error, and after success. A screen state the user has not seen described is an open decision. The flow also names the surfaces it reuses: a screen an existing component already carries says so, and two flows over one entity's fields are one component in two modes, never two screens. Before the plan is confirmed, when the work adds a screen or its layout could reasonably go more than one way, offer `/prototype` as one question — prototype first, or straight to the plan — with prototype recommended; taking it pauses the interview, which resumes here with the prototype as the plan's visual reference.

Every answer reshapes the plan: a settled decision surfaces the decisions that hang off it. Recompute what is still open after each answer.

## Done when

No open decision remains that would change what gets built, and nothing is silently assumed. Then:

1. Present the plan: goal, decisions taken with their reasons, UX flow when the work touches UI (each screen with its entry point, actions with their visible results, and its empty, loading, error, and success states, each state also an acceptance criterion), ordered implementation steps each ending on a checkable done-condition, acceptance criteria as Given/When/Then (one state, one action, one observable result each), out of scope.
2. Ask the user to confirm the plan matches their intent. Settle any disagreement with further questions, one per turn.
3. Do whatever the calling skill asked for once the plan is confirmed.
4. Tell the user what to run next, as the calling skill names it. Stop.
