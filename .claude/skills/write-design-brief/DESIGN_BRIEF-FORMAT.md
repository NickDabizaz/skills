# Design brief format

Path: `.workspace/DESIGN_BRIEF.md`. `write-design-brief` writes it from `.workspace/PRD.md` ([PRD-FORMAT.md](../setup-project/PRD-FORMAT.md)); `prototype` reads it for which pages to build and their features, `designing` reads it to skip questions it already answers. Retained as kickoff history after the kickoff spec closes its last ticket ([MODES.md](../implementing/MODES.md)).

```md
# <Product> design brief

## Pages

- **<Page>**: purpose; the PRD features it carries; entry points; reference paths when supplied.
  - Fields, actions, and states: <the field/action inventory for this page>.

## Components

- **<Component>**: which pages need it; roughly what it does.

## Typography direction

- <mood, or a reference product's type feel>
```

Rules:

- Every page names the PRD feature(s) it exists for; a page with none is out of scope for this brief.
- A component two or more pages need is named once here, not repeated per page.
- Typography direction is a feel; supplied design tokens take precedence once reconciled, otherwise `DESIGN.md` supplies the scale and preset.

Read [FIDELITY.md](../prototype/FIDELITY.md) for the field/action inventory and source handling. The brief owns the initial screen inventory; once a spec exists, it owns the reconciled contract and the brief remains historical input. A page with unresolved fields or behaviour is not ready for reproduction or implementation; a supplied image settles only what it shows.
