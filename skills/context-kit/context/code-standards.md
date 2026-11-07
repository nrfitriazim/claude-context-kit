# Code Standards

## General

- [Principle — e.g. Keep modules small and single-purpose]
- [Principle — e.g. Fix root causes, do not layer workarounds]
- [Principle — e.g. Do not mix unrelated concerns in one
  component or route]

## TypeScript

[Rename this section to the project's language if it is
not TypeScript.]

- [Rule — e.g. Strict mode is required throughout the project]
- [Rule — e.g. Avoid any — use explicit interfaces or narrowly
  scoped types]
- [Rule — e.g. Validate unknown external input at system
  boundaries before trusting it]

## [Framework — e.g. Next.js]

- [Convention — e.g. Default to server components]
- [Convention — e.g. Add use client only when browser
  interactivity requires it]
- [Convention — e.g. Keep route handlers focused on a
  single responsibility]

## Styling

- [Rule — e.g. Use CSS custom property tokens — no
  hardcoded hex values]
- [Rule — e.g. Follow the border radius scale defined
  in ui-context.md]

## API Routes

- [Rule — e.g. Validate and parse request input before
  any logic runs]
- [Rule — e.g. Enforce auth and ownership before any mutation]
- [Rule — e.g. Return consistent, predictable response shapes]

## Data and Storage

- [Rule — e.g. Metadata belongs in the database]
- [Rule — e.g. Large generated content belongs in file
  or blob storage]
- [Rule — e.g. Do not store large content directly in
  the database]

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

| Level     | Tests                                          |
| --------- | ---------------------------------------------- |
| Prototype | None                                           |
| Alpha     | No test files — ACs checked in a browser       |
| Beta      | Playwright smoke test per critical AC (pages load, login, admin create → edit → delete), run after every deploy |
| GA        | + Vitest on the money logic (pricing, totals, shipping, discounts — server side) + a forged-webhook test (a fake "paid" must be rejected) + a sandbox payment run end to end + one real paid order before launch |

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

- `[folder]/` — [What belongs here]
- `[folder]/` — [What belongs here]
- `[folder]/` — [What belongs here]
- `[folder]/` — [What belongs here]
