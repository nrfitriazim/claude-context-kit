# Code Standards

## General

- [e.g. One job per file or module]
- [e.g. Fix the cause of a bug, not its symptom]
- [e.g. Components render; data fetching and business
  rules live elsewhere]

## TypeScript

[Rename this section to the project's language if it is
not TypeScript.]

- [e.g. `strict: true` in tsconfig]
- [e.g. No `any`: type the shape instead]
- [e.g. Data from forms, URLs and other services is
  parsed (with Zod, say) before the code uses it]

## [Framework, e.g. Next.js]

- [e.g. Server components, unless the page needs the
  browser]
- [e.g. One route handler per action]

## Styling

- [e.g. Colours come from the tokens in
  `ui-context.md`; no raw hex in components]
- [e.g. Radius, spacing and shadows use the scales in
  `ui-context.md`]

## API Routes

- [e.g. Parse the request body first; reject what
  doesn't fit]
- [e.g. Check who is asking, and that they own the
  record, before any write]
- [e.g. Every response has the same shape: `{ data }`
  or `{ error }`]

## Data and Storage

- [e.g. Records and relations go in the database]
- [e.g. Files and images go in object storage; the
  database keeps their URL]

## Testing

**Tools**: [e.g. Vitest for logic, Playwright for the
browser, PGlite for migrations] — dev dependencies of
this project only.

**Commands**:

- `[e.g. pnpm test]` — unit / logic tests
- `[e.g. pnpm test:e2e]` — browser tests; target URL is
  passed in (`BASE_URL=…`), never hardcoded

**What gets tested** (by the project's Workflow Depth in
`project-overview.md`; each level adds to the one above):

| Level             | Tests                                          |
| ----------------- | ---------------------------------------------- |
| Prototype         | None                                           |
| Alpha             | No test files — ACs checked by hand where it runs |
| Beta              | Automated smoke test per critical AC (it starts, sign-in works, create → edit → delete), run after every deploy |
| GA, money         | + unit tests on the money logic (prices, totals, shipping, discounts — server side) + a forged-notification test (a fake "paid" must be rejected) + a sandbox payment run end to end + one real payment before launch |
| GA, personal data | + an access test for every role (a user cannot read or change another user's records; signed-out requests are refused) + a delete-on-request test + one restore from backup before launch |

A GA project runs the GA row for each GA risk it has
(`project-overview.md` → Workflow Depth).

Rules:

1. **Every test names its AC** —
   `test('AC-2: sold-out size cannot be added')` — so a
   failure says which promise broke
2. **Every bug fix starts with a regression test** that
   fails before the fix and passes after
3. **Production stays clean** — tests that write
   data run on staging. On live: read-only checks, or
   self-cleaning flows with throwaway accounts the
   script creates and deletes. No real passwords, no
   fake data left behind
4. [GA, optional: CI runs `test` + build on every push]

## File Organization

- `[folder]/` — [what goes here]
- `[folder]/` — [what goes here]
- `[folder]/` — [what goes here]
