# Skills

**Eighteen agent skills that turn a coding agent into a colleague who asks before it builds.**

```bash
npx skills add NickDabizaz/skills
```

Works with Claude Code, Codex, Cursor, and every other agent the [`skills`](https://skills.sh) CLI supports.

---

## Why this exists

Most work with a coding agent fails the same way. You describe a task in one paragraph, the agent silently guesses at everything you left out, and you spend the next hour undoing the guesses.

The problem is not the model. It is that the conversation skipped the part where a good colleague would have asked "who is this for?" and "what happens when it fails?" before touching the keyboard.

This set puts that part back. It is a chain of small skills, each with one job and a clear hand-off to the next:

```
widen the idea  →  settle the requirements  →  cut it into tickets  →  build  →  review
```

Every skill asks **one question at a time**, offers you options with a recommendation, and refuses to move on while a decision that would change the output is still open. Facts are the agent's job — it reads your codebase before it asks you anything. Decisions are yours.

---

## Quick start

```bash
# Recommended: pick your skills and your agents when prompted
npx skills add NickDabizaz/skills

# Browse what is in here without installing anything
npx skills add NickDabizaz/skills --list

# Take only the ones you want
npx skills add NickDabizaz/skills --skill discuss --skill implement --skill review

# Choose the agents yourself
npx skills add NickDabizaz/skills -a claude-code -a codex

# Install for every project instead of just this one
npx skills add NickDabizaz/skills -g
```

> **A note on `--all`.** It is shorthand for `--skill '*' --agent '*' -y`: every skill, **every agent the CLI can detect**, and no prompts. That writes `.claude/`, `.agents/`, `agent/` and a `skills-lock.json` into your folder in one go. Handy in CI, surprising on a laptop — prefer the plain command above and answer the prompts. Note also that when the CLI detects it is running inside an agent session, it goes non-interactive on its own and picks the agent for you.

Installed something you did not want? `npx skills list` shows what is there and `npx skills remove` takes it back out.

Then, in your agent, type the skill you need:

```
/ask-me   I have a bug but I don't know where it comes from
```

`/ask-me` is the only name you have to remember. It reads your situation and points you at the right skill, with the reason.

---

## The chain

```
                     ┌────────────────┐
   a vague idea  →   │   /brainstorm  │  →  a direction worth planning
                     └────────────────┘
                              ↓
                     ┌────────────────┐
   a known change →  │    /discuss    │  →  a settled plan
                     │       or       │
                     │  /discuss-     │
                     │   with-docs    │
                     └────────────────┘
                              ↓
                     ┌────────────────┐
                     │ /write-tickets │  →  one ticket per unit of work
                     └────────────────┘
                              ↓
                     ┌────────────────┐
                     │   /implement   │  →  code, verified
                     │       or       │
                     │ /implement-all │
                     └────────────────┘
                              ↓
                     ┌────────────────┐
                     │     review     │  →  Spec · Standards · Logic · UI/UX
                     └────────────────┘
```

Three side entrances join the same chain:

| You are starting from | Enter at |
| --- | --- |
| A bug whose cause is unknown | `/investigate` |
| A codebase that needs improving | `/audit` |
| A screen you cannot picture yet | `/prototype` |

---

## Walkthroughs

### 1. You have a hunch, not a plan

You want to build *something* around recurring payments, but you cannot yet say what.

```
/brainstorm  I keep losing track of my subscriptions, feels like there's something here
```

`/brainstorm` reads your repo first, then answers with three concrete directions — deliberately at different ambition levels, each solving a different problem for a different person. It never opens with questions, because you cannot answer abstract questions at this stage but you can always react to something concrete.

You react. Each round ends with one question: *go deeper on this one, or spread again from a new angle?* Rounds continue until the direction has all three of: who it is for, the problem it solves, and the smallest version already worth using.

```
→ .issues/subscription-tracker/ideas.md
```

Now the requirements:

```
/discuss-with-docs  .issues/subscription-tracker/ideas.md
```

Questions start, one per turn, until nothing is left open that would change what gets built. The confirmed plan lands as a spec beside your ideas.

```
→ .issues/subscription-tracker/spec.md
```

Then cut it up and build it:

```
/write-tickets  .issues/subscription-tracker/spec.md
/implement-all  .issues/subscription-tracker/spec.md
```

`/implement-all` reads the dependency graph, builds unblocked tickets in parallel on their own branches, resolves conflicts against the spec, merges into your target branch, and reviews the whole diff at the end.

---

### 2. You have a ticket from your company's tracker

No `CONTEXT.md` in the repo, so the set runs in **legacy mode**: it writes no documents into your company's codebase and imposes no test discipline you did not ask for.

```
/discuss

  PROJ-482 — Users report the export button does nothing on Safari.
  Acceptance: export works on Safari 16+.
```

The interview fills in what the ticket left open and adds nothing it did not ask for. The plan stays in the conversation — nothing is written to disk.

```
/implement
```

Before the first change, `/implement` asks how this run should be verified: lint and typecheck plus a traced logic check, the existing tests nearest the change, or characterization tests written first. Your answer is the standard for the run. When every step's done-condition holds, it calls `review` by itself, fixes what comes back, and re-reviews — three rounds at most.

---

### 3. Something is broken and you don't know why

```
/investigate  Checkout total is off by one cent, but only for orders with a discount
```

`/investigate` reproduces the bug on demand first — a test, a script, a command. Then it traces from the symptom to the line that causes it. A hypothesis counts as confirmed only when changing that one thing changes the symptom; candidates it rules out are reported with the reason.

It never fixes. You get a proven cause, every other caller that runs through the same code, and a fix plan — then it routes: `/write-tickets` when the fix is heavy, `/implement` when it is one clear change.

---

### 4. The codebase needs work, but you don't know where to start

```
/audit  src/billing
```

`/audit` reads every module in scope and judges it on four themes: readability, structure and architecture, efficiency, and current practice for the stack. It reports in **your language**, with code, options, and the trade-off per finding.

```
→ .issues/audit/report.html   (open it in a browser)
→ .issues/audit/spec.md       (feed it to /write-tickets)
```

A pattern repeated in five files is one finding with five locations, not five findings. Anything a formatter would fix is left out.

---

## The two modes

Whether a repo has a `CONTEXT.md` at its root decides how every skill behaves.

|  | **Own project** (`CONTEXT.md` present) | **Legacy** (no `CONTEXT.md`) |
| --- | --- | --- |
| Where work comes from | A spec, split into tickets | A ticket you paste from your tracker |
| Documents written | `CONTEXT.md`, `DESIGN.md`, `CLAUDE.md` / `AGENTS.md`, `.issues/` — all gitignored | None, beyond `.issues/` when you ask for it (kept out of the remote via `.git/info/exclude`) |
| Tests | An acceptance test per criterion, written before the code, red-green per step | Whatever you choose at the start of `/implement` |
| Design rules | `DESIGN.md` | The components already in the code |

Run `/setup-new-project` (empty repo) or `/setup-project` (existing code) once to make a repo an own project. `/setup-project` reads your stack, commands, conventions, and tests from the code and asks only what the code cannot say — and where there is no test suite, it never imposes one.

---

## Where work lives

Each piece of work is one folder that disappears when its last ticket is done:

```
.issues/
  subscription-tracker/
    ideas.md                      written by /brainstorm
    spec.md                       written by /discuss-with-docs
    tickets/
      01-subscription-model.md    written by /write-tickets
      02-import-statements.md     ticked and closed by /implement
      03-renewal-reminders.md
```

`.issues/` is gitignored in an own project, and kept out of the remote via `.git/info/exclude` in a legacy repo. Nothing here ever reaches a pull request.

---

## Skill reference

**You type these:**

| Skill | Job |
| --- | --- |
| [`/ask-me`](.claude/skills/ask-me/SKILL.md) | Describe your situation, get pointed at the right skill with the reason. |
| [`/setup-new-project`](.claude/skills/setup-new-project/SKILL.md) | Interview once; write `CONTEXT.md`, `DESIGN.md`, and the instruction file for an empty repo. |
| [`/setup-project`](.claude/skills/setup-project/SKILL.md) | The same documents for a repo that already has code, read from the code first. |
| [`/brainstorm`](.claude/skills/brainstorm/SKILL.md) | Widen a raw idea: three directions a round until one is clear enough to plan. |
| [`/discuss`](.claude/skills/discuss/SKILL.md) | Settle a plan one question at a time. Stays in the conversation. |
| [`/discuss-with-docs`](.claude/skills/discuss-with-docs/SKILL.md) | The same interview, written to `spec.md` for tickets, later sessions, and review. |
| [`/prototype`](.claude/skills/prototype/SKILL.md) | Clickable self-contained HTML: three options to choose from, or one refined page. |
| [`/investigate`](.claude/skills/investigate/SKILL.md) | Prove a bug's root cause with evidence, then route the fix. |
| [`/audit`](.claude/skills/audit/SKILL.md) | Report where a codebase can improve, as HTML plus a spec. |
| [`/write-tickets`](.claude/skills/write-tickets/SKILL.md) | Split a spec into tickets with criteria, checklist, and blockers — local files or GitHub Issues. |
| [`/implement`](.claude/skills/implement/SKILL.md) | Build one ticket or one plan on the current branch, then hand off to review. |
| [`/implement-all`](.claude/skills/implement-all/SKILL.md) | Build every open ticket in parallel, one branch each, merged and reviewed as a whole. |

**The agent calls these:**

| Skill | Job |
| --- | --- |
| [`review`](.claude/skills/review/SKILL.md) | Check a diff on Spec, Standards, Logic & Security — plus UI/UX when the diff is visible. Reports; never edits. |
| [`discussing`](.claude/skills/discussing/SKILL.md) | The shared interview loop behind every discuss entry point. |
| [`implementing`](.claude/skills/implementing/SKILL.md) | The shared build loop behind `/implement` and `/implement-all`. |
| [`designing`](.claude/skills/designing/SKILL.md) | Write or complete `DESIGN.md`, by interview or by extraction from existing code. |
| [`resolve-conflicts`](.claude/skills/resolve-conflicts/SKILL.md) | Resolve merge conflicts using the spec and both tickets as the reference. |
| [`writing-for-agents`](.claude/skills/writing-for-agents/SKILL.md) | The rules every document here follows. Use it to write your own. |

---

## How it thinks

A few rules run through every skill. They are what make the set feel different from prompting.

- **One question per turn.** Two to four options, one marked recommended with the reason, and you are always free to answer outside them. A wall of questions gets skimmed; one question gets answered.
- **Facts are the agent's job.** A question whose answer is already in your codebase is never asked. The agent reads `CONTEXT.md`, the conventions, and the code around the change before it opens its mouth.
- **Every step ends on a checkable condition.** Not "understanding reached" but "no open decision would change what gets built". Vague completion criteria are how agents stop early.
- **Review reports; it never edits.** Findings go back to `/implement`, which fixes them and asks for another review. Three rounds at most, then whatever is left comes to you.
- **New code takes the shape of its neighbours.** And when a neighbour is clearly flawed, that becomes a question rather than a pattern to copy.
- **Nothing is committed unless you ask.** No automatic commits, no automatic pull requests.

---

## Repository layout

```
.claude/skills/<name>/SKILL.md               Claude Code
.claude/skills/<name>/agents/openai.yaml     Codex metadata
.agents/skills/<name>/                       the same tree, for Codex and others
```

Both trees hold the same skills; the `skills` CLI reads either one and installs to whichever agents you have. Reference files (`MODES.md`, `TICKET-FORMAT.md`, `SPEC-FORMAT.md`, `REPORT-FORMAT.md`, `DESIGN-FORMAT.md`, `CONTEXT-FORMAT.md`) sit beside the skill that owns them and are pointed at from every skill that shares them.

### Manual install

- **Claude Code, every project:** copy each skill folder into `~/.claude/skills/`
- **Codex and other agents:** copy each skill folder into `.agents/skills/` (repo) or `~/.agents/skills/` (user)

---

## Adding your own skill

Call `writing-for-agents` — it carries the naming rules, the layout, and the pruning pass every document here has been through. In short:

- A core skill is one bare verb (`discuss`); a variant of it adds a suffix (`discuss-with-docs`).
- A loop that several skills share is a gerund (`discussing`).
- A supporting skill is verb plus object (`resolve-conflicts`).
- Every skill ships an `agents/openai.yaml` so it works outside Claude Code.
- Every new skill gets a row in `ask-me` and in this README, in the same change.

---

## License

MIT
