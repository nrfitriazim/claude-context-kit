# UI Context

Token values and component rules. The art direction
these come from — references, mood, do/don't — lives
in `design.md`. Everything here is rendered on the
design system page (see the end of this file).

## Theme

[The look in two or three lines — e.g. Light and warm:
off-white pages, soft cards with a hairline border, one
coral accent for anything you can press. Dark mode
follows the system setting.]

## Colors

[Every colour is a CSS variable, and components use
only these variables. Figma-first projects copy the
values from the Figma variables.]

| Role                    | CSS Variable           | Value    |
| ----------------------- | ---------------------- | -------- |
| Background              | `--color-bg`           | `#[hex]` |
| Cards and panels        | `--color-surface`      | `#[hex]` |
| Text                    | `--color-text`         | `#[hex]` |
| Secondary text          | `--color-text-soft`    | `#[hex]` |
| Accent (buttons, links) | `--color-accent`       | `#[hex]` |
| Borders                 | `--color-border`       | `#[hex]` |
| Error                   | `--color-error`        | `#[hex]` |
| Success                 | `--color-success`      | `#[hex]` |

## Typography

| Role     | Font                 | Variable         |
| -------- | -------------------- | ---------------- |
| Body     | [e.g. Inter]         | `--font-body`    |
| Headings | [e.g. Fraunces]      | `--font-heading` |
| Code     | [e.g. JetBrains Mono] | `--font-mono`   |

### Type Scale

| Style     | Font      | Size / Line height | Weight     | Use            |
| --------- | --------- | ------------------ | ---------- | -------------- |
| Display 1 | [Heading] | [48 / 56]          | [Bold]     | [Page titles]  |
| Heading 1 | [Body]    | [28 / 36]          | [Semibold] | [Card titles]  |
| Body      | [Body]    | [14 / 20]          | [Regular]  | [Body copy]    |
| Small     | [Body]    | [12 / 16]          | [Regular]  | [Captions]     |

## Spacing

Base unit: [e.g. 4px]. Scale: [e.g. 4 · 8 · 12 · 16 ·
24 · 32 · 48 · 64]. No off-scale values.

## Border Radius

| Used on               | Value         |
| --------------------- | ------------- |
| Buttons, inputs, tags | [e.g. 8px]    |
| Cards                 | [e.g. 12px]   |
| Dialogs               | [e.g. 16px]   |

## Shadows

| Level | Value                         | Use              |
| ----- | ----------------------------- | ---------------- |
| [Sm]  | [e.g. 0 1px 2px rgba(…)]      | [e.g. Inputs]    |
| [Md]  | [e.g. 0 4px 12px -2px rgba(…)] | [e.g. Cards]    |

## Component States

[Where AI-built UI drifts most. Define every state once
here; the design system page renders each one.]

| Component | Default | Hover | Focus | Disabled | Error |
| --------- | ------- | ----- | ----- | -------- | ----- |
| [Primary button] | [e.g. accent bg, white text] | [darker 10%] | [2px ring] | [40% opacity] | — |
| [Text input]     | [e.g. 1px border]            | —            | [accent border] | [muted bg] | [error border + message] |

## Component Library

[Which library, and how it is used — e.g. shadcn/ui,
added through its CLI into `components/ui/`, never
hand-copied.]

## Layout Patterns

- [e.g. Dashboard: sidebar on the left, content on the
  right; on phones the sidebar becomes a bottom bar]
- [e.g. Forms: one column, labels above the fields]
- [e.g. Dialogs: centred, over a dimmed page]

## Icons

[Icon set and sizes — e.g. Lucide, outline style;
16px beside text, 20px in buttons.]

## Motion

[Project-specific motion — durations, easing, page
transitions, reduced-motion behaviour. Keep it short:
motion that is not decided here tends to get invented
per component.]

## Design System Page

One page that renders every token and component state
above, so the system can be checked at a glance and
approved before pages are built.

- **Where**: [App projects: a page inside the app, e.g.
  `/design-system`, reachable on dev/staging only — it
  renders the REAL components, so it cannot drift. No
  app to host it (site builder, CMS theme, plain HTML):
  a standalone `context/design-system.html`.]
- **Sections**: Colors · Typography + type scale ·
  Spacing · Radius + shadows · Icons · Buttons (all
  states) · Inputs · Badges / tags · Status indicators ·
  Cards · Navigation · [project-specific components]
- **Approval**: [How whoever signs off on the look sees
  it — e.g. the staging link, or the page printed to
  PDF.] Log the approval in `design.md` → Approval Log.
