# claude-context-kit

**Discuss first. Spec second. Code last.**

A Claude Code skill plus seven context templates for starting a project the spec-first way: talk the idea through, write down what to build, approve it, and only then let Claude write code.

## Quick start

Ask Claude to "build me an app" and it guesses everything you didn't say, then the app breaks. This kit turns that around: discuss first, write the spec, approve it, and only then does Claude write code.

1. **Install** once: [copy the skill folder](#install) into `~/.claude/skills/`. The seven templates come with it.
2. **`discuss [idea]`** in your project folder, for example `discuss a pre-order page for my mum's kuih raya`. Claude asks one question at a time, offers 2–3 approaches with one recommended, and shows the design section by section for you to approve. If the idea doesn't hold up, you stop there, and no code is wasted.
3. **`context kit`**: Claude fills the seven files in `context/` and the first feature spec (`F-01`) from your answers, checks its own work (no placeholders, no contradictions), and waits for your approval.
4. **Approve the specs**, and Claude writes code: one feature at a time, against the acceptance criteria (`AC-1`, `AC-2`…) in its spec. The ACs are the contract.

Anything that takes money is **GA**, the strictest level of checks.

## What it is

```
skills/context-kit/
├── SKILL.md          the two commands and the gate
├── discuss.md        how `discuss [idea]` runs
├── fill.md           how `context kit` fills and checks the files
└── context/          the blank templates, copied into your project
    ├── project-overview.md
    ├── architecture.md
    ├── code-standards.md
    ├── design.md
    ├── ui-context.md
    ├── ai-workflow-rules.md
    ├── progress-tracker.md
    └── feature-specs/_template.md
```

Two commands, one gate:

| Command          | What happens                                                                                     | Writes          |
| ---------------- | ------------------------------------------------------------------------------------------------ | --------------- |
| `discuss [idea]` | Questions one at a time, 2–3 approaches with a recommendation, the design approved section by section. The idea is allowed to die here. | Nothing |
| `context kit`    | The seven context files and the first feature specs, filled from the discussion, self-reviewed, handed to you for approval. | `context/`, plus a short pointer in `CLAUDE.md` |

**The gate:** no code until you approve the filled specs.

## Why spec-first

- **Guesses become decisions.** Everything Claude would have guessed is asked, proposed as a default you approve, or logged as `⚠️ Assumed`. It lives in the repo, not in a chat you will lose.
- **Acceptance criteria are the contract.** Every build task serves an AC, and every check points back to one. "Done" means every AC checked, not "looks done".
- **Gaps show up before code.** Every value a feature shows or computes names its source. A ❓ means a decision is owed, and you find out before the build, not after.
- **Ideas can die cheaply.** A discussion that ends in "not worth building" costs minutes. A half-built app costs a weekend.
- **Any session can pick up.** The next session, or the next person, reads `context/` and knows what is built, what is next and what is still open.

## Install

The skill is plain Markdown. There is nothing to run and it needs no network access.

Clone this repo, then copy the skill folder. The templates travel inside it.

**For every project** (your user skills):

```bash
mkdir -p ~/.claude/skills && cp -r claude-context-kit/skills/context-kit ~/.claude/skills/
```

**For one project** (committed with the repo, so teammates get it too):

```bash
mkdir -p .claude/skills && cp -r /path/to/claude-context-kit/skills/context-kit .claude/skills/
```

**Windows (PowerShell):**

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null; Copy-Item -Recurse claude-context-kit\skills\context-kit "$HOME\.claude\skills\"
```

To update, pull this repo and copy the folder again.

## Use

### `discuss [idea]`

Run it in the project folder. If the folder already has code or docs, Claude reads them first and skips the questions they answer.

1. **Questions, one at a time.** Numbered (`1 / 6`), usually 4–8 of them, mostly pick-one with a recommended option. They cover who it is for, the core flow, what is in and out of v1, whether it takes money, what success looks like, your constraints, and the look if it has a UI.
2. **Two or three approaches**, with trade-offs and one marked Recommended. You pick.
3. **The design, section by section:** Product, Depth, Architecture, Look, First features. You approve each one before the next.

Nothing is written during the discussion.

### `context kit`

Turns the approved design into the project's `context/` folder: the seven files, plus one spec per first feature (`feature-specs/F-01-….md`). Claude then reviews its own output (no placeholders, no contradictions between files, every AC checkable as pass or fail) and hands it to you.

It also adds a short "Context kit" section to the project's `CLAUDE.md`, so every later session reads the tracker and specs first and builds only against approved specs.

You read, ask for changes, and approve. Until then, Claude writes nothing outside `context/` apart from that pointer.

Typed `context kit` without a discussion? Claude starts the discussion first. The files are filled from your answers, never guessed.

### Later features

In a project whose `context/` is already filled, run `discuss [feature]` for the new feature, then `context kit`. Claude adds the next spec (`F-02`, `F-03`…) and updates the tracker, leaving the other files as they are.

## The seven files

| File                   | Owns                                                                                       |
| ---------------------- | ------------------------------------------------------------------------------------------ |
| `project-overview.md`  | What, for whom, goals, core flow, in and out of scope, success criteria, **workflow depth** |
| `architecture.md`      | Stack, system boundaries, storage model, auth, **skills**, invariants                      |
| `code-standards.md`    | Language and framework conventions, API rules, **testing**, file organization              |
| `design.md`            | Art direction: references (take / don't take), mood, brand assets, imagery, do / don't, approval log |
| `ui-context.md`        | Tokens (color, type scale, spacing, radius, shadows), component states, layout, motion, **design system page** |
| `ai-workflow-rules.md` | Scoping rules, input coverage check, missing-requirement rules, done criteria, skill check |
| `progress-tracker.md`  | Current phase and goal, feature status, open questions, **open assumptions**, decisions    |
| `feature-specs/`       | One spec per feature from `_template.md`: IDed acceptance criteria, where each value comes from, decisions, verification |

## How work flows

1. **Spec.** Each feature gets `feature-specs/F-NN-name.md`. Its acceptance criteria (`AC-1`, `AC-2`…) are the contract.
2. **Input coverage check.** Before building, every value the feature shows or computes names its source. A ❓ means a decision is owed: ask, or build on an assumption logged as `⚠️ Assumed` in the spec and in `progress-tracker.md`.
3. **Build** against the spec only, one feature at a time.
4. **Verify** every AC the way the project's workflow depth requires, with a dated line in the spec.

## Workflow depth

How hard each feature gets checked. The level is set during the discussion and lives in `project-overview.md`.

| Level         | Used for                              | Checks (each adds to the one above)                                                   |
| ------------- | ------------------------------------- | ------------------------------------------------------------------------------------- |
| **Prototype** | Prototypes, practice builds           | Build, then screenshot and look at it                                                 |
| **Alpha**     | Brochure / content sites              | + every AC checked on staging/live, dated                                             |
| **Beta**      | Someone edits content via admin / CMS | + automated smoke test on the live site (throwaway accounts the script creates and deletes) |
| **GA**        | Anything that takes money             | + payment-path audit + code review + security review before launch + one real paid order checked end to end |

- **The money path is always GA**, even inside a lower-level project.
- **Levels only go up mid-project, never down silently.** A prototype that becomes the real build moves up, and its checks catch up before launch.

### Testing

Tools, commands and what each level tests live in `code-standards.md` → Testing. Every test names its AC (`test('AC-2: …')`), every bug fix starts with a regression test, and tests that write data run on staging. Live gets read-only or self-cleaning checks only.

## Design system page

`design.md` holds the direction and `ui-context.md` holds the tokens. Both are rendered on one design system page, approved before pages are built: inside the app when there is one (real components, so it cannot drift), or a standalone `context/design-system.html` when there is no app to host it.

## Skill check

When the stack is decided, and again whenever a new tool joins the project, Claude looks for the vendor's official agent skill for each tool (community skills only when there is no official one), reads it before proposing it, and shows you a table: skill, vendor, whether it runs code, size, recommendation. Nothing installs without your approval. An install is a copy of the reviewed files into the repo's `.claude/skills/`, pinned by commit SHA in `architecture.md` → Skills. The full steps are in `ai-workflow-rules.md`.

## Without Claude Code

The templates are plain Markdown. Copy `skills/context-kit/context/` into any repo and fill it by hand or with any AI tool; `discuss.md` and `fill.md` describe the method step by step.

## License

[MIT](LICENSE). Made by Azim.
