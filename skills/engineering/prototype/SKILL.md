---
name: prototype
description: "Builds an inspectable UI prototype from an approved design brief when the user requests one, and records its approved baseline."
---

# Prototype

Read `.workspace/DESIGN.md`, the issue `spec.md`, and [BRIEF-FORMAT.md](../to-design-brief/BRIEF-FORMAT.md) through its completed `design-brief.md`. Reuse existing assets and components when practical. Build the smallest inspectable prototype that covers every specified page, transition, and significant state. Use the brief's content, tokens, and viewport expectations; surface any missing decision before inventing product behavior.

Show the user the prototype and collect corrections. Once approved, preserve that version in the issue's `prototype/` folder, identify its viewports and states, and update the brief and spec with the baseline reference. An approved version is not silently overwritten; a changed layout becomes a new baseline and reconciles open tickets.

Done when the user can inspect all agreed screens and the baseline is traceable from the spec. Offer `to-tickets` next; if the prototype exposed a missing behavior decision, offer `grill-with-docs` to settle and revise the spec first.
