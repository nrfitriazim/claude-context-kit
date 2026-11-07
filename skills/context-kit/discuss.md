# `discuss [idea]`

Goal: a design the user approved section by section, or an honest decision not to build it. The discussion writes no files.

## 1. Look before asking

If the user typed `discuss` with no idea, ask for it in one line.

If the working folder has anything in it (code, a README, git history, a brief, notes, a `context/` folder), read it first. Skip any question those files already answer. If `context/` is already filled, this discussion is about one new feature: read the context files and aim every question at that feature.

Then restate the idea in one or two sentences so the user can correct it early.

## 2. Questions, one at a time

One question per message, then wait. Number them (`1 / 6`); the total is your estimate and may change. Prefer questions the user can answer by picking: 2–4 options, your recommended one first with a one-line reason. They can always answer in their own words.

Before each question, look at the coverage table and ask about the most important row still open. Rows that need neither the user's facts nor their taste get no question: propose a default in the design instead, where approving it costs one word.

| Row             | What you need                                                                 | Fills                                        |
| --------------- | ----------------------------------------------------------------------------- | -------------------------------------------- |
| Who and problem | Who uses it, and what pain it removes                                          | `project-overview.md` → Overview, Goals      |
| Core flow       | The one thing a user must be able to do, end to end                           | Core User Flow, the first spec               |
| v1 scope        | What is in, and what is explicitly out                                        | Scope                                        |
| Money, editors  | Does it take money? Who edits content after launch?                           | Workflow Depth                               |
| Success         | How the user will know v1 worked                                              | Success Criteria                             |
| Constraints     | Deadline, budget, hosting, a stack already chosen, the builder's experience  | Stack, the approaches                        |
| Look (UI only)  | 1–3 references with what to take and not take from each, mood words, brand assets that exist | `design.md`, `ui-context.md`  |

Done when every row is answered or has a default ready to propose. That is usually 4–8 questions; stop asking as soon as you could write the design.

## 3. Two or three approaches

Offer 2–3 genuinely different ways to build it: a different shape, stack or scope, not one idea spelled three ways. For each: one line on what it is, then the trade-offs (time, cost, complexity, what it rules out later). Mark one **Recommended** and give the reason in one sentence tied to the user's answers. Wait for their pick.

The rejected approaches and why they lost go into the design: they end up in `progress-tracker.md` → Architecture Decisions.

## 4. The design, section by section

Show one section per message and wait for approval before the next. Fold changes in and re-show only what changed. Mark the defaults you chose for unasked rows, so the user sees what they are approving.

| # | Section        | Holds                                                                                       | Becomes                                |
| - | -------------- | ------------------------------------------------------------------------------------------- | -------------------------------------- |
| 1 | Product        | Overview, goals, core flow, features, in and out of scope, success criteria                 | `project-overview.md`                  |
| 2 | Depth          | The workflow depth level and why; every feature raised to GA because it takes money          | `project-overview.md` → Workflow Depth |
| 3 | Architecture   | Stack, system boundaries (folders), storage, auth and access, invariants, testing tools      | `architecture.md`, `code-standards.md` |
| 4 | Look (UI only) | References with take and don't take, mood, brand assets, theme direction                     | `design.md`, `ui-context.md`           |
| 5 | First features | The first 1–3 features as `F-01`…, each with 2–4 acceptance criteria (`AC-1`…), each one observable and checkable on its own | `feature-specs/` |

For section 2, show the Workflow Depth table and its two rules from the template `context/project-overview.md` beside this skill, and place the project on it.

Done when every section is approved. Then send a short recap: each approved section in a few lines, the open questions, anything still assumed, and the language the files will be written in (the discussion's, unless the user asks for another). End by telling the user the next step is `context kit`.

## The idea is allowed to die

At any point, if the answers show the idea already exists, cannot fit the constraints, or no longer interests the user, say so plainly and offer to stop. Dropping an idea before any code is written is a good outcome.

Pivots are normal too: fold the new direction in and carry on, leaving settled sections settled.
