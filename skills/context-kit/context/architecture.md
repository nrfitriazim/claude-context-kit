# Architecture Context

## Stack

| Layer     | Technology                  | Used for                                  |
| --------- | --------------------------- | ----------------------------------------- |
| Framework | [e.g. Next.js, TypeScript]  | [e.g. Pages and server logic]             |
| Styling   | [e.g. Tailwind CSS]         | [e.g. All styling, through the tokens in `ui-context.md`] |
| Auth      | [e.g. Supabase Auth]        | [e.g. Email and Google sign-in]           |
| Database  | [e.g. Postgres on Supabase] | [e.g. Users, records, settings]           |
| [Layer]   | [Technology]                | [Used for]                                |

## System Boundaries

[One line per top-level folder: what it owns, and what
stays out of it — e.g. `app/` — routes and pages; no
direct database calls.]

- `[folder]` — [what it owns]
- `[folder]` — [what it owns]
- `[folder]` — [what it owns]

## Storage Model

[Each place data is kept, and what goes there.]

- **[e.g. Postgres]**: [e.g. accounts, records and who
  owns them]
- **[e.g. Object storage]**: [e.g. uploads and images;
  the database keeps their URL]

## Auth and Access Model

- [Sign-in — e.g. Email or Google, through Supabase
  Auth]
- [Ownership — e.g. Each record belongs to the user who
  created it]
- [Who can change what — e.g. A user edits only their
  own records; an admin can edit any]

## Skills

[Agent skills committed to this repo's skills folder
(`.claude/skills/`, or `.agents/skills/`).
Found by the skill check (`ai-workflow-rules.md`):
vendor skills first, read before installing, approved
before committing. The SHA pins exactly what was reviewed.]

| Skill                 | Source repo                     | Commit SHA | Runs code? | Reviewed   |
| --------------------- | ------------------------------- | ---------- | ---------- | ---------- |
| [e.g. supabase]       | [e.g. the vendor's skills repo] | [sha]      | [No / what it runs] | [date] |

Global skills used here (not committed): [e.g.
frontend-design]

## Invariants

[Rules that hold everywhere in the code, whatever the
feature.]

1. [e.g. Prices are computed on the server, never taken
   from the browser]
2. [Invariant]
3. [Invariant]
