# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-13 Remove reviews that violate rules\
**Actor:** On-site Staff\
**Feature:** F-02 Reviews & QR\
**Login required:** Yes (staff credentials and required role are checked by FR-04-07 and FR-04-08)\
**Source:** AD-UC-13 · FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-07, FR-04-08, FR-04-12

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F02-04 | Reported Reviews | On-site Staff | F-02 | On-site Staff open the reported reviews area to retrieve and view reviews reported by readers. Staff select a reported review, inspect it, and decide whether it violates the library's review rules. They can choose to remove a violating review or dismiss the report when the review follows the rules. The list is refreshed when staff handle another report. If no reports are waiting, the screen displays an empty-state message. | Staff page after staff sign-in (`S-F00-02`) → Reported Reviews | UC-13 · FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-12. Staff access requires FR-04-07 and FR-04-08. | Must | `screens/screen-spec-S-F02-04.md` |

**Priority note:** S-F02-04 is Must because UC-13 supports the staff moderation flow: retrieving reported reviews (FR-02-14), removing a review from public display after confirmation (FR-02-10), and dismissing a report while keeping the review public (FR-02-20). The empty-list message (FR-02-19) and audit entry after removal (FR-04-12) are states/system outcomes of this screen, not separate screens.

**Shared screens, not defined here**

- `S-F00-02` Staff sign in / staff page access (FR-04-07, FR-04-08): On-site Staff submit internal library account credentials. If credentials and the required role are valid, the system starts a staff session and opens the staff page. This is a shared access screen, not specific to UC-13.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| Confirm removal of reported review | S-F02-04 | Staff confirm or cancel removal of the selected review (FR-02-10). If confirmed, the system removes the review from public display and writes an audit entry (FR-04-12). If cancelled, the review remains public and stays in the reported-reviews list. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Staff sign in | A shared platform screen (`S-F00-02`), not specific to UC-13. |
| Check staff session and role (FR-04-08) | A system access-control step; it determines whether the moderation page can be opened. |
| Deny access to the moderation page (FR-04-08) | An access-control outcome, not a separate screen; the request is denied when there is no valid staff session and role. |
| Sign in now? | A decision in the activity flow, not a screen. If staff choose Yes, they use the shared staff sign-in screen (`S-F00-02`); if No, the request ends. |
| Retrieve the reported reviews (FR-02-14) | A system action that loads the content displayed on S-F02-04, not a separate screen. |
| No reported reviews are waiting (FR-02-19) | An empty state of S-F02-04, not a separate screen. |
| Select and inspect a reported review | An action performed on S-F02-04, not a separate screen. |
| Decide whether the review violates the rules | A staff judgement on S-F02-04; the system does not judge review content. |
| Choose Remove on the review | An action on S-F02-04 that opens the confirmation modal, not a separate screen. |
| Cancel the removal confirmation | An action of the confirmation modal; the review remains public and stays in the reported list. |
| Remove the review from public display (FR-02-10) | A system action after staff confirm removal; the resulting update is a state of S-F02-04. |
| Write an audit entry for the review removal (FR-04-12) | A system record created after removal, not a staff-facing screen. |
| Dismiss the report (FR-02-20) | An action on S-F02-04; the review stays public and is removed from the reported-reviews list. |
| Handle another reported review? | A decision in the activity flow; choosing Yes reloads the reported-reviews list on S-F02-04, while choosing No ends the activity. |
| Notify the review author | Not included in this release; the modelling decision states that no notice is sent when a review is removed. |

## On-site Staff actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-13.

| AD-UC-13 node | On-site Staff action | Screen |
|---|---|---|
| a1 | Open the reported reviews | S-F02-04 |
| d1 | Choose whether to sign in now | S-F00-02 (if Yes); no screen if No |
| a2 | Sign in with the internal library account | S-F00-02 |
| a3 | Select a reported review | S-F02-04 |
| d3 | Judge whether the review violates the rules | S-F02-04 |
| a4 | Choose Remove on the review | S-F02-04 |
| d4 | Confirm or cancel the removal | Modal "Confirm removal of reported review" |
| a5 | Dismiss the report when the review follows the rules | S-F02-04 |
| d5 | Choose whether to handle another reported review | S-F02-04 |
