# Usage Flow: Group H Library Core System — UC-01

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/usage-flow-UC01.md
One map per actor and goal: the order in which an actor uses the system's use cases in real life
to reach one goal. An actor with one goal gets one flow; an actor who comes for clearly different
goals gets one flow per goal.
It is the bridge between Lesson 7 (one activity diagram = one use case) and the screens
(one actor moves through several use cases). Do not copy objectives, features or the architecture
here: they already live in W0, the Function List and your Lesson 4 architecture.
-->

| Field | Value |
|---|---|
| Product | Group H Library Core System |
| Version | v0.2 — revised draft |
| Date | 2026-11-06 |
| Sources | W0 Table 1 (use case inventory); Use Case Diagram; `docs/activity/activity-index.md`; AD-UC-01 v1.2; AD-UC-02 v1.2; `OPAC_Screen_Lists_UC01_UC02_UC11.md` |

## Before you draw: is Lesson 4 still true?

The Inputs check table at the top of `activity-index.md` has 8 findings. Rows 1, 2, 6 and 8 are
"Done". Rows 3, 4, 5 and 7 are still "Open" and are logged as open questions:

- Row 3: a use case "Sync data from the library internal system" (started by time) is still to be added.
- Row 4: the sequence UI Flow (UC-01, UC-02) tells two use cases and is to be split into one sequence per use case.
- Row 5: the sequence User Interface Flow uses optional continuation for map viewing; the choice is now a decision in AD-UC-01.
- Row 7: step references cite FR-01-01, FR-01-03, FR-01-06, FR-01-07, FR-01-09, FR-01-10 correctly according to W1.

None of them changes the flow below: it uses only use cases and the order in which the reader uses them.

- [ ] Every row of the Inputs check table has Status "Done", or is logged as an open question.

## Reader: Find a book's physical shelf location and optionally view its map

```mermaid
flowchart LR
  A(["The Reader wants to find where a book is shelved"]) --> U1["UC-01: View book shelf location"]
  U1 --> D{"Would the Reader like to view the book's room on the map?"}
  D -->|"No"| Z(["The Reader has the book's shelf location"])
  D -->|"Yes"| U2["UC-02: Browse interactive digital library map"]
  U2 --> Z
```

| Step | Use case | Activity diagram | Screens (fill in after Block 2) |
|---|---|---|---|
| 1 | UC-01 View book shelf location | `AD-UC-01.md` | S-F01-01 |
| 2 | UC-02 Browse interactive digital library map, only when the Reader chooses to view the room on the map | `AD-UC-02.md` | S-F01-02 |

Step 1 is always used. Step 2 is used only when the Reader decides to view the book's room on the interactive digital library map. Step 2 is skipped when the Reader only needs the shelf text details or when the map branch is declined.

## Use cases without a flow

No use case in this flow is started by time or by an external system. UC-01 and UC-02 are started by the Reader.

| Use case | Started by | Described in |
|---|---|---|
| — | — | — |

## Checks before you save

- [x] Every actor that starts a use case has at least one flow: Reader is covered for UC-01 and UC-02.
- [x] An actor with clearly different goals has one flow per goal; no flow has more than about 9 boxes.
- [x] Every actor name matches the Use Case Diagram and the Context Diagram (`Reader`).
- [x] Coverage: every in-scope use case of W0 Table 1 (Must, Should, Could) that a person starts appears in at least one flow, with the same ID and name.
- [x] No box is a click or a screen; no box tells two use cases. Diamond represents actor decision between Use Cases.
- [x] Every flow renders on mermaid.live.
- [x] After Block 2: every step has at least one screen, and every screen in the screen list appears in some step (S-F01-01, S-F01-02).