# PRD format

Path: `.workspace/PRD.md`. `setup-new-project` writes it when the user takes the PRD-driven kickoff; `write-design-brief`, and `discuss-with-docs` for that project's first spec, read it. Deleted, with `.workspace/DESIGN_BRIEF.md` and `.workspace/API_REQUIREMENT.md` when they exist, once that spec's last ticket closes ([MODES.md](../implementing/MODES.md)).

```md
# <Product> PRD

## Vision

One paragraph: the problem, who it is for, and the outcome.

## Users

- **<User type>**: what they need, why they need it.

## Features

- **<Feature>**: what it does; why it's in this scope.

## Success criteria

- <A measurable signal the product works>

## Out of scope

- <What this scope deliberately skips>
```

Rules:

- Independent of `CONTEXT.md`: `CONTEXT.md` stays useful after this file is gone, so it never links here.
- Every feature is what `DESIGN_BRIEF.md`'s ([DESIGN_BRIEF-FORMAT.md](../write-design-brief/DESIGN_BRIEF-FORMAT.md)) pages and the kickoff spec's decisions trace back to.
- This file is read, not maintained: a feature that changes after the kickoff spec is written changes the spec, not this file.
