# DESIGN.md contract

Path: `.workspace/DESIGN.md`. Create it for projects with UI before a design brief or prototype. An existing application's actual theme and components are the starting evidence; a new project's choices are discussed with the user.

Record:

- Product tone, users, accessibility baseline, and UX rules for feedback, navigation, and empty/loading/error/success states.
- Color roles and palette, typography families/scale/weights, spacing, radii, borders or elevation, motion, density, responsive breakpoints, and the default viewport.
- UI framework and component library choice, with reasons and any existing tokens/configuration that are authoritative.
- Patterns for forms and validation, data fetching and error handling, shared vs local state, routing, and component reuse.
- Existing component inventory and when to use or extend each. For a new project, name planned components only when a concrete issue requires them.
- Shared rules and links to per-app exceptions for multi-app projects.

Do not copy every value from an existing theme config. Point to the config and write only the rule or reason agents cannot derive from it. If an app has a distinct identity, put its differences in `.workspace/apps/<app-slug>.md` and link them here.
