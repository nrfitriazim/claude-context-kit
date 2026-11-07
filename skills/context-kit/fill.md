# `context kit`

Goal: the project's `context/` folder, every file filled from the approved design, self-reviewed, and handed to the user for approval. Every write in this command goes inside `context/`, plus one short pointer section in `CLAUDE.md`.

## 0. Check the starting point

Take the first case that matches:

- **No approved design in this conversation**: tell the user the files are filled from a discussion, not guessed, and run `discuss.md`, picking up wherever an earlier discussion stopped. Come back here once every section is approved.
- **The project already has a filled `context/`**: this is a new feature, and the existing files are kept. It needs its own approved discussion first. Then write its spec, `F-NN` with the next free number, and edit only the parts of other files the feature changes: its row in `progress-tracker.md`, a scope line in `project-overview.md`, a new tool in `architecture.md`.
- **The project has `context/` with blank templates in it**: fill those in place.
- **Otherwise**: a fresh fill.

## 1. Write the files

Read each template from this skill's `context/` and write the filled version to the project's `context/` under the same name:

- `project-overview.md`, `architecture.md`, `code-standards.md`, `design.md`, `ui-context.md`, `ai-workflow-rules.md`, `progress-tracker.md`
- `feature-specs/_template.md`, copied unchanged: it is the blank for future specs
- `feature-specs/F-01-<short-name>.md` and onwards, one per approved first feature, from the template

Then give later sessions the way in: add this section to the project's `CLAUDE.md` (create the file if it is missing; append if it exists, leaving its other text as it is; skip if the section is already there):

```markdown
## Context kit

This project is spec-driven. Before any work, read `context/progress-tracker.md`, then the spec for the feature at hand in `context/feature-specs/`. Build only against specs whose Status is `Approved`, one feature at a time, following `context/ai-workflow-rules.md`. A spec still in `Draft` waits for the user's approval: say so, and point them to what to review.
```

### Filling rules

- Every bracketed placeholder `[…]` becomes project content. Bracketed guidance (notes to whoever fills the file) is removed once its section is filled, and bracketed optional items that don't apply are removed.
- Unbracketed template text is the method, and stays word for word: the workflow depth table and its rules, the testing table and rules, the ❓ note, the input coverage and missing-requirement rules.
- A section that doesn't apply keeps its heading plus one line saying why (`No UI: command-line tool.`). Rename the `TypeScript` section to the project's language when it differs.
- Product facts use the user's own words. Defaults the user approved are written as decided.
- Anything the discussion never settled becomes one of two things. A product or money question goes to `progress-tracker.md` → Open Questions. A value a spec needs before it can be built goes into that spec's Decisions as `D-n ⚠️ Assumed (<date>, awaiting approval)`, with a matching line in Open Assumptions. An assumption no single feature owns (hosting terms, a vendor's sign-up rules) goes into the first spec that depends on it. A ❓ in a value table always sits beside one of these.
- Dates are absolute, `YYYY-MM-DD`, today's date unless the discussion gave another.

### File by file

