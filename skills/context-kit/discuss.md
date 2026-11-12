# `discuss [idea]`

Goal: a design the user approved section by section, or an honest decision not to build it. The discussion writes no files.

## 1. Look before asking

If the user typed `discuss` with no idea, ask for it in one line.

If the working folder has anything in it (code, a README, git history, a brief, notes, a `context/` folder), read it first. Skip any question those files already answer. If `context/` is already filled, this discussion is about one new feature: read the context files and aim every question at that feature.

Then restate the idea in one or two sentences so the user can correct it early.

## 2. Questions, in rounds

Ask in rounds. A round holds every question you can ask now: each open row of the coverage table below whose answer does not depend on another row that is still open. A question that needs an answer you have not heard yet waits for a later round. Most discussions take two or three rounds of 2–5 questions.

Number the questions across the whole discussion (`Q1`, `Q2`, and on into later rounds), so the user can reply by number: "1 yes, 2 B, 3 not sure". Give each question a short title, then the question, then 2–4 options when picking works, then your recommendation on its own line, worded so that "yes" accepts it, with a one-line reason. The user can always answer in their own words. Send the round, then wait for the answers.

```
**Q1 · Who it is for**: who opens this, and what do they do today instead?
A. …  B. …  C. …
➡️ A, because …
```

Rows that need neither the user's facts nor their taste get no question: propose a default in the design instead, where approving it costs one word. A row the idea or the folder already answers is not asked either; restate it in one line so the user can correct it. Some answers only the user has (a deadline, a budget): ask those plainly, with an example answer instead of a recommendation.

Facts are yours to find; decisions are the user's. When a question needs a fact you can look up (the folder, the docs, a vendor's pricing page), look it up before you send the round and put what you found in the question. When the lookup would take long, send the rest of the round first; only the questions that depend on that fact wait.

After each round, see what the answers opened or closed. A settled row can open a follow-up (Figma first opens who makes the screens), and a pivot can reopen rows you thought were done. The next round is whatever is open now.

| Row             | What you need                                                                 | Fills                                        |
| --------------- | ----------------------------------------------------------------------------- | -------------------------------------------- |
| Who and problem | Who uses it, and what pain it removes                                          | `project-overview.md` → Overview, Goals      |
| Core flow       | The one thing a user must be able to do, end to end                           | Core User Flow, the first spec               |
| v1 scope        | What is in, and what is explicitly out                                        | Scope                                        |
| Risk, editors   | Does it take money or keep sensitive personal data? Who changes content or data after launch? | Workflow Depth                 |
| Success         | How the user will know v1 worked                                              | Success Criteria                             |
| Constraints     | Deadline, budget, hosting, a stack already chosen, the builder's experience  | Stack, the approaches                        |
| Look (UI only)  | 1–3 references with what to take and not take from each, mood words, brand assets that exist | `design.md`, `ui-context.md`  |
| Design source (UI only) | Figma first or code first, and for Figma first, who makes the screens (below) | `design.md` → Design Source |

Done when every row is answered or has a default ready to propose. That is usually 4–8 questions over two or three rounds; stop asking as soon as you could write the design.

### Figma first, or code first

Every UI project gets this as a question, because only the user knows how they work:

- **Code first**: the look is approved on the design system page inside the app (`ui-context.md` → Design System Page). Recommend it for solo builds and prototypes.
- **Figma first**: each feature's screens are designed and approved in Figma before its code is written. Recommend it when a client expects mockups, or the user already designs in Figma.

When the answer is Figma first, ask who makes the screens in the next round:

- **The user or their designer**: Claude reads the frames and variables through a Figma MCP server when one is connected, or from the links and screenshots the user shares.
- **Claude drafts them in Figma** through a Figma MCP server, and the user approves or edits them there. Check that a Figma MCP server is connected before offering this; when none is, say so and offer the other two routes.

## 3. Two or three approaches

Offer 2–3 genuinely different ways to build it: a different shape, stack or scope, not one idea spelled three ways. For each: one line on what it is, then the trade-offs (time, cost, complexity, what it rules out later). Mark one **Recommended** and give the reason in one sentence tied to the user's answers. Wait for their pick.

The rejected approaches and why they lost go into the design: they end up in `progress-tracker.md` → Architecture Decisions.

## 4. The design, section by section

Show one section per message and wait for approval before the next. Fold changes in and re-show only what changed. Mark the defaults you chose for unasked rows, so the user sees what they are approving.

| # | Section        | Holds                                                                                       | Becomes                                |
| - | -------------- | ------------------------------------------------------------------------------------------- | -------------------------------------- |
| 1 | Product        | Overview, goals, core flow, features, in and out of scope, success criteria                 | `project-overview.md`                  |
| 2 | Depth          | The workflow depth level (Prototype, Alpha, Beta or GA) and why; every feature raised to GA by a GA risk (money, sensitive personal data) | `project-overview.md` → Workflow Depth |
| 3 | Architecture   | Stack, system boundaries (folders), storage, auth and access, invariants, testing tools      | `architecture.md`, `code-standards.md` |
| 4 | Look (UI only) | References with take and don't take, mood, brand assets, theme direction, design source (Figma first or code first, and who makes the screens) | `design.md`, `ui-context.md` |
| 5 | First features | The first 1–3 features as `F-01`…, each with 2–4 acceptance criteria (`AC-1`…), each one observable and checkable on its own | `feature-specs/` |

For section 2, read the template `context/project-overview.md` beside this skill first, then show its Workflow Depth table, GA risks and two rules, and place the project on it. Those four levels are the only ones; a project never gets a level of its own. When it keeps sensitive personal data, name the data protection law that likely applies, from where its users are (GDPR, PDPA…), for the user to confirm.

For section 4, when a design skill is installed (Anthropic's `frontend-design`, for example), load it before proposing the look, and show the palette (named hex values) and typefaces it leads to, so `context kit` writes those exact values.

Done when every section is approved. Then send a short recap: each approved section in a few lines, the open questions, anything still assumed, and the language the files will be written in (the discussion's, unless the user asks for another). End by telling the user the next step is `context kit`.

## The idea is allowed to die

At any point, if the answers show the idea already exists, cannot fit the constraints, or no longer interests the user, say so plainly and offer to stop. Dropping an idea before any code is written is a good outcome.

Pivots are normal too: fold the new direction in and carry on, leaving settled sections settled.
