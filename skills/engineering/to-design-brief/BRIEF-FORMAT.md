# Design brief

Path: `.workspace/issues/<issue-slug>/design-brief.md`. Produce it from the approved issue spec and `.workspace/DESIGN.md` when the user requests a prototype. It is the prototype's screen contract, not a second functional spec.

For every screen or state include:

- App, route, entry point, navigation target, and intended viewport(s).
- Layout regions and their hierarchy; reusable components and interactions.
- Exact content inventory: headings, labels, helper text, representative data, buttons, links, tables, and empty copy. Mark copy that remains open.
- Each action's visible success, failure, validation, disabled, and loading behavior; empty, loading, error, and success screen states.
- Responsive changes, keyboard path, focus and contrast requirements.
- Relevant design tokens and visual references from `DESIGN.md`.
- What a reviewer must compare between prototype and implementation; any allowed difference.

List the screen sequence and cross-screen transitions before individual screens. Reuse one component for the same entity's create/edit flows when the difference is mode and initial values. Resolve missing content or behavior with the user before prototyping. After prototype approval, record its immutable baseline path/version here and in `spec.md`; do not silently replace an approved baseline.
