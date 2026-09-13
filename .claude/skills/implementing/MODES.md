# Modes

`CONTEXT.md` at the repo root marks an **own project**; without it the repo is **legacy**. `setup-project` writes that file — interviewing on an empty repo, reading the code first on one that already has it; nothing else does.

| | Own project | Legacy |
| --- | --- | --- |
| Where work comes from | A spec, split into tickets by `write-tickets`; or a plan in the conversation | A ticket the user pastes from their tracker, settled into a plan by `discuss`; an `audit` or `research` spec, split by `write-tickets`; or a plan in the conversation |
| Documents in the repo | `CONTEXT.md`, `DESIGN.md`, `CLAUDE.md` / `AGENTS.md`, `.workspace/`; all gitignored. `DECISIONS.md`, appended to by `domain-modeling`, joins them once a decision first calls for it. A PRD-driven kickoff adds `.workspace/PRD.md`, `.workspace/DESIGN_BRIEF.md`, `.workspace/API_REQUIREMENT.md` — read once, deleted together when the kickoff spec's tickets are all done | None. Only `.workspace/` when the user chose `brainstorm`, `discuss-with-docs`, `prototype`, `investigate`, `research`, `audit`, or `triage`; kept out of the remote via `.git/info/exclude` |
| Design rules | `DESIGN.md`, written by `designing` | The components and theme already in the code |
| Tests | `CONTEXT.md` `tests: acceptance`: an acceptance test per criterion before code; red-green per step; new suite green at the end. `tests: none`: as legacy | None by default. The user says at the start of `implement` how the change is verified |
| Standards | `CONTEXT.md` conventions, then neighbouring code | Documented conventions, then neighbouring code |
| Tickets | `.workspace/<issue-name>/tickets/` beside the spec, or GitHub Issues, as `CONTEXT.md` says | The user's tracker; no ticket files here. Exception: tickets cut from an `audit` spec live in `.workspace/audit/tickets/` or GitHub Issues, as the user chose when `write-tickets` asked |
