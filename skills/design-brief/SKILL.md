---
name: design-brief
description: Turn an approved spec into a design brief: the screens and states, layout regions, content inventory, interactions, visual direction, and motion intent. Use when a spec needs a design layer before a prototype, or when the user will design it manually.
---

# Design Brief

Use when an approved spec (or a settled conversation) needs a design layer before it is built. The brief is the source of truth for what to design. The user can draw from it manually, or hand it to `prototype` to build.

Read the spec, the project's design tokens, and any design guidelines first. Report what exists, then propose. Use `grilling` for decisions the spec does not answer, and apply `principle-ui-craft` and `principle-motion-decision` so the brief carries the craft bar from the start. When naming a motion effect, use the vocabulary in [references/animation-vocabulary.md](references/animation-vocabulary.md) so the brief uses precise terms.

## What the brief contains

- **Screens and states.** Every screen or surface the work touches, and every meaningful state of it: default, loading, empty, error, success, disabled, and any edge state the spec names. Do not invent states; surface missing ones for the user to decide.
- **Layout regions.** The structural areas of each screen (header, main, aside, footer, overlay), and the order and priority within them.
- **Content inventory.** The real content each region holds: labels, headings, values, actions, icons. Mark open copy explicitly rather than inventing it.
- **Interactions.** What each control does, where it leads, and how the surface responds: transitions between views, dismissals, confirmations.
- **Visual direction.** How it should feel, anchored to the project's tokens (color, type, spacing, radius) and its personality (a crisp tool versus a playful product). Reference existing patterns to reuse before proposing new ones.
- **Motion intent.** Where motion helps: entrances and exits, feedback, spatial origin, state changes. Name the purpose per `principle-motion-decision`, and leave the exact values to implementation.
- **Accessibility path.** The keyboard path, focus order, labels, and reduced-motion behavior the design must support.

## Rules

- One brief per piece of work. Keep functional rules in the spec and link to them; do not duplicate them.
- Keep decisions in the brief and open questions as open questions. Mark anything unresolved as open rather than guessing.
- Reuse existing tokens and components. A brief that invents a parallel visual system is a defect.

## Output

Write the brief inside the workspace at `.workspace/design/<feature>/brief.md`. When no workspace is in use, present it in conversation. Keep it in the user's language, identifiers in English.

Done when the brief covers every screen and state the spec touches, every open decision is marked open, and the user can either draw from it or hand it to `prototype`.