- **`project-overview.md`**: design sections 1 and 2. Feature overrides list each feature raised above the project's level: in a project below GA, every feature that takes money is raised to GA. When nothing is raised (a GA project, say), write one line saying so, and each spec's Depth then says it inherits the project level.
- **`architecture.md`**: section 3. In Skills, write one line saying the skill check has not run yet and runs after approval (it looks up vendors' repos online, so it waits for the user's go-ahead), then list the stack tools it will check. The table keeps one row: `Not run yet`.
- **`code-standards.md`**: conventions for the chosen stack. Testing names real tools and commands for that stack, and keeps the full "What gets tested" table and rules; the project's level is the row that applies, and GA features use the GA row.
- **`design.md`, `ui-context.md`**: section 4. Token values are concrete and follow from the approved direction (mood, references, brand colours). They stay proposals until the design system page is approved, so the Approval Log says: `<date> — Direction approved in discussion; token values proposed, approval due on the design system page.` In Design System Page, keep the variant of Where that fits the stack.
- **`ai-workflow-rules.md`**: Approach is one paragraph for this project. When to Split Work, Protected Files and the build command come from the stack.
- **`progress-tracker.md`**: Current Phase `Specs drafted, awaiting approval`. Current Goal: the user approves the specs. Features: every feature in `project-overview.md` gets an `F-NN` row with status `Draft` (`Not specced` for features without a spec yet) and its depth. Next Up: the design system page first when there is a UI, then `F-01`. Open Questions and Open Assumptions: every one from the discussion and the specs. Architecture Decisions: the chosen approach and why, and each rejected approach and why. Session Notes: where things stand, so a new session can resume.
- **`feature-specs/F-NN-<short-name>.md`**: Status line shows the current status only: `Status: Draft`. Depth is the project's level, or GA when the feature takes money. Acceptance criteria are the approved ones with their IDs. Where Each Value Comes From lists every value the feature shows, computes or stores, each with its source; that table is the input coverage check. Decisions: `✅ Accepted` for what the discussion settled, `⚠️ Assumed` for the rest. Verification has one line per AC: `AC-n ⬜ not checked yet — <how it will be checked at this depth>`.

## 2. Self-review

Re-read every file you wrote, then run all four checks. Fix what fails and run all four again. Done when one full pass finds nothing to fix. `feature-specs/_template.md` is exempt: it stays blank.

1. **No placeholders.** Search the written files for `[`. Every hit is a real Markdown link, a checkbox or code, never template text. No `TODO`, `TBD`, `#[hex]`, or template example (`e.g. …`) standing in for a real value.
2. **One story across files.** No contradictions:
   - The project name, the depth level and the stack read the same in every file.
   - Every feature in `project-overview.md` → Features has a row in `progress-tracker.md` → Features; every spec file has a row; statuses match.
   - Each spec's Depth matches its row in `progress-tracker.md` and the level or Feature overrides in `project-overview.md`. Anything that takes money is GA in all three places.
   - Nothing under Out of Scope shows up as a feature or an AC.
   - The folders in `architecture.md` → System Boundaries match `code-standards.md` → File Organization.
   - The testing tools and commands fit the stack, and the build command in `ai-workflow-rules.md` is a real command for it.
   - Every `⚠️ Assumed` in a spec has its line in Open Assumptions, and every line there points back to a spec decision.
   - Every ❓ in a value table has its `⚠️ Assumed` decision or Open Question.
   - Every success criterion is covered by at least one AC, or says it is checked after launch.
   - The tokens in `ui-context.md` fit the mood and Do / Don't in `design.md`.
3. **Readable one way.** Someone who missed the discussion can check each AC as pass or fail: a concrete actor, action and observable result. Words like fast, simple, nice or user-friendly carry a number or an example.
4. **Traceable.** Every product fact came from the discussion or an approved default; anything else is a logged assumption.

## 3. Hand over for approval

Tell the user, briefly:

- the files written, with one line each on what it holds, and the pointer section added to `CLAUDE.md`
- the open questions and assumptions that need their call
- where to start reading: `project-overview.md`, then `F-01`

Then state the gate in your own words: no code until they approve these specs. They can ask for changes (edit the files, run the self-review again) or approve.

While the specs wait for approval, a request to start coding gets one reminder: approval comes first, here is the quickest way to review (the few sections that matter most), and here is what is still open. The reminder offers one way forward, which is review and approve. The user's explicit approval opens the gate ("approved", "ok, build F-01"). It is their project, so if they still insist on building after that reminder, treat it as approval and log in `progress-tracker.md` → Session Notes that the specs were approved without review.

On approval: set each approved spec's Status to `Approved` and its row in `progress-tracker.md` to match, set Current Phase to `Specs approved`, and log the date in Session Notes. Offer the skill check before the first build, then build one feature at a time by the project's `context/ai-workflow-rules.md`.
