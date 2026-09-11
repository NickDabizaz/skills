# API requirement format

Path: `.workspace/API_REQUIREMENT.md`. `discuss-with-docs` writes it, offered and skippable, at the start of the PRD-driven kickoff's first run, once UI/UX exists, from `.workspace/PRD.md` ([PRD-FORMAT.md](../setup-new-project/PRD-FORMAT.md)) and `.workspace/DESIGN_BRIEF.md` ([DESIGN_BRIEF-FORMAT.md](../write-design-brief/DESIGN_BRIEF-FORMAT.md)); the kickoff spec reads it. Deleted, with those two, once that spec's last ticket closes ([MODES.md](../implementing/MODES.md)).

```md
# <Product> API requirements

## Endpoints

- **<METHOD> <path>**: purpose; request shape; response shape; error cases.

## Auth

- <how requests are authenticated and authorized>

## Data contracts

- **<Resource>**: fields and types the API exposes.
```

Rules:

- Skipped when the kickoff has no separate API (a single client-only app): the offer is declined, and the file is never written.
- Endpoints trace to `.workspace/PRD.md`'s features and the pages in `.workspace/DESIGN_BRIEF.md`; one endpoint with no feature behind it is out of scope.
- This file is read, not maintained: an endpoint that changes after the kickoff spec is written changes the spec, not this file.
