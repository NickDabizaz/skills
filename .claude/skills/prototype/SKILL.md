---
name: prototype
description: "Turn a page or flow the user cannot yet picture into clickable HTML prototypes in .workspace/prototype/<page-name>/: several distinct options to choose from, or one refined design of an existing page."
argument-hint: "<the page or flow, and whether you want options or one better version>"
disable-model-invocation: true
---

Prototyping produces HTML the user can open and react to; it never touches the app's code. A visual settles a UI decision faster than a paragraph does, so the prototype is the question.

## Before building

Facts are your job. Read what the user wrote, then the source of the spec: a `.workspace/<issue-name>/spec.md` and its UX flow, `.workspace/DESIGN_BRIEF.md` ([DESIGN_BRIEF-FORMAT.md](../write-design-brief/DESIGN_BRIEF-FORMAT.md)) for the page's purpose and features when no spec exists yet, a pasted ticket, `CONTEXT.md`, or, for an existing page, the page and components that render it now. The prototype carries the real content, fields, states, and flows of that spec, never lorem ipsum. Look and behaviour follow `DESIGN.md` where it exists ([DESIGN-FORMAT.md](../setup-new-project/DESIGN-FORMAT.md)), otherwise the app's existing fonts, colours, spacing, and components, unless the user asked for a new look.

Ask, discuss-style ([discussing](../discussing/SKILL.md) format, one per turn), only what the spec leaves open and the build depends on. Always settle one thing first when the user did not say it: the purpose.

- **Options**: the user has no picture, or wants to compare directions. Build three.
- **Refine**: the user has a page and wants it better. Build one.

## Build

Folder: `.workspace/prototype/<page-name>/`, `<page-name>` kebab-case. Create it if missing; if it holds files already, read them first and continue from them. Legacy ([MODES.md](../implementing/MODES.md)): when `.workspace/` is not ignored, add it to `.git/info/exclude` so nothing reaches the remote.

Every file is self-contained: one `.html`, CSS and JS inline, no build step, no network dependency, opens by double-click and works at phone and desktop widths. Interactions the spec names (tabs, modals, form validation, empty and error states) work with plain JS on static data. Every interactive control draws its hover, focus-visible, active, disabled, and loading state; where the spec names a surface two flows share, the prototype renders it once with a mode switch.

**Options** produce `option-1.html`, `option-2.html`, `option-3.html` and `index.html`. The options differ in layout, navigation, and information hierarchy, never only in colour. Each option opens with a small banner: its number and one line on what it optimises for. `index.html` lists the three with that line and a link each.

**Refine** produces `prototype.html`, opened by a banner listing each change from the current page and why.

If the harness can show HTML to the user directly (Claude Code: the Artifact tool), show `index.html` or `prototype.html` as well; the files on disk are the deliverable.

## Done when

Every file opens and every named interaction works. Then:

1. Options: ask one question, the three options with the line each optimises for, one recommended with why. Once the user picks, delete the other two and `index.html`; the pick, renamed to `prototype.html`, is the reference. Refine: ask whether it matches; adjust, one round per turn, until it does.
2. Tell the user what to run next with the file path: `/discuss` when the requirements behind the page are still open, `/implement` when they are settled and the prototype is the plan's visual reference. Stop.
