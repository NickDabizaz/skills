---
name: prototype
description: Build an interactive prototype of a UI piece, either several genuinely different variants behind a visual picker or one variant when the direction is set. Use when a design brief or a spec needs a prototype to look at and choose from. Starts from a brief if one exists, or straight from a spec.
---

# Prototype

Use when you need to see and choose a UI piece, not just read about it. Work from a `design-brief` if one exists, otherwise from the spec or the settled conversation. Build real interactions held to the craft bar, never lorem ipsum or dead buttons.

Apply `principle-ui-craft`, `principle-motion-decision`, and `principle-fluid-interfaces`. For ready recipes, read [references/recipes.md](references/recipes.md). For component or library choices, read [references/library-picks.md](references/library-picks.md).

## Two modes

- **Explore.** Build three to five genuinely different variants, each on a named axis (layout, density, personality, motion, interaction model), behind a visual picker. Three tints of one idea waste the picker; every variant must be a direction you could ship on its own.
- **Build.** One prototype in the direction already chosen, closer to production quality, still isolated from production code.

Decide the mode from context. If the direction is unclear, explore. If a variant was chosen or the brief is specific, build.

## Recon

Before writing code, map the ground:

- **Stack.** Framework, styling system, motion library.
- **Tokens.** Colors, radii, spacing, fonts, easing and duration variables. Variants should look like they could ship in this product tomorrow.
- **Personality.** Playful product or crisp tool; this bounds how far the boldest variant may go.
- **Context.** Where the piece renders: background, neighbors, sizes.

If there is no project (empty directory, or the user is just exploring), use a restrained default: neutral grays, one accent, system font.

## Where prototypes live

Every prototype is a folder per topic inside the workspace, with a self-contained HTML file as the entry:

```
.workspace/prototype/<topic>/index.html
```

- Topic names are lower kebab-case English slugs, for example `toast-checkout` or `pricing-card`.
- `index.html` is self-contained: CSS and JS inline, openable in a browser with no build step.
- In explore mode, `index.html` holds every variant plus the picker. In build mode, it holds one prototype.
- A later round on the same topic adds files in the same folder.

When the project has a dev server, an isolated route is also acceptable, but nothing imports from the prototype surface into production code.

## The picker

In explore mode, the picker renders one variant at a time, full size, in realistic surrounding context (a toast needs a page behind it, a card needs siblings). Side-by-side thumbnails distort spacing; never judge UI at small size. Switching is instant with no animation: flipping is a high-frequency action.

The picker is chrome, not a contestant. Its exact markup and behavior live in [references/picker.md](references/picker.md). Keep it plain and fixed at the bottom center, and never adapt it to the project's style.

## Craft bar

Every variant individually meets the bar: `ease-out` on entrances, never `ease-in`; UI motion under 300ms; correct `transform-origin`; `transform` and `opacity` only; reduced motion handled; press feedback on `:active`. A sloppy variant does not widen the exploration, it just loses on execution.

## Verify and hand off

Run the prototype. Confirm every variant renders, every interaction responds, and the console is clean. Flip through all of them yourself before showing the user. Then present the set and stop: the choice belongs to the user.

| # | Variant | Axis | When it is right | Its cost |
| --- | --- | --- | --- | --- |

Name the entry path and the keys to flip.

## Promote on selection

When the user picks, integrate that variant where it belongs, following the project's conventions, then delete the prototype surface unless the user asks to keep it. If the user wants another round, keep the harness and diverge around the direction they leaned toward.

Done when the user has a prototype they can open, every variant works, and the tradeoffs are stated honestly.
