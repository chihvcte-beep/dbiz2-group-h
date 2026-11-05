# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-03 Filter books by access format (online, physical or both)\
**Actor:** Reader\
**Feature:** F-03 Discovery, Reading History & Recommendation\
**Login required:** No (a signed-in library-card reader receives a reading-history entry; FR-03-02)\
**Source:** AD-UC-03 · FR-03-12, FR-03-23, FR-03-13, FR-03-02

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F03-01 | Book Catalogue & Access Format Filter | Reader | F-03 | A reader opens the access-format filter and chooses one of the three available options: Online, Physical or Both. The screen displays matching books with an access-format label. If no books match, it displays a message and lets the reader choose another format. From the results, the reader can open an online book on the current OPAC. | Existing OPAC book catalogue / search results → Access-format filter | UC-03 · FR-03-12, FR-03-23, FR-03-13, FR-03-02 | Must | `screens/screen-spec-S-F03-01.md` |

**Priority note:** S-F03-01 is Must because FR-03-12 requires readers to filter the catalogue by Online, Physical or Both, and FR-03-23 requires an empty result to invite another format choice. Opening an online book from the results also triggers the read-log and, for a signed-in library-card reader, reading-history behaviour (FR-03-13 and FR-03-02).

**Shared screens, not defined here**

- The current OPAC's online-book page is an existing destination, not a new screen delivered by this platform. W0 Table 3 excludes building a viewer or download function; the reader follows the result link to the current OPAC.

## Modals and overlays

| Modal | Opened from screen | Purpose |
|---|---|---|
| None specified | — | AD-UC-03 does not define any confirmation dialog or overlay. Format selection, empty-result feedback and result display are states or actions on S-F03-01. |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Choose Online, Physical or Both | A filter-selection action on S-F03-01, not a separate screen. |
| Retrieve books in the selected access format (FR-03-12) | A system step that updates the results shown on S-F03-01. |
| Matching book results with access-format labels (FR-03-12) | The results state of S-F03-01, not a separate screen. |
| No books found (FR-03-23) | An empty-result state of S-F03-01; the reader can choose another format from the same screen. |
| Choose another access format | An action that returns to the filter selection on S-F03-01, not a separate screen. |
| Open an online book from the results | An action from S-F03-01 that hands the reader over to the current OPAC. |
| Current OPAC online-book viewer or download | An existing OPAC destination; this project does not build a viewer or download function (W0 Table 3). |
| Record the book and time of the read without reader identity (FR-03-13) | A background system action triggered when an online book is opened; it does not require a separate screen. |
| Check whether the reader is signed in with a library card | A system check that determines whether a reading-history entry is created; it is not a screen. |
| Add the book to the reader's reading history (FR-03-02) | A background system action for a signed-in library-card reader; no separate screen is specified in AD-UC-03. |
| Finish filtering | An action that ends the activity while the result list remains on S-F03-01. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-03.

| AD-UC-03 node | Reader action | Screen |
|---|---|---|
| r1 | Open the access-format filter | S-F03-01 |
| r2 | Choose an access format: Online, Physical or Both | S-F03-01 |
| d2 | Choose another access format | S-F03-01 |
| r3 | Open an online book from the results | S-F03-01 → current OPAC online-book page (existing destination) |
| s1 / d1 | Retrieve books in the selected format / check whether matching books exist | S-F03-01 (system action and results state) |
| s2 | Display matching books with their access-format labels | S-F03-01 |
| s3 | Display that no books were found | S-F03-01 (empty-result state) |
| s4 | Record the book and time of the read without reader identity | No screen (background system action) |
| d3 | Check whether the reader is signed in with a library card | No screen (system check) |
| s5 | Add the book to the reader's reading history | No screen (background system action) |
