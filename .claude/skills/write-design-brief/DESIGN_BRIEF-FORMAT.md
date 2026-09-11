# Design brief format

Path: `.workspace/DESIGN_BRIEF.md`. `write-design-brief` writes it from `.workspace/PRD.md` ([PRD-FORMAT.md](../setup-new-project/PRD-FORMAT.md)); `prototype` reads it for which pages to build and their features, `designing` reads it to skip questions it already answers. Deleted, with `.workspace/PRD.md` and `.workspace/API_REQUIREMENT.md`, once the PRD-driven kickoff's spec closes its last ticket ([MODES.md](../implementing/MODES.md)).

```md
# <Product> design brief

## Pages

- **<Page>**: purpose; the PRD features it carries.

## Components

- **<Component>**: which pages need it; roughly what it does.

## Typography direction

- <mood, or a reference product's type feel>
```

Rules:

- Every page names the PRD feature(s) it exists for; a page with none is out of scope for this brief.
- A component two or more pages need is named once here, not repeated per page.
- Typography direction is a feel, not a scale — `DESIGN.md`'s style preset (clean, soft, bold) turns it into actual tokens.
