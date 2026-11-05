# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-12 Save physical books to a personal list and remove them\
**Actor:** Reader\
**Feature:** F-03 Discovery, Reading History & Recommendation\
**Login required:** Yes (checked by FR-04-08; sign-in is UC-11)\
**Source:** AD-UC-12 · FR-03-06, FR-03-07, FR-03-08, FR-03-24, FR-03-25, FR-01-07, FR-04-08 · FR-04-01 through the sign-in step

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F03-03 | Saved Books List | Reader | F-03 | A signed-in reader opens their saved-books list to view saved physical books and each book's synced shelf location. The reader can remove a saved book from this screen. The screen also displays an empty-list message when no books have been saved, and shows shelf location as unavailable when the location is missing or inconsistent. | Reader account / personal area after sign-in (`S-F00-01`) → Saved Books List | UC-12 · FR-03-07, FR-03-08, FR-03-25, FR-01-07. The list reflects books saved under FR-03-06 and prevents duplicate entries under FR-03-24. Access requires FR-04-08. | Must | `screens/screen-spec-S-F03-03.md` |

**Priority note:** S-F03-03 is Must because FR-03-07 requires readers to view saved physical books with their shelf locations, and FR-03-08 allows them to remove books from the list. FR-03-25 defines the empty-list message, while FR-01-07 defines how unavailable shelf locations are displayed. Saving a book is an action from the existing book display and does not require a separate UC-12 screen.

**Shared screens, not defined here**

- `S-F00-01` Sign in (UC-11, FR-04-01): opened when a reader without a valid session chooses to sign in. After successful sign-in, the flow returns to the saved-books request and checks the session again. This is a shared platform screen, not specific to UC-12.
- Existing OPAC book detail / catalogue display: the Reader selects Save on a physical book from the existing book display. UC-12 adds the Save action to that existing screen; it does not define a new book-detail screen.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| None specified | — | AD-UC-12 does not define a confirmation dialog or overlay. The Reader selects Remove directly from the saved-books list; duplicate-save, empty-list and unavailable-location feedback are states of the relevant screen. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Sign in | A shared platform screen (`S-F00-01`, UC-11), not specific to UC-12. |
| Check the reader's session (FR-04-08) | A system access-control step; it determines whether the saved-books request is allowed. |
| Ask whether the reader wants to sign in | A decision in the activity flow, not a separate screen. If the reader chooses Yes, they use the shared sign-in screen; if No, the request ends without access. |
| Deny access without a valid reader session (FR-04-08) | An access-control outcome, not a separate screen. |
| Select Save on a physical book (FR-03-06) | An action on the existing OPAC book display, not a separate UC-12 screen. |
| Check whether the book is already in the saved list (FR-03-24) | A system validation step; its result is displayed on the existing book display or saved-list flow. |
| Message that the book is already saved (FR-03-24) | An informational state, not a separate screen; no duplicate entry is added. |
| Add the book to the reader's saved-books list (FR-03-06) | A system action performed after the Save action, not a separate screen. |
| Retrieve saved books with synced shelf locations (FR-03-07) | A system retrieval step; the resulting list is displayed on S-F03-03. |
| Empty saved-books list (FR-03-25) | An empty state of S-F03-03, not a separate screen. |
| Missing or inconsistent shelf location (FR-01-07) | A data/display state of the relevant saved-book entry on S-F03-03; it is shown as unavailable and directs the reader to library staff. |
| Display saved books with shelf locations (FR-03-07) | The main content state of S-F03-03, not a separate screen. |
| Choose whether to remove a saved book | A decision/action on S-F03-03, not a separate screen. |
| Select Remove on a saved book (FR-03-08) | An action on S-F03-03, not a separate screen. |
| Delete a book from the saved-books list (FR-03-08) | A system action performed after the Reader selects Remove; the refreshed list is shown on S-F03-03. |
| Reload the saved-books list after removal | An updated state of S-F03-03, not a separate screen. |
| Online-only books | Save is offered only for physical books under the UC-12 scope; no screen or save action is defined for online-only books. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-12.

| AD-UC-12 node | Reader action | Screen |
|---|---|---|
| r1 | Request a saved-books action | No separate screen (entry action that leads to the protected UC-12 flow) |
| d1 | Choose whether to sign in now | No screen (activity-flow decision) |
| c1 | Sign in (UC-11) | S-F00-01 |
| d2 | Choose Save a book, View saved books, or Finish | Existing book display / S-F03-03, depending on the chosen action |
| r2 | Select Save on a physical book | Existing OPAC book detail / catalogue display (shared screen) |
| r3 | Open the saved books list | S-F03-03 |
| d6 / r4 | Choose whether to remove a saved book / select Remove | S-F03-03 |
| s0 / d0 | Check the reader's session / determine whether the session is valid | No screen (system access-control step) |
| s1 | Deny access without a valid session | No screen (access-control outcome) |
| d3 / s2 / s3 | Check for an existing saved entry / display that it is already saved / add the book to the saved list | Existing book display or S-F03-03 (system validation, feedback or data update) |
| s4 / d4 | Retrieve saved books with shelf locations / check whether the list is empty | S-F03-03 (system action and display state) |
| s5 | Display that no books have been saved yet | S-F03-03 (empty-list state) |
| d5 / s6 | Check for missing or inconsistent shelf location / show location unavailable and direct the reader to library staff | S-F03-03 (location state) |
| s7 | Display saved books with the shelf location of each book | S-F03-03 |
| s8 | Delete the selected book from the saved-books list | S-F03-03 (system action; refreshed-list state) |
