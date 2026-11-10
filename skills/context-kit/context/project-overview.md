# [Project Name]

## Overview

[One paragraph: what the product is, who uses it, and
the problem it takes away.]

## Goals

1. [A goal you can measure — e.g. A student sees every
   deadline for the week on one screen]
2. [Goal]
3. [Goal]

## Core User Flow

[The one path a user must be able to complete, step by
step.]

1. [e.g. The student signs in with Google]
2. [e.g. Adds an assignment with its due date]
3. [e.g. Sees it on the dashboard, sorted by due date]
4. […until the path is complete]

## Features

### [Group — e.g. Assignments]

- [Feature — e.g. Add, edit and delete assignments]
- [Feature]

### [Group]

- [Feature]

## Scope

### In Scope

- [What v1 includes]

### Out of Scope

- [What v1 leaves out, said plainly — e.g. No sync with
  the university portal]

## Success Criteria

1. [Something you can check — e.g. Ten classmates use
   it through one full week of deadlines]
2. [Criterion]
3. [Criterion]

## Workflow Depth

**Level**: [Prototype / Alpha / Beta / GA]

[Why this level — e.g. Beta: the owner edits products
in the admin, no payments yet. At GA, also name each
GA risk, and for personal data the data protection law
that applies — e.g. GA: patients' IC numbers and visit
notes; PDPA (Malaysia).]

| Level         | Used for                                                          | Checks (each adds to the one above)            |
| ------------- | ----------------------------------------------------------------- | ---------------------------------------------- |
| **Prototype** | Practice builds, demos, throwaway experiments                     | Build, run it, and look at it (a screenshot when it has a screen) |
| **Alpha**     | Real users, but the content only changes when the code does       | + every AC checked where it runs (staging or live), dated |
| **Beta**      | Others change content or data after launch (an admin, a CMS, user accounts) | + automated smoke test against the running app (throwaway accounts and data the script creates and deletes) |
| **GA**        | A GA risk: a mistake costs someone money or exposes their sensitive personal data | + code review + security review before launch + the checks for each GA risk below |

GA risks and their checks:

- **Money** (payments, subscriptions, deposits,
  payouts): money logic (prices, totals, shipping,
  discounts) runs on the server; payment-path audit; a
  forged "paid" notification is rejected; one real
  payment checked end to end before launch.
- **Sensitive personal data** (ID or passport numbers,
  health, finances, exact location, children's data,
  or records whose leak would harm someone, such as
  grades or HR files): each person reaches only their
  own records, checked with a test for every role; only
  what a feature uses is collected; a privacy notice
  says what is kept and why; a person can get, correct
  and delete their records; backups exist, and one
  restore is tried before launch. Ordinary account
  details (a name, an email, a sign-in handled by an
  auth provider) are not a GA risk on their own.

These are engineering checks, not legal advice; the
law's own requirements still apply.

Rules:

- **Money and sensitive personal data are always GA**,
  even inside a lower-level project — raise that
  feature's spec to GA.
- **Levels only go up mid-project, never down
  silently.** A prototype that becomes the real build
  moves up, and its checks catch up before launch.

Feature overrides:

- [e.g. F-04 Checkout — GA (money)]
