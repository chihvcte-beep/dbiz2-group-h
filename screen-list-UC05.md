# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-05 View book reviews\
**Actor:** Reader\
**Feature:** F-02 Reviews & QR\
**Login required:** No\
**Source:** AD-UC-05 · FR-02-02, FR-02-13, FR-02-15 · FR-02-09 through the call to UC-14

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F02-01 | Book Reviews | Reader | F-02 | A reader wants to read the reviews of a book, one page at a time, without any removed review. The reader can ask for the next page when more reviews exist, and can select Report on a review. When the book has no reviews, the screen shows a one-line message that there are no reviews to show. | Existing OPAC Book Detail (S-F03-03) → Reviews | UC-05 · FR-02-02, FR-02-13, FR-02-15. Shared with UC-04 (write, edit and delete own review) | Must | `screens/screen-spec-S-F02-01.md` |

**Priority note:** S-F02-01 is Must because FR-02-02, FR-02-13 and FR-02-15 are all Must. Reporting a
review (FR-02-09, Could) is an action on this screen and belongs to UC-14, so it does not change the
priority.

**Related screen, not defined here:** `S-F02-02` Book Information and Reviews (QR landing page, UC-06)
shows the reviews of a book with the same rules as UC-05. It is not a screen of UC-05; the ID is only
mentioned so that the lists of UC-04, UC-05 and UC-06 use the same IDs.

## Modals and overlays

No modals or overlays are identified in the project documents for UC-05. The report form and its
confirmation belong to UC-14.

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Ask for the next page of reviews (FR-02-02) | An action on S-F02-01. The next page is offered only when more reviews exist. |
| "No reviews to show" message (FR-02-15) | The empty state of S-F02-01. It covers a book that has no reviews and a book that is not found. |
| Leave out removed reviews (FR-02-13) | A system rule applied to the list; it has no user interface of its own. |
| Find the book and find its reviews (FR-02-02) | System steps with no screen of their own. |
| Report a review (UC-14, FR-02-09) | Starts from an action on S-F02-01; the report itself belongs to UC-14 and is listed in the screen list of UC-14. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-05.

| AD-UC-05 node | Reader action | Screen |
|---|---|---|
| r1 | Ask to see the reviews of a book | S-F02-01 |
| d4 | What does the reader do next? | S-F02-01 |
| r2 | Ask for the next page of reviews | S-F02-01 |
| c1 | Report a review (UC-14) | Starts on S-F02-01; continues in UC-14 (not in this list) |
