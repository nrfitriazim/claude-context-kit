# [Project Name]

## Overview

[One paragraph describing what this application does,
who it's for, and what problem it solves.]

## Goals

1. [Goal one — specific and measurable]
2. [Goal two]
3. [Goal three]

## Core User Flow

1. [Step one — e.g. User signs in]
2. [Step two]
3. [Step three]
4. [Continue until the core flow is complete]

## Features

### [Feature Category One]

- [Feature description]
- [Feature description]

### [Feature Category Two]

- [Feature description]
- [Feature description]

## Scope

### In Scope

- [What you are building]
- [What you are building]

### Out of Scope

- [What you are explicitly not building]
- [What you are explicitly not building]

## Success Criteria

1. [Specific, verifiable condition — e.g. A signed-in
   user can create and open a project]
2. [Condition two]
3. [Condition three]

## Client

[Client projects only: built for someone else who makes
the final call. Otherwise keep this heading and one
line: Not a client project.]

- **Client**: [Name and business — e.g. Puan Aminah,
  Kedai Kek Aminah]
- **Signs off**: [Who makes the final call, and how the
  sign-off arrives — e.g. Puan Aminah, on WhatsApp]
- **Accounts in the client's name**: [e.g. domain,
  hosting, payment gateway, business email, and who
  holds the logins until handover]
- **Data responsibility**: [When the project keeps
  personal data: the client is responsible for it
  under the law (data user / controller); the builder
  handles it for them (processor). Otherwise: none.]

Sign-offs:

- [date — what was approved, by whom, how — e.g.
  12 Nov — specs F-01 to F-03, Puan Aminah, WhatsApp]

Rules:

- The client's sign-off opens the gate. The builder
  relays it, and it is logged above with a date.
- A request outside the approved scope is a new
  feature with its own `discuss` and spec, so the
  change is visible, and can be quoted, before it is
  built.

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
