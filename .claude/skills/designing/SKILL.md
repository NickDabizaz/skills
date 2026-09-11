---
name: designing
description: "Write or complete DESIGN.md for an own project: interview a new project about its users, tone, style preset, and code patterns, or extract tokens, patterns, and components from an existing codebase and confirm them. Called by setup-new-project and setup-project, and by discussing when UI work meets an own project without DESIGN.md; not a starting point on its own."
---

Produces `DESIGN.md` at the repo root in the format of [DESIGN-FORMAT.md](../setup-new-project/DESIGN-FORMAT.md); nothing else. If the file exists, read it first and only fill what is missing.

## Pick the path

- **No UI code yet**: interview.
- **UI code exists**: extract.

## Interview

Ask in the [discussing](../discussing/SKILL.md) format, one question per turn, without calling that skill: the caller's loop is already running. The content being settled is DESIGN-FORMAT.md; decisions the user already stated, `.workspace/DESIGN_BRIEF.md` ([DESIGN_BRIEF-FORMAT.md](../write-design-brief/DESIGN_BRIEF-FORMAT.md)) already answers, or the repo already shows are not asked:

- Who the users are and what they come to do.
- Tone: the one or two words the interface should feel like, and a product the user points at as a reference.
- Mobile-first or desktop-first.
- Tokens the user already has (brand colours, fonts); otherwise propose a baseline that fits the tone, as one question with options.
- The style preset: one question, these three options, the one nearest the tone recommended. The pick fills radius, elevation, motion, and density, and decides how each interaction state is drawn; the user tunes any line afterwards. Colour stays with the token question above.
  - **Clean**: radius 6px; layers separated by borders, shadow under overlays only; 150ms ease-out; controls 40px.
  - **Soft**: radius 12–16px; layered soft shadows; 200ms ease-out, overlays fade and rise; controls 44px.
  - **Bold**: radius 2–4px; flat, heavy borders; 120ms linear; controls 36px; a large display step in the type scale.
- Patterns: propose them from the Stack in `CONTEXT.md` — form library and validation, where server state lives, local versus shared state, where a page, a component, and a hook belong — as one draft, confirmed in one round.

## Extract

Read the theme and config files (Tailwind config, CSS variables, theme objects), then every component the app renders. Tokens come from the config; where a config states them, the line names the file instead of copying values. Patterns come from what the code already does: the form library and validation in use, where data fetching lives, how folders are laid out. Components come from the code, one line each, with the variants their props already carry. UX principles come from what the pages already do consistently, plus the required ones.

Where two components carry one entity's fields, name it in the confirmation round: the Patterns line this project needs is the one that would have prevented it.

Show the draft as one message and ask whether it matches, discuss-style, one round per turn, until it does.

## Done when

`DESIGN.md` has all five sections, every component in the code is listed with its variants, and the user has confirmed it. Return to the calling skill.
