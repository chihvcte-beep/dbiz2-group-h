# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-04 Write, edit and delete own book reviews\
**Actor:** Reader\
**Feature:** F-02 Reviews & QR\
**Login required:** Yes (checked by FR-04-08; sign-in is UC-11)\
**Source:** AD-UC-04 · FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12 · FR-04-08 and FR-04-01 through the sign-in step

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F02-01 | Book Reviews | Reader | F-02 | A reader looks at the reviews of a book and, when signed in, writes a new review, edits own review, or deletes own review on the same page. After a review is saved, replaced or removed, the reader sees a confirmation and the updated list here. | Existing OPAC Book Detail (S-F03-03) → Reviews | UC-04 · FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12. Shared with UC-05 (FR-02-02, FR-02-13, FR-02-15) | Must | `screens/screen-spec-S-F02-01.md` |

**Priority note:** S-F02-01 is Must because FR-02-01 (write), FR-02-11 and FR-02-12 are Must. The Edit
action (FR-02-03) and the Delete action (FR-02-04) are Could: if they are cut, the screen stays and
only those actions are removed.

**Shared screens, not defined here**

- `S-F00-01` Sign in (UC-11, FR-04-01): opened when a reader without a valid session asks for a review action and chooses to sign in.
- `S-F02-02` Book Information and Reviews (QR landing page, UC-06): UC-06 calls UC-04 from it, so Write, Edit and Delete can also start there. It is not a screen of UC-04; the ID is only mentioned so that the lists of UC-04, UC-05 and UC-06 use the same IDs.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| Confirm deletion of own review | S-F02-01 | The reader confirms or cancels the removal of own review (FR-02-04). Cancel ends the activity with the review still public. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Review form (write a new review, edit own review) | Part of S-F02-01; the review form has no screen of its own. |
| Sign in | A shared platform screen (`S-F00-01`), not specific to UC-04. |
| Check the reader's session and deny the request (FR-04-08) | A system step with no screen of its own; a reader without a session is sent to sign in or the request ends. |
| Write review, Edit and Delete buttons | Actions on S-F02-01, not screens. |
| Cancel the deletion | An action of the confirmation modal, not a screen. |
| Error message for a rejected review action (FR-02-11) | An error state of S-F02-01 (text that is empty, over 2,000 characters or not plain text, or a review that is not the reader's own). |
| Confirmation and updated review list (FR-02-12) | The success state of S-F02-01, shown after a review is saved, replaced or removed. |
| Check the review text (FR-02-01, FR-02-03) | A system step; the result appears as the error state of S-F02-01. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-04.

| AD-UC-04 node | Reader action | Screen |
|---|---|---|
| r1 | Request a review action on a book | S-F02-01 |
| d1 / c1 | Sign in now? / Sign in (UC-11) | S-F00-01 |
| d2 | Which action? (Write, Edit or Delete) | S-F02-01 |
| r2 | Submit a new review text | S-F02-01 |
| r3 | Submit an edited text of own review | S-F02-01 |
| r4 | Choose own review to delete | S-F02-01 |
| d6 | Confirm the deletion? | Modal "Confirm deletion of own review" |
| r5 | Cancel the deletion | Modal "Confirm deletion of own review" |
