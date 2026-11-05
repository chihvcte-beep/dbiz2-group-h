# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-10 Print QR code labels for physical books (QR codes are generated automatically)\
**Actor:** On-site Staff; the automatic QR generation is started by time (daily sync finished)\
**Feature:** F-02 Reviews & QR\
**Login required:** Yes (staff session and role are checked by FR-04-08; staff sign-in is FR-04-07)\
**Source:** AD-UC-10 · FR-02-07, FR-02-08, FR-02-17, FR-02-18, FR-04-07, FR-04-08, FR-04-12

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F02-03 | QR Code Label Printing | On-site Staff | F-02 | On-site Staff select physical books on the staff page and choose Print labels. The screen supports selecting at least one book, receiving the printable QR label sheet, and printing it. If some selected books do not have QR codes, they are left out and listed to staff; if none has a QR code, no sheet is produced. A successful label print also creates an audit entry. | Staff page after staff sign-in (`S-F00-02`) → QR Code Label Printing | UC-10 · FR-02-08, FR-02-17, FR-02-18, FR-04-12. Staff access requires FR-04-07 and FR-04-08. | Must | `screens/screen-spec-S-F02-03.md` |

**Priority note:** S-F02-03 is Must because FR-02-08 requires the system to produce a printable QR label sheet for selected books. FR-02-17 and FR-02-18 define the selection and missing-QR handling, while FR-04-12 requires an audit entry for every label print. The screen's empty-selection, partial-result and no-label outcomes are states of this same screen, not separate screens.

**Shared screens, not defined here**

- `S-F00-02` Staff sign in / staff page access (FR-04-07, FR-04-08): On-site Staff submit internal library account credentials. If they are not signed in, they can choose to sign in; a successful sign-in starts a staff session and returns them to the book selection. The staff page requires a valid session and role. This is a shared access screen, not specific to UC-10.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| None specified | — | AD-UC-10 does not define a confirmation modal or overlay for printing QR code labels. The sign-in choice and book-selection feedback are represented as flow decisions and screen states, not separate modal requirements. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Staff sign in | A shared platform screen (`S-F00-02`), not specific to UC-10. |
| Check the staff session and role (FR-04-08) | A system access-control step; it determines whether the print request is allowed. |
| Sign in now? | A decision in the activity flow, not a screen. If staff choose Yes, they use the shared staff sign-in screen (`S-F00-02`); if No, the request ends. |
| Deny the request (FR-04-08) | An access-control outcome, not a separate screen; no label sheet is produced. |
| Ask staff to select at least one physical book (FR-02-17) | An empty-selection state or validation message on S-F02-03, not a separate screen. |
| Leave out books without a QR code and list them to staff (FR-02-18) | A partial-result state on S-F02-03; the system lists books without QR codes while producing labels for the selected books that do have QR codes. |
| No QR label sheet produced when no selected book has a QR code | A no-result state of S-F02-03, not a separate screen. |
| Produce the printable QR label sheet (FR-02-08) | The output of the S-F02-03 action, not a separate navigable screen. |
| Receive and print the QR code labels | Staff actions associated with the output of S-F02-03, not separate screens. |
| Write an audit entry for the label print (FR-04-12) | A system record created after a label sheet is produced; it has no staff-facing screen in AD-UC-10. |
| Automatic QR generation after the daily catalogue sync (FR-02-07) | A time-triggered background process. The system finds books added by the sync and generates a unique QR code for each new physical book without one; no person navigates to a screen to start it. |
| Online-only books | They do not receive QR codes under the UC-10 business rule, so no QR-generation or label action is defined for them. |

## On-site Staff actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-10.

| AD-UC-10 node | On-site Staff action | Screen |
|---|---|---|
| a1 | Select physical books on the staff page | S-F02-03 |
| a2 | Choose Print labels | S-F02-03 |
| s0 / d0 | Check the staff session and role / decide whether the session and role are valid | No screen (system access-control step) |
| d1 / a3 | Choose whether to sign in / sign in with the internal library account | S-F00-02 |
| s1 | Deny the request when there is no valid staff session and staff decline to sign in | No screen (access-control outcome) |
| d2 / s2 | Check whether at least one book is selected / ask staff to select at least one physical book | S-F02-03 (validation state) |
| d3 / s3 / d4 | Check selected books for QR codes / list books without QR codes / determine whether any selected book remains | S-F02-03 (result state) |
| s4 / s5 | Produce the printable QR label sheet / write an audit entry for the label print | S-F02-03 (system actions) |
| a4 / a5 | Receive the printable QR label sheet / print the QR code labels | S-F02-03 |
| t1 / s6 / d5 / s7 | Daily sync finishes / find newly added books / check for new physical books without QR codes / generate unique QR codes | No screen (automatic time-triggered background process) |
