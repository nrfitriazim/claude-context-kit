# F-[NN] · [Feature Name]

Status: Draft → Approved → Built → Verified
Depth: [Inherits project level from project-overview.md,
or raised here — e.g. GA (money): it takes payments]
Design: [Figma-first projects only: link to this
feature's frames, and whether they are approved. Delete
this line in code-first projects.]

## What & Why

[2–3 lines. What this feature does, for whom, and why
it exists.]

## Acceptance Criteria

[The contract. Each criterion is IDed, observable, and
checkable on its own. Build tasks and verification
both point back to these IDs.]

- **AC-1**: [Observable outcome — e.g. Price shows the
  DB price, never a price sent from the browser]
- **AC-2**: [Key edge case or failure — e.g. A sold-out
  size cannot be added to cart]
- **AC-3**: [e.g. Works at 375px with no horizontal
  scroll]

## Where Each Value Comes From

[Input coverage check — list every value this feature
shows, computes, or stores, and name its source. Fill
this BEFORE building.]

| Shown / computed     | Source                          |
| -------------------- | ------------------------------- |
| [e.g. Price]         | [e.g. products.price, server]   |
| [e.g. Stock badge]   | [e.g. variants.stock]           |
| [e.g. Tile image]    | ❓ not decided                  |

A ❓ row means a decision is owed: ask, or build on an
assumption and log it under Decisions as Assumed.
Never fill the gap silently.

## Decisions

- **D-1** ✅ Accepted: [Decision — and why]
- **D-2** ⚠️ Assumed ([date], awaiting approval):
  [The assumption this build uses]

## Out of Scope

- [What this feature deliberately does not do]

## Verification

[One line per AC once checked. Done = every AC has a
date and where it was checked. Depth decides how — see
ai-workflow-rules.md.]

- AC-1 [✅ / ❌] [date] — [where + how, e.g. live,
  browser check / smoke test / access test / real
  payment] —
  [test that covers it, e.g. `e2e/cart.spec.ts`, or
  "manual"]
