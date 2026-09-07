# DESIGN.md format

Path: repo root, gitignored, own project only ([MODES.md](../implementing/MODES.md)); its presence changes no mode. `designing` writes it; `discussing`, `prototype`, `implementing`, and `review` read it whenever the work touches UI.

```md
# <Project> design

## UX principles

- <A rule about how the product behaves for the user. One line each, with the reason when it is not obvious.>

## Visual tokens

- colour: <palette with roles: background, surface, text, primary, danger, ...>
- typography: <families, scale, weights>
- spacing: <scale>
- radius: <scale>
- elevation: <what separates layers: borders, shadows, or both; the steps>
- motion: <duration and easing, per kind: hover, entry, overlay>
- density: <control height and field spacing>
- breakpoints: <widths, and which one is designed first>

## Interaction states

- <Control or group>: how it is drawn at rest, then on hover, focus-visible, active, disabled, and loading.

## Patterns

- **Forms**: <library and validation; one schema serves create and edit; the mode arrives as a prop>
- **Data**: <where server state lives; how loading and failure are handled>
- **State**: <local vs shared, and where shared state lives>
- **Files**: <where a page, a component, a hook belongs>
- **Reuse**: <a new component only when no existing one fits behind a prop>

## Components

- **<Component>**: what it is for; when to use it over its neighbours. Variants: <the props that flex it>.
```

Rules:

- UX principles always include: every user action gets visible feedback; every screen handles empty, loading, error, and success; navigation and copy tone. Add the project's own on top.
- Tokens only when no config file states them (a Tailwind config, a theme file); otherwise the config is the source of truth and the line names it.
- Interaction states cover every control the user can reach. A state with no described look is a decision left open.
- Patterns bind new code; Components describe what exists. Where the two disagree, Patterns wins and the component is what moves.
- One entity's create and edit are one component in two modes: the difference is initial values, the submit action, and the labels. Two components carrying one entity's fields is a duplicate.
- Components list what exists in the code, with its purpose and the variants it already carries, so extending it is decidable without opening the file. A component in the code and not here is missing; a component here and not in the code is stale.
