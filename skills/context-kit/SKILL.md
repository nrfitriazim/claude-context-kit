---
name: context-kit
description: Spec-first project start. Use when the user types `discuss [idea]` (talk an idea through before any code - one question at a time, 2-3 approaches, a design approved section by section) or `context kit` (turn the approved design into seven context files and the first feature specs, then hold all code until the user approves them), or asks to plan or spec a new project or feature before building it.
---

# Context kit

Two commands, one gate.

| Command          | Does                                                                     | Writes          |
| ---------------- | ------------------------------------------------------------------------ | --------------- |
| `discuss [idea]` | Talks the idea through until the user approves a design, or drops the idea | Nothing         |
| `context kit`    | Fills the seven context files and the first feature specs from that design | `context/`, plus a pointer in `CLAUDE.md` |

**The gate**: until the user approves the filled specs, every file you write lives in the project's `context/` folder, apart from the short pointer section `context kit` adds to `CLAUDE.md` so later sessions find the specs. Code, scaffolding, package installs and config come after approval, one feature at a time, built against its spec.

## Where things live

- **Templates**: `context/` beside this file, the seven files plus `feature-specs/_template.md`. Read them fresh from here every time; they are the source of truth.
- **The project's copy**: `context/` at the project root, which is the working directory unless the user names another folder.

## Route the request

- `discuss [idea]`: read `discuss.md` (beside this file) and follow it.
- `context kit`: read `fill.md` (beside this file) and follow it. It starts by checking that a design was approved, and sends you to `discuss.md` when none was.
- A new feature in a project whose `context/` is already filled: `discuss` scoped to that one feature, then `context kit` adds its spec. `fill.md` covers this case.
- The user wants only the blank templates: copy this skill's `context/` into the project unfilled, and stop.

## Both commands

- **Speak the user's language** (BM, English, rojak: match them). Keep file names, template headings and IDs (`F-01`, `AC-1`, `D-1`) exactly as the templates have them, because the method and other tools rely on them.
- **One question per message**, then wait for the answer.
- **Every decision has an owner**: the user's answer, a default the user approved, or a logged `⚠️ Assumed`. A gap you notice becomes a question or a logged assumption, so nothing is decided silently.

## After approval

Build one feature at a time by the project's `context/ai-workflow-rules.md`: input coverage check, build, verify every AC the way the project's workflow depth requires, then update `progress-tracker.md`.
