---
name: to-design-brief
description: "Creates a detailed screen contract from an approved UI issue spec before a requested prototype."
argument-hint: "<issue spec>"
disable-model-invocation: true
---

# To Design Brief

Read [BRIEF-FORMAT.md](BRIEF-FORMAT.md), the approved issue `spec.md`, and `.workspace/DESIGN.md`. If design rules are missing, call `design-system` first. Inventory every screen and state the spec requires; resolve missing content, actions, and transitions with the user. Write `.workspace/issues/<issue-slug>/design-brief.md` in the user's input language. Keep functional rules in the spec and link them rather than duplicating them.

Done when each screen has enough content, interactions, viewports, and states for a prototype and a later visual comparison. Offer `prototype`; after the user approves a prototype, the next offer is `to-tickets`. If the user decides no prototype is needed, offer `to-tickets` directly.
