# AI Workflow Rules

## Approach

[Describe the overall development approach — e.g. Build
this project incrementally using a spec-driven workflow.
Context files define what to build, how to build it, and
the current state of progress. Always implement against
these specs — do not infer or invent behavior from scratch.]

## Scoping Rules

- Work on one feature unit at a time
- Prefer small, verifiable increments over large
  speculative changes
- Do not combine unrelated system boundaries in a
  single implementation step

## When to Split Work

Split an implementation step if it combines:

- [Concern one — e.g. UI changes and background task changes]
- [Concern two — e.g. Multiple unrelated API routes]
- [Concern three — e.g. Behavior not clearly defined in
  the context files]

If a change cannot be verified end to end quickly,
the scope is too broad — split it.

## Feature Specs

Every feature gets a spec in `feature-specs/`, copied
from `feature-specs/_template.md`. Its acceptance
criteria (AC-1, AC-2…) are the contract: every build
task serves an AC, and every check points back to one.

In Figma-first projects (`design.md` → Design Source),
a feature's code waits until its frames are approved
as well as its spec, and the build matches those frames.

## Before Building: Input Coverage Check

List every value the feature shows, computes, or
stores, and name its source in the spec's "Where Each
Value Comes From" table. Any value without a named
source is an owed decision — not "just wiring".

## Handling Missing Requirements

- Do not invent product behavior not defined in the
  context files
- If a requirement is ambiguous, resolve it in the
  relevant context file before implementing
- If a decision is owed, either ask first, or build on
  an explicit assumption: log it in the spec as
  **D-n ⚠️ Assumed** (date, the assumption) and list it
  under Open Assumptions in `progress-tracker.md`.
  Never fill the gap silently — the assumption must
  live in the repo, not in chat
- If a requirement is missing, add it as an open question
  in `progress-tracker.md` before continuing

## Protected Files

Do not modify the following unless explicitly instructed:

- [e.g. components/ui/* — generated UI library components]
- [e.g. Any third-party library internals]

## Keeping Docs in Sync

Update the relevant context file whenever implementation
changes:

- System architecture or boundaries
- Storage model decisions
- Code conventions or standards
- Feature scope

## Before Moving to the Next Unit

1. The current unit works end to end within its defined scope
2. Every AC in its spec is checked the way the project's
   Workflow Depth requires (`project-overview.md`), with
   a dated line in the spec's Verification section
3. No invariant defined in `architecture.md` was violated
4. `progress-tracker.md` reflects the completed work,
   including any new Open Assumptions
5. `[build command, e.g. pnpm build]` passes

## Skill Check

Runs when the stack is decided, and again whenever a
new tool joins the project (e.g. a payment provider).

1. List the stack's tools from `architecture.md`
2. Look for the vendor's official skill first; community
   skills only when there is no official one
3. Read each before proposing it: what it instructs,
   any scripts and whether they touch the network,
   size, last update
4. Present a table (skill · vendor · runs code? · size ·
   recommendation) — nothing installs without approval
5. Install = copy the reviewed files into
   `.claude/skills/`; record source + commit SHA in
   `architecture.md` → Skills. No installer CLIs, no `-y`
6. On a new project phase: diff upstream against the
   pinned SHA, review, update on approval
