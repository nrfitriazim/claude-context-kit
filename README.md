# claude-context-kit

**Discuss first. Spec second. Code last.**

A Claude Code skill plus seven context templates for starting a project the spec-first way: talk the idea through, write down what to build, approve it, and only then let Claude write code.

## Quick start

Ask Claude to "build me an app" and it guesses everything you didn't say, then the app breaks. This kit turns that around: discuss first, write the spec, approve it, and only then does Claude write code.

1. **Install** once: [copy the skill folder](#install) into `~/.claude/skills/`. The seven templates come with it.
2. **`discuss [idea]`** in your project folder, for example `discuss a pre-order page for my mum's kuih raya`. Claude asks one question at a time, offers 2–3 approaches with one recommended, and shows the design section by section for you to approve. If the idea doesn't hold up, you stop there, and no code is wasted.
3. **`context kit`**: Claude fills the seven files in `context/` and the first feature spec (`F-01`) from your answers, checks its own work (no placeholders, no contradictions), and waits for your approval.
4. **Approve the specs**, and Claude writes code: one feature at a time, against the acceptance criteria (`AC-1`, `AC-2`…) in its spec. The ACs are the contract.

Anything that takes money or keeps sensitive personal data is **GA**, the strictest level of checks.

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
| `context kit`    | The seven context files and the first feature specs, filled from the discussion, self-reviewed, handed to you for approval. | `context/`, plus a short pointer in `CLAUDE.md` (or your tool's own instructions file) |

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

**Codex or Gemini CLI** (one project; see [Without Claude Code](#without-claude-code) for how far each was tested):

```bash
mkdir -p .agents/skills && cp -r /path/to/claude-context-kit/skills/context-kit .agents/skills/
```

Gemini CLI loads a project's skills only after you trust the folder, which it asks the first time you run it there.

To update, pull this repo and copy the folder again.

## Use

### `discuss [idea]`

Run it in the project folder. If the folder already has code or docs, Claude reads them first and skips the questions they answer.

1. **Questions, one at a time.** Numbered (`1 / 6`), usually 4–8 of them, mostly pick-one with a recommended option. They cover who it is for, the core flow, what is in and out of v1, whether it takes money or keeps sensitive personal data, what success looks like, your constraints, and the look if it has a UI, including whether to design in Figma first or go straight to code.
2. **Two or three approaches**, with trade-offs and one marked Recommended. You pick.
3. **The design, section by section:** Product, Depth, Architecture, Look, First features. You approve each one before the next.

Nothing is written during the discussion.

### `context kit`

Turns the approved design into the project's `context/` folder: the seven files, plus one spec per first feature (`feature-specs/F-01-….md`). Claude then reviews its own output (no placeholders, no contradictions between files, every AC checkable as pass or fail) and hands it to you.

It also adds a short "Context kit" section to the project's instructions file (`CLAUDE.md` in Claude Code, `AGENTS.md` in Codex, `GEMINI.md` in Gemini CLI), so every later session reads the tracker and specs first and builds only against approved specs.

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

| Level         | Used for                                                     | Checks (each adds to the one above)                                                   |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
| **Prototype** | Practice builds, demos, throwaway experiments                | Build, run it, and look at it                                                         |
| **Alpha**     | Real users, but the content only changes when the code does  | + every AC checked where it runs (staging or live), dated                             |
| **Beta**      | Others change content or data after launch (an admin, a CMS, user accounts) | + automated smoke test against the running app (throwaway accounts and data the script creates and deletes) |
| **GA**        | A mistake costs someone money or exposes their sensitive personal data | + code review + security review before launch + the checks for each risk below |

GA has two risks, each with its own checks:

- **Money** (payments, subscriptions, deposits, payouts): money logic runs on the server, a forged "paid" notification is rejected, and one real payment is checked end to end before launch.
- **Sensitive personal data** (ID numbers, health, finances, exact location, children's data, grades, HR files): each person reaches only their own records (tested for every role), only what a feature uses is collected, a privacy notice says what is kept and why, a person can get, correct and delete their records, and a backup restore is tried before launch. The discussion names the data protection law that applies (GDPR, PDPA…). A name, an email and a sign-in on their own are not a GA risk.

These are engineering checks, not legal advice.

- **Money and sensitive personal data are always GA**, even inside a lower-level project.
- **Levels only go up mid-project, never down silently.** A prototype that becomes the real build moves up, and its checks catch up before launch.

### Testing

Tools, commands and what each level tests live in `code-standards.md` → Testing. Every test names its AC (`test('AC-2: …')`), every bug fix starts with a regression test, and tests that write data run on staging. Live gets read-only or self-cleaning checks only.

## Design system page

`design.md` holds the direction and `ui-context.md` holds the tokens. Both are rendered on one design system page, approved before pages are built: inside the app when there is one (real components, so it cannot drift), or a standalone `context/design-system.html` when there is no app to host it.

### Figma first, or code first

The discussion asks how you want to work:

- **Code first** (the default for solo builds and prototypes): the look is approved on the design system page.
- **Figma first** (when a client expects mockups, or you already design in Figma): each feature's screens are approved in Figma before its code is written, the tokens come from your Figma variables, and each spec links its frames. Claude then asks who makes the screens: you or your designer (Claude reads them), or Claude drafting them in Figma for you to approve. For Claude to read or draft in Figma, connect a Figma MCP server to Claude Code; without one, you make the screens and share links or screenshots.

## Skill check

When the stack is decided, and again whenever a new tool joins the project, Claude looks for the vendor's official agent skill for each tool (community skills only when there is no official one), reads it before proposing it, and shows you a table: skill, vendor, whether it runs code, size, recommendation. Nothing installs without your approval. An install is a copy of the reviewed files into the repo's `.claude/skills/`, pinned by commit SHA in `architecture.md` → Skills. The full steps are in `ai-workflow-rules.md`.

## With Superpowers

This kit's discussion step takes its shape from the brainstorming skill in [Superpowers](https://github.com/obra/superpowers) (see [Credits](#credits)), so the first half overlaps: questions one at a time, approaches, a design you approve, no code before that. The difference is what stays behind. Superpowers writes a design doc and a plan for each piece of work, then drives the build with test-driven development, subagents and code review. This kit writes the project's standing context (the seven files, IDed acceptance criteria, where each value comes from, assumptions, workflow depth) and stops at approved specs. How the code gets written is left to you, or to Superpowers.

They work together. Tested with both installed in one project (Superpowers 7.0.0, Claude Code 2.1.319, Claude Opus 5.5):

- `discuss [idea]`, and a plain "let's plan it properly before any code", ran this kit's discussion in 3 of 3 runs.
- After the design was approved, Claude pointed to `context kit` rather than a Superpowers plan, and `context kit` wrote the files as usual.
- Asked to build an approved spec, Claude followed the spec and the project's workflow rules. Superpowers' test-driven-development skill joined in for 2 of 3 runs. No run brainstormed an approved spec again.
- With the specs still in Draft, a new session refused to build.

So: plan with this kit, build with Superpowers. When its test-driven-development skill joins in, it writes tests first whatever the project's depth, so a Prototype may get more tests than its depth asks for.

## Without Claude Code

Codex and Gemini CLI read the same skill format. Tested on 2026-11-10, one run each, with the same idea (a student planner, asked in Malay):

- **Codex** (codex-cli 0.162.1, gpt-6-astra): found the skill in `.agents/skills/`, ran the discussion, and filled every file and spec. Levels, specs and the tracker agreed with each other. The `context kit` step took about 25 minutes at high reasoning effort, against about 6 in Claude Code. A second `context kit` run at medium effort took about 8 minutes and wrote its pointer to `AGENTS.md`.
- **Gemini CLI** (0.67.0, Gemini 3.1 Pro): found the skill and ran the discussion, but gave the project a depth level of its own instead of one of the kit's four. `discuss.md` now names the four levels; that fix is not re-tested in Gemini, and neither is `context kit` (the free quota ran out).

Any other tool: the templates are plain Markdown. Copy `skills/context-kit/context/` into any repo and fill it by hand or with any AI tool; `discuss.md` and `fill.md` describe the method step by step.

## Credits

- **The six-file idea** (project overview, architecture, code standards, UI context, AI workflow rules, progress tracker) comes from JS Mastery's [Six-File Context System](https://jsmastery.com/waitlist/six-file-context). The templates here are written in this kit's own words, and add `design.md`, feature specs with IDed acceptance criteria, where each value comes from, logged assumptions, risk-based workflow depth and the skill check.
- **The discussion step** takes its shape from the brainstorming skill in Jesse Vincent's [Superpowers](https://github.com/obra/superpowers): questions one at a time, a few approaches, a design approved section by section.

## License

[MIT](LICENSE). Made by Azim.
