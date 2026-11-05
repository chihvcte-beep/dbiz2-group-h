# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-14 Report a review that violates rules\
**Actor:** Reader\
**Feature:** F-02 Reviews & QR\
**Login required:** Yes (checked by FR-04-08; sign-in is UC-11)\
**Source:** AD-UC-14 · FR-02-09, FR-02-21, FR-04-08 · FR-04-01 through the sign-in step (UC-11)

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F02-01 | Book Reviews | Reader | F-02 | A reader views a book's reviews and selects Report on a review. The system checks the reader's session; if needed, the reader can sign in and return to the report action. The screen shows either a message that the review has already been reported or a confirmation after the report is saved. | Existing OPAC Book Detail → Reviews (UC-05) | UC-14 · FR-02-09, FR-02-21, FR-04-08. Shared with UC-04 (FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12) and UC-05. | Must | `screens/screen-spec-S-F02-01.md` |

**Priority note:** S-F02-01 is Must because FR-02-09 requires the system to save a report against the selected review, and FR-02-21 prevents the same reader from reporting the same review more than once. Reporting is an action on the existing Book Reviews screen; no separate report screen is defined.

**Shared screens, not defined here**

- `S-F00-01` Sign in (UC-11, FR-04-01): opened when a reader without a valid session chooses to sign in after selecting Report. After successful sign-in, the flow returns to the report action and checks the session again. This is a shared platform screen, not specific to UC-14.
- `S-F02-01` Book Reviews is shared with UC-04 and UC-05. UC-14 adds the Report action to the existing review display; it does not introduce another review-list screen.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| None specified | — | AD-UC-14 does not define a confirmation modal or overlay. The Reader selects Report directly on the Book Reviews screen; duplicate-report and submission feedback are screen states. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Sign in | A shared platform screen (`S-F00-01`, UC-11), not specific to UC-14. |
| Open the reviews of a book (UC-05) | Uses the existing Book Reviews screen (`S-F02-01`); UC-14 does not create another review-list screen. |
| Select Report on a review | An action on S-F02-01, not a separate screen. |
| Check the reader's session (FR-04-08) | A system access-control step; it determines whether the report request can proceed. |
| Ask whether the reader wants to sign in | A decision in the activity flow, not a separate screen. If the reader chooses Yes, they use the shared sign-in screen; if No, the request ends and no report is saved. |
| Deny the request without a valid reader session (FR-04-08) | An access-control outcome, not a separate screen. |
| Sign in (UC-11) | A call to the shared UC-11 sign-in use case, not a screen specific to UC-14. |
| Submit the report for the selected review | An action performed on S-F02-01, not a separate screen. |
| Check whether the reader has already reported this review (FR-02-21) | A system validation step; its result is displayed on S-F02-01. |
| Message that the review has already been reported (FR-02-21) | An informational state of S-F02-01; no second report is saved. |
| Save the report against the selected review (FR-02-09) | A system action after the session and duplicate-report checks, not a separate screen. |
| Report-submitted confirmation (FR-02-09) | A success state of S-F02-01, not a separate screen. |
| Remove the reported review from public display (FR-02-10) | A downstream staff process handled by UC-13; UC-14 ends when the report is saved and confirmed. The review remains public until staff handle it. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-14.

| AD-UC-14 node | Reader action | Screen |
|---|---|---|
| r1 | Select Report on a review | S-F02-01 |
| d1 | Choose whether to sign in now | No screen (activity-flow decision) |
| c1 | Sign in (UC-11) | S-F00-01 |
| r2 | Submit the report for the selected review | S-F02-01 |
| s0 / d0 | Check the reader's session / determine whether the session is valid | No screen (system access-control step) |
| s1 | Deny the request without a valid session | No screen (access-control outcome) |
| d2 | Check whether the reader has already reported this review | No screen (system validation step) |
| s2 | Display that the review has already been reported | S-F02-01 (informational state) |
| s3 / s4 | Save the report / display a confirmation | S-F02-01 (system action and success state) |
