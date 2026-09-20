---
name: prototype
description: "Reproduce supplied HTML/CSS or JPG/PNG designs 1:1 as clickable prototypes, explore layout options, or refine an existing page in .workspace/prototype/<page-name>/."
argument-hint: "<reference or page/flow; reproduce, options, or refine>"
disable-model-invocation: true
---

Prototyping produces HTML the user can open and react to; it never touches the app's code. A supplied design is reproduced by default; exploration and redesign require the user to ask for them. Read [FIDELITY.md](FIDELITY.md) for source handling, approval versions, field contracts, and render verification whenever a reference applies.

## Before building

Facts are your job. Read what the user wrote, then the source of the spec: a `.workspace/<issue-name>/spec.md` and its UX flow, `.workspace/DESIGN_BRIEF.md` ([DESIGN_BRIEF-FORMAT.md](../write-design-brief/DESIGN_BRIEF-FORMAT.md)) for the page's purpose and features when no spec exists yet, a pasted ticket, `CONTEXT.md`, or, for an existing page, the page and components that render it now. Read supplied files or attachments as design input, including HTML/CSS and JPG/PNG in `.workspace/design-reference/`; their location or author does not change their authority. The prototype carries the real content, fields, states, and flows of that spec, never lorem ipsum. Look and behaviour follow `DESIGN.md` where it exists ([DESIGN-FORMAT.md](../setup-project/DESIGN-FORMAT.md)), otherwise the app's existing fonts, colours, spacing, and components, unless the user asked for a new look.

Ask, discuss-style ([discussing](../discussing/SKILL.md) format, one per turn), only what the spec leaves open and the build depends on. Always settle one thing first when the user did not say it: the purpose.

Resolve source conflicts per FIDELITY.md before building; record the choice in the plan and reconcile `DESIGN.md`.

- **Reproduce**: the user supplied a design and did not request changes. Build one matching prototype.
- **Options**: the user has no picture, or wants to compare directions. Build three.
- **Refine**: the user has a page and wants it better. Build one.

## Build

Folder: `.workspace/prototype/<page-name>/`, `<page-name>` kebab-case. Create it if missing; if it holds files already, read them first and continue from them. Legacy ([MODES.md](../implementing/MODES.md)): when `.workspace/` is not ignored, add it to `.git/info/exclude` so nothing reaches the remote.

Without supplied code, default to a self-contained `.html` with inline CSS/JS and local assets. For supplied HTML/CSS, preserve its file structure and assets when that avoids reconstruction; provide the command needed to open it. Match agreed viewports; a reference for one width does not settle other widths. Interactions the spec names (tabs, modals, form validation, empty and error states) work with plain JS on static data. Every interactive control draws its hover, focus-visible, active, disabled, and loading state; where the spec names a surface two flows share, the prototype renders it once with a mode switch.

**Options** produce `option-1.html`, `option-2.html`, `option-3.html` and `index.html`. The options differ in layout, navigation, and information hierarchy, never only in colour. `index.html` lists the three with one line on what each optimises for and a link each. Keep presentation notes outside the product UI.

**Reproduce** and **Refine** produce `prototype.html` (with local source/assets as needed). Describe changes in the conversation, outside the product UI.

If the harness can show HTML to the user directly (Claude Code: the Artifact tool), show `index.html` or `prototype.html` as well; the files on disk are the deliverable.

## Done when

Every file opens, every named interaction works, and supplied-reference builds pass FIDELITY.md verification. Keep comparisons and unresolved limitations visible to the user. Then:

1. Options: ask which option to choose, with one recommended and why; make the selected option the current `prototype.html`. Reproduce or Refine: ask whether the result matches; adjust until confirmed. Preserve the approved version and its assets per FIDELITY.md; `prototype.html` may be the convenient current entry point, but the plan links the approved version. Keep original references. Changes to an already-approved prototype also reconcile the affected plan and tickets before implementation resumes.
2. Tell the user what to run next with the file path: `/discuss` when the requirements behind the page are still open, `/implement` when they are settled and the plan names the approved baseline plus its field/action contract. Stop.
