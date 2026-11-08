# Screen List: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: docs/external-design/screen-list.md
One row per screen. A screen is a place the user navigates to (a page or route). Loading, empty,
error and success are STATES of a screen and are written in its Screen Spec, not here. A dialog
that only confirms or cancels an action (for example "Delete this post?") is a MODAL of the screen
that opens it, not a separate screen.
-->

**Use case:** UC-06 Access book information and reviews via QR code\
**Actor:** Reader\
**Feature:** F-02 Reviews & QR\
**Login required:** No\
**Source:** AD-UC-06 · FR-02-05, FR-02-06, FR-02-16 · FR-02-01, FR-02-03, FR-02-04 through the calls to UC-04

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in, settings) use `S-F00-<nn>`.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F02-02 | Book Information and Reviews (QR landing page) | Reader | F-02 | A reader scans the QR code on a physical book and wants the information and the reviews of that book on a phone. The reader can start writing, editing or deleting own review from here. When the QR code is linked to no book, the screen shows that the book cannot be found. | Scan of the QR code on a physical book | UC-06 · FR-02-05, FR-02-16 | Must | `screens/screen-spec-S-F02-02.md` |

**Priority note:** S-F02-02 is Must because FR-02-05 and FR-02-16 are Must. Counting the scan
(FR-02-06) has no user interface, so it does not change the priority of the screen.

**Related screen, not defined here:** `S-F02-01` Book Reviews (UC-05) shows the reviews of a book
from the existing OPAC. It is not a screen of UC-06; the ID is only mentioned so that the lists of
UC-04, UC-05 and UC-06 use the same IDs.

## Modals and overlays

No modals or overlays are identified in the project documents for UC-06. The confirmation of a
deletion belongs to UC-04.

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Find the book linked to the QR code (FR-02-05) | A system step with no screen of its own. |
| Count the QR code scan (FR-02-06) | A background system event that raises the scan count; it has no user interface. |
| "The book cannot be found" message (FR-02-16) | An error state of S-F02-02, shown when the QR code is linked to no book. |
| Write, edit or delete own review (UC-04) | Starts from an action on S-F02-02 and continues in UC-04; it is listed in the screen list of UC-04. |
| Sign in | Needed only when the reader acts on a review; it is a shared platform screen (`S-F00-01`) reached through UC-04. |

## Reader actions mapped to screens

This table also fills section 5 "Screens touched" of AD-UC-06.

| AD-UC-06 node | Reader action | Screen |
|---|---|---|
| r1 | Scan the QR code on a physical book | S-F02-02 |
| d2 | Act on a review? | S-F02-02 |
| c1 | Write a review (UC-04) | Starts on S-F02-02; continues in UC-04 (not in this list) |
| c2 | Edit own review (UC-04) | Starts on S-F02-02; continues in UC-04 (not in this list) |
| c3 | Delete own review (UC-04) | Starts on S-F02-02; continues in UC-04 (not in this list) |
