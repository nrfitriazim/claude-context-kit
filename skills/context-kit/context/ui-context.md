# UI Context

Token values and component rules. The art direction
these come from — references, mood, do/don't — lives
in `design.md`. Everything here is rendered on the
design system page (see the end of this file).

## Theme

[Describe the overall visual language — e.g. Dark only.
No light mode. The design language is a dark technical
workspace — near-black backgrounds, layered surfaces,
and vivid accent colors for interactive elements.]

## Colors

[Define your color tokens as CSS custom properties.
All components must use these tokens — no hardcoded
hex values. Figma-first projects take these values
from the Figma variables.]

| Role            | CSS Variable       | Value    |
| --------------- | ------------------ | -------- |
| Page background | `--bg-base`        | `#[hex]` |
| Surface         | `--bg-surface`     | `#[hex]` |
| Primary text    | `--text-primary`   | `#[hex]` |
| Muted text      | `--text-muted`     | `#[hex]` |
| Primary accent  | `--accent-primary` | `#[hex]` |
| Border          | `--border-default` | `#[hex]` |
| Error           | `--state-error`    | `#[hex]` |
| Success         | `--state-success`  | `#[hex]` |

## Typography

| Role      | Font              | Variable      |
| --------- | ----------------- | ------------- |
| UI text   | [e.g. Geist Sans] | `--font-sans` |
| Display   | [e.g. Playfair Display] | `--font-display` |
| Code/mono | [e.g. Geist Mono] | `--font-mono` |

### Type Scale

| Style     | Font      | Size / Line height | Weight     | Use            |
| --------- | --------- | ------------------ | ---------- | -------------- |
| Display 1 | [Display] | [48 / 56]          | [Bold]     | [Page titles]  |
| Heading 1 | [Sans]    | [28 / 36]          | [Semibold] | [Card titles]  |
| Body      | [Sans]    | [14 / 20]          | [Regular]  | [Body copy]    |
| Small     | [Sans]    | [12 / 16]          | [Regular]  | [Captions]     |

## Spacing

Base unit: [e.g. 4px]. Scale: [e.g. 4 · 8 · 12 · 16 ·
24 · 32 · 48 · 64]. No off-scale values.

## Border Radius

| Context           | Class            |
| ----------------- | ---------------- |
| Inline / small UI | `rounded-[size]` |
| Cards / panels    | `rounded-[size]` |
| Modals / overlays | `rounded-[size]` |

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

[e.g. shadcn/ui on top of Tailwind. Components live
in components/ui/. Use the CLI to add new components
rather than writing from scratch.]

## Layout Patterns

- [Pattern — e.g. Editor: full-viewport split with
  left sidebar, center canvas, right sidebar]
- [Pattern — e.g. Sidebars: fixed width with border separator]
- [Pattern — e.g. Modals: centered overlay with backdrop blur]
- [Pattern — e.g. Navbar: top bar with bottom border]

## Icons

[e.g. Lucide React. Stroke-based icons only. Sizes:
h-4 w-4 for inline, h-5 w-5 for buttons.]

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
