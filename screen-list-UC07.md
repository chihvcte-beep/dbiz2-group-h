# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-07 Update and view personal reading history and preferences\
**Actor:** Reader\
**Feature:** F-03 Discovery, Reading History & Recommendation\
**Login required:** Yes (checked by FR-04-08; sign-in is UC-11)\
**Source:** AD-UC-07 · FR-03-01, FR-03-02, FR-03-03, FR-03-04, FR-03-05, FR-03-22, FR-04-08 · FR-04-01 through the sign-in step

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F03-02 | Reading History & Preferences | Reader | F-03 | A signed-in reader opens their personal reading history and preferences. The screen displays history entries with reading status and lets the reader update a book's status and progress or update reading preferences. It shows the saved changes or an error while keeping the previous saved data unchanged when an update fails validation. | Reader account / personal area after sign-in (`S-F00-01`) → Reading History & Preferences | UC-07 · FR-03-01, FR-03-04, FR-03-05, FR-03-22, FR-04-08. History entries are also added by background events under FR-03-02 and FR-03-03. | Must | `screens/screen-spec-S-F03-02.md` |

**Priority note:** S-F03-02 is Must because FR-03-01 requires readers to view their reading history, FR-03-04 allows them to update reading status and progress, and FR-03-05 allows them to update reading preferences. FR-03-22 requires invalid updates to be rejected while preserving saved data and displaying an error. The automatic history-entry processes (FR-03-02 and FR-03-03) update the data shown on this screen but do not require a separate screen.

**Shared screens, not defined here**

- `S-F00-01` Sign in (UC-11, FR-04-01): opened when a reader without a valid session chooses to sign in. After successful sign-in, the flow returns to the reading-history request and checks the session again. This is a shared platform screen, not specific to UC-07.
- `S-F03-01` Book Catalogue & Access Format Filter (UC-03): opening an online book from its results can trigger an automatic reading-history entry for a signed-in reader (FR-03-02). That event updates the data displayed on S-F03-02; it is not a separate UC-07 screen.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| None specified | — | AD-UC-07 does not define a confirmation dialog or overlay. Reading status, progress and preference updates are submitted on the Reading History & Preferences screen; validation feedback is displayed as a screen state. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Sign in | A shared platform screen (`S-F00-01`, UC-11), not specific to UC-07. |
| Check the reader's session (FR-04-08) | A system access-control step; it determines whether the reading-history request is allowed. |
| Ask whether the reader wants to sign in | A decision in the activity flow, not a separate screen. If the reader chooses Yes, they use the shared sign-in screen; if No, the activity ends without showing the history. |
| Deny access without a valid reader session (FR-04-08) | An access-control outcome, not a separate screen. |
| Retrieve and display the reader's reading history and preferences (FR-03-01) | Retrieval is a system action; the history and preferences are displayed on S-F03-02. |
| Submit reading status and progress | An action performed on S-F03-02, not a separate screen. |
| Check that status is Reading or Finished and progress is between 0 and 100 percent (FR-03-04) | A system validation step; its result is displayed on S-F03-02. |
| Save and display updated reading status and progress (FR-03-04, FR-03-01) | A system action and updated state of S-F03-02, not a separate screen. |
| Submit and validate updated reading preferences (FR-03-05) | An action and system validation step performed on S-F03-02, not a separate screen. |
| Save and display updated preferences (FR-03-05) | A system action and updated state of S-F03-02, not a separate screen. |
| Error message for a rejected update (FR-03-22) | An error state of S-F03-02; the saved data stays unchanged. |
| Daily loan-record sync finished (time event) | A time-triggered background event, not a user-navigable screen. |
| Find new borrow records and add borrowed books to readers' histories (FR-03-03) | A background process after the daily sync; it updates the history data without reader interaction or a separate screen. |
| Online book opened by a signed-in reader (accept event from UC-03) | An event originating in UC-03, not a screen in UC-07. |
| Add the opened online book to the reader's history (FR-03-02) | A background system action triggered by the UC-03 event; it updates the history data shown on S-F03-02. |
| Automatically track reading progress | Not included in this release (W0 Table 3). Progress is entered manually by the reader. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-07. The time-event and accept-event parts have no screen.

| AD-UC-07 node | Reader action | Screen |
|---|---|---|
| r1 | Open reading history and preferences | S-F03-02 |
| d1 | Choose whether to sign in now | No screen (activity-flow decision) |
| c1 | Sign in (UC-11) | S-F00-01 |
| d2 | Choose to update reading status and progress, update preferences, or finish | S-F03-02 |
| r2 | Submit the reading status and progress of a book | S-F03-02 |
| r3 | Submit updated reading preferences | S-F03-02 |
| s0 / d0 | Check the reader's session / determine whether the session is valid | No screen (system access-control step) |
| s1 | Deny access without a valid session | No screen (access-control outcome) |
| s2 / s3 | Retrieve and display the reader's reading history with reading status | S-F03-02 |
| s4 / d3 | Validate reading status and progress / determine whether the update passes validation | S-F03-02 (system validation) |
| s5 / s6 | Save reading status and progress / display the updated history | S-F03-02 |
| s7 / d4 | Validate reading preferences / determine whether the preferences pass validation | S-F03-02 (system validation) |
| s8 / s9 | Save preferences to the reader's profile / display updated preferences | S-F03-02 |
| s10 | Reject an invalid update, keep saved data and display an error message | S-F03-02 (error state) |
| t1 / s11 / d5 / s12 | Process new borrow records after daily sync and add each borrowed book to the reader's history | No screen (automatic time-triggered background process) |
| e1 / s13 | Receive the online-book-opened event from UC-03 and add the book to the signed-in reader's history | No screen (automatic event-triggered background process) |
