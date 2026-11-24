# Group H Library Core System

Analysis and design documents of **Group H, course DBIZ2**. The product is an add-on to the library's existing
catalogue system (OPAC, [opac.nlv.gov.vn](https://opac.nlv.gov.vn)). It helps readers find the right shelf, browse a
map of the library, read and write book reviews, scan a QR code on a physical book and get book recommendations.

This repository holds documents only, no product code. The screens are wireframes, the input for the build in DBIZ3.

## Status

Updated 23/11/2026.

| Item | Count | Status |
|---|---|---|
| Use cases, each with an activity and a sequence diagram | 15 | Draft |
| Screens, each with a screen spec | 15 | Draft |
| Modals (specified inside the spec of their parent screen) | 5 | Draft |
| Functional requirements (FR) | 81 | In [fr-list.md](docs/function-list/fr-list.md) |
| Effort and cost | | In [cost.md](docs/function-list/cost.md) |

Work still to be done, with owners, is tracked in one place:
[Pending tasks](docs/project/decision-index.md#pending-tasks).

## Product scope

Two groups of users: **Readers** and **On-site Staff**.

| ID | Feature | Users | Use cases | Screens |
|---|---|---|---|---|
| F-01 | Book location and library map | Reader | UC-01, 02 | S-F01-01, 02 |
| F-02 | Book reviews and QR codes | Reader, On-site Staff | UC-04, 05, 06, 10, 13, 14 | S-F02-01 to 04 |
| F-03 | Discovery, reading history and recommendations | Reader | UC-03, 07, 08, 09, 12 | S-F03-01, 02, 03, 06, 07 |
| F-04 | Sign-in, access and operations | All | UC-11, 15 | S-F00-01 to 03, S-F04-01 |

Use case priority:

- **Must:** UC-01, 02, 04, 05, 06, 10, 11, 15
- **Should:** UC-03, 07, 12
- **Could:** UC-08, 09, 13, 14

**Out of scope:** borrowing, returning and renewing books; reading books online inside the platform; keyword search
(the OPAC already has it); online reader accounts and Google sign-in; a full librarian workspace. The full list and
reasons: [scope.md, Table 3](docs/function-list/scope.md#table-3-wont-have).

## Documents

Folders follow the teacher's example
[LabDesk](https://github.com/chienact-code/dbiz2-labdesk-example/tree/main/docs), with lower-case names joined by hyphens like the example (D53, D54).

| Folder | File | What it holds |
|---|---|---|
| [project/](docs/project/) | [decision-index.md](docs/project/decision-index.md) | Every decision and the pending tasks |
| | [task-assignment-26-11.md](docs/project/task-assignment-26-11.md) | Tasks of 24/11/2026, in Vietnamese, due 26/11/2026 |
| [context/](docs/context/) | [cvca.md](docs/context/cvca.md) | Customer value chain: who pays whom and who gives what information |
| | [context-diagram.md](docs/context/context-diagram.md) | System boundary and the flows that cross it |
| [use-case/](docs/use-case/) | [use-case.md](docs/use-case/use-case.md) | Use case diagram and the list of all use cases |
| | [sequence-index.md](docs/use-case/sequence-index.md) | Index of the 15 sequence diagrams (`sd-uc-01.md` … `sd-uc-15.md`) |
| [architecture/](docs/architecture/) | [system-architecture.md](docs/architecture/system-architecture.md) | Parts of the system, data stores, connections to outside systems |
| [function-list/](docs/function-list/) | [scope.md](docs/function-list/scope.md) | W0: features, what is left out, data the system keeps or reads |
| | [fr-list.md](docs/function-list/fr-list.md) | All functional requirements, priorities and work items |
| | [cost.md](docs/function-list/cost.md) | Effort, cost and cash flow (kept apart from the FRs) |
| [activity/](docs/activity/) | [activity-index.md](docs/activity/activity-index.md) | Index of the 15 activity diagrams (`ad-uc-01.md` … `ad-uc-15.md`) |
| [external-design/](docs/external-design/) | [usage-flow.md](docs/external-design/usage-flow.md) | How a user moves through the product |
| | [screen-list.md](docs/external-design/screen-list.md) | All screens and modals, with links to their specs |
| | [screen-transition.md](docs/external-design/screen-transition.md) | Screen transition diagram |
| | [ui-conventions.md](docs/external-design/ui-conventions.md) | UI rules, standard messages and design tokens |
| | [screens/specs/](docs/external-design/screens/specs/) | One screen spec per screen, with its mock-up |
| | [screens/notes/](docs/external-design/screens/notes/) | Wireframe notes per screen and modal |
| | [screens/img/](docs/external-design/screens/img/) | Mock-up images of every screen and state |
| | [screens/src/](docs/external-design/screens/src/) | Wireframe sources (HTML, CSS, draw.io) |

## Reading order

1. **The problem:** [cvca.md](docs/context/cvca.md), [context-diagram.md](docs/context/context-diagram.md),
   [scope.md](docs/function-list/scope.md).
2. **Use cases and system:** [use-case.md](docs/use-case/use-case.md),
   [system-architecture.md](docs/architecture/system-architecture.md).
3. **Requirements:** [fr-list.md](docs/function-list/fr-list.md).
4. **Business flow of each use case:** [activity-index.md](docs/activity/activity-index.md), then
   [sequence-index.md](docs/use-case/sequence-index.md).
5. **How a user moves through the product:** [usage-flow.md](docs/external-design/usage-flow.md),
   [screen-list.md](docs/external-design/screen-list.md),
   [screen-transition.md](docs/external-design/screen-transition.md).
6. **Screen detail:** [ui-conventions.md](docs/external-design/ui-conventions.md), then the specs in
   [screens/specs/](docs/external-design/screens/specs/).
7. **Why something was decided:** [decision-index.md](docs/project/decision-index.md); search for the ID cited in
   the document, for example `D7` or `L8-01`.

## ID conventions

| ID | Meaning | Example |
|---|---|---|
| `UC-nn` | Use case | `UC-04` |
| `FR-<feature>-<nn>` | Functional requirement | `FR-02-23` |
| `AD-UC-nn` / `SD-UC-nn` | Activity / sequence diagram of one use case | `AD-UC-10` |
| `S-F<feature>-<nn>` | Screen. `S-F00` is the shared sign-in | `S-F01-02` |
| `M-F00-<nn>` | Modal shared by several screens | `M-F00-01` |
| `M-<screen>-<nn>` | Modal of one screen | `M-F02-03-01` |
| `MSG-nn` | Standard message in [ui-conventions.md](docs/external-design/ui-conventions.md) | `MSG-04` |
| `D<n>`, `UI Q<n>`, `L8-<nn>` | Decision in [decision-index.md](docs/project/decision-index.md) | `D12` |

IDs keep their upper-case form inside documents. File names are the same ID in lower case, joined by hyphens:
`AD-UC-10` is in `ad-uc-10.md`, `S-F01-02` in `screen-spec-s-f01-02.md`.

<a id="workbook-labels"></a>

## Workbook labels

Until 23/11/2026 the FRs and costs lived in an Excel workbook, now frozen at commit [cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/tree/cd61897/%5BDBIZ%202%5D%20GROUP%20H) (D51). Older
text still cites its sheets. They now mean:

| Label in older text | Now in |
|---|---|
| W0 Table 1 (use case inventory) | [use-case.md §3](docs/use-case/use-case.md#3-use-case-inventory-w0-table-1) |
| W0 Tables 2, 3, 4 (features, won't have, data functions) | [scope.md](docs/function-list/scope.md) |
| W1 (function list), W4 (priorities), W5 §4 (open questions) | [fr-list.md](docs/function-list/fr-list.md) |
| Parameters, W2_Costing, W2_Rollup, W5 §1–3, W6 | [cost.md](docs/function-list/cost.md) |

## Rules for updating documents

- **Changing a decision:** add a new row with a new ID to
  [decision-index.md](docs/project/decision-index.md) that supersedes the old one. Do not change a requirement
  in any document without that row.
- **Changing an FR:** edit [fr-list.md](docs/function-list/fr-list.md) directly (D51), then ask the cost owner to
  update [cost.md](docs/function-list/cost.md). Totals in cost.md are not automatic.
- **UI values:** colours, font sizes and message wording are defined once in
  [ui-conventions.md](docs/external-design/ui-conventions.md).
  [ui-tokens.css](docs/external-design/screens/src/ui-tokens.css) copies its section 6 exactly.
- **Screens and states:** error messages, empty lists and confirmations are states of a screen, not new screens.
- **Retired IDs** are never reused, for example `S-F03-04` and `S-F03-05`.
- **Language:** documents in English; text on the screens in Vietnamese with diacritics.
- **File names:** lower-case words joined by hyphens (`fr-list.md`), inside `docs/` (D54). Every mention of another file is a clickable link.

## AI tools

AI assistants working in this repository follow [AGENTS.md](AGENTS.md). In short: they do not read
[cost.md](docs/function-list/cost.md) or the archived workbook unless asked for cost work in so many words.

## Viewing diagrams and wireframes

- Diagrams in `.md` files are written in Mermaid. Activity diagrams use `swimlane-beta`, checked with Mermaid 12.3.0
  in Chrome; older viewers may fail to draw them.
- `.html` files in [screens/src/](docs/external-design/screens/src/) open directly in a browser.
- `.drawio` files open in [diagrams.net](https://app.diagrams.net).
