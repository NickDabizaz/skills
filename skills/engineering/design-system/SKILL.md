---
name: design-system
description: "Creates or updates the project's UI design rules before design briefs, prototypes, or significant UI implementation."
---

# Design System

Read [DESIGN-FORMAT.md](DESIGN-FORMAT.md), `CONTEXT.md`, the architecture, and any existing theme, components, or visual references. For a new UI, use `grilling` to settle audience, tone, palette, typography, component library, layout conventions, and interaction rules. For an existing UI, extract observed rules and ask only about gaps or intended changes. Prefer current config and components over duplicating token values or introducing a new library without need.

Write `.workspace/DESIGN.md` and app-specific exceptions only where needed. Cover feedback, accessibility basics, and empty/loading/error/success states. Show the user the resulting rules and settle corrections before treating them as approved.

Done when a design brief can point to unambiguous visual and interaction rules. Offer `to-spec` for a clear UI issue or `to-design-brief` when its spec already exists and a prototype was requested.
