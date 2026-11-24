# Functional Requirements: Group H Library Core System

Every functional requirement (FR) of the product, with its acceptance criterion, source, dependencies, priority and the work items it splits into. **This file is the source of truth for FRs** from 23/11/2026 (D51). It holds no effort or cost: those are in [cost.md](cost.md).

| Field | Value |
|---|---|
| Version | v1.0 · 23/11/2026 |
| Exported from | Sheets W1_FunctionList and W4_Prioritization of [GROUP-H_UC_FR_COST.xlsx @ cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/blob/cd61897/%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx) (frozen, read-only). Documents that cite "W1" mean the FR sections of this file; "W4" means the Priority field and [Priority changes](#priority-changes-w4). |
| Counts | 81 FRs (L2) · 136 work items (L3) · Must 33, Should 17, Could 24, Won't 7 |
| How to change | Edit the FR here, in the same commit add the decision row to [decision-index.md](../project/decision-index.md) that explains it, and tell the cost owner to update the matching rows of [cost.md](cost.md). Never reuse a removed FR ID. |

## How to read an FR

- **ID** `FR-<feature>-<nn>`. Work items (L3) add the layer: `-FE` screen, `-BE` server, `-INT` integration.
- **Criterion** is written in EARS form (WHEN / IF … THEN … the system SHALL …).
- **Priority** is the effective priority after the W4 review. Rules R1–R4 are in [Priority rules](#priority-rules-w4).
- **Won't** rows stay in the list so their IDs are never reused; they are out of scope, see [scope.md](scope.md#table-3-wont-have).
- **Hidden work** = Yes marks technical work no user asked for directly (floor plan, sync, deploy, tests).

## Summary

| FR | Name | Feature | Use cases | Priority |
|---|---|---|---|---|
| [FR-01-01](#fr-01-01) | View book shelf location | F-01 | UC-01 | Must |
| [FR-01-02](#fr-01-02) | Browse the digital library map | F-01 | UC-02 | Must |
| [FR-01-03](#fr-01-03) | Show a book's room on the map | F-01 | UC-01, UC-02 | Could |
| [FR-01-04](#fr-01-04) | Prepare the digital floor plan | F-01 | – | Must |
| [FR-01-05](#fr-01-05) | Check room codes against the internal system | F-01 | UC-15 | Should |
| [FR-01-06](#fr-01-06) | Show that an online-only book has no shelf location | F-01 | UC-01 | Must |
| [FR-01-07](#fr-01-07) | Handle a missing or inconsistent shelf location | F-01 | UC-01, UC-12 | Must |
| [FR-01-09](#fr-01-09) | Handle a room not found on the floor plan | F-01 | UC-01, UC-02 | Could |
| [FR-01-10](#fr-01-10) | Handle an unavailable floor plan | F-01 | UC-01, UC-02 | Must |
| [FR-01-11](#fr-01-11) | Select a reading room on the map | F-01 | UC-02 | Must |
| [FR-02-01](#fr-02-01) | Write a book review | F-02 | UC-04 | Must |
| [FR-02-02](#fr-02-02) | View book reviews | F-02 | UC-05 | Must |
| [FR-02-03](#fr-02-03) | Edit own review | F-02 | UC-04 | Could |
| [FR-02-04](#fr-02-04) | Delete own review | F-02 | UC-04 | Could |
| [FR-02-05](#fr-02-05) | Open book information and reviews via QR code | F-02 | UC-06 | Must |
| [FR-02-06](#fr-02-06) | Count QR code scans | F-02 | UC-06 | Could |
| [FR-02-07](#fr-02-07) | Generate QR codes for new physical books | F-02 | UC-10 | Must |
| [FR-02-08](#fr-02-08) | Print QR code labels | F-02 | UC-10 | Must |
| [FR-02-09](#fr-02-09) | Report a review that breaks the rules | F-02 | UC-14 | Could |
| [FR-02-10](#fr-02-10) | Review and remove reported reviews | F-02 | UC-13 | Could |
| [FR-02-11](#fr-02-11) | Reject invalid review actions | F-02 | UC-04 | Must |
| [FR-02-12](#fr-02-12) | Confirm review changes | F-02 | UC-04 | Must |
| [FR-02-13](#fr-02-13) | Hide removed reviews from the list | F-02 | UC-05 | Must |
| [FR-02-14](#fr-02-14) | View the reported-reviews list | F-02 | UC-13 | Could |
| [FR-02-15](#fr-02-15) | End a review request with nothing to show | F-02 | UC-05 | Must |
| [FR-02-16](#fr-02-16) | Handle a QR code linked to no book | F-02 | UC-06 | Must |
| [FR-02-17](#fr-02-17) | Require at least one book for label printing | F-02 | UC-10 | Must |
| [FR-02-18](#fr-02-18) | Leave books without a QR code out of the label sheet | F-02 | UC-10 | Must |
| [FR-02-19](#fr-02-19) | Show an empty reported-reviews list | F-02 | UC-13 | Could |
| [FR-02-20](#fr-02-20) | Dismiss a report on a review that follows the rules | F-02 | UC-13 | Could |
| [FR-02-21](#fr-02-21) | Reject a duplicate report | F-02 | UC-14 | Could |
| [FR-02-22](#fr-02-22) | Post a review under the reader's name or anonymously | F-02 | UC-04, UC-06 | Should |
| [FR-02-23](#fr-02-23) | List physical books awaiting a QR label | F-02 | UC-10 | Must |
| [FR-02-24](#fr-02-24) | Reject a report on the reader's own review | F-02 | UC-14 | Could |
| [FR-02-25](#fr-02-25) | Reprint QR labels for labelled books | F-02 | UC-10 | Should |
| [FR-03-01](#fr-03-01) | View reading history | F-03 | UC-07 | Should |
| [FR-03-02](#fr-03-02) | Add a history entry when an online book is opened from this platform | F-03 | UC-07, UC-03 | Should |
| [FR-03-03](#fr-03-03) | Add history entries from borrowed physical books | F-03 | UC-07 | Should |
| [FR-03-04](#fr-03-04) | Mark reading status and progress | F-03 | UC-07 | Should |
| [FR-03-05](#fr-03-05) | Set reading preferences | F-03 | UC-07 | Could |
| [FR-03-06](#fr-03-06) | Save a physical book to a personal list | F-03 | UC-12 | Should |
| [FR-03-07](#fr-03-07) | View saved books with shelf locations | F-03 | UC-12 | Should |
| [FR-03-08](#fr-03-08) | Remove a saved book | F-03 | UC-12 | Could |
| [FR-03-09](#fr-03-09) | Search books by chatting with the AI chatbot | F-03 | UC-08 | Could |
| [FR-03-10](#fr-03-10) | Save chatbot conversations per reader | F-03 | UC-08 | Could |
| [FR-03-11](#fr-03-11) | Recommend books automatically | F-03 | UC-09 | Could |
| [FR-03-12](#fr-03-12) | Filter books by access format | F-03 | UC-03 | Should |
| [FR-03-13](#fr-03-13) | Log anonymous online-book reads | F-03 | UC-03 | Could |
| [FR-03-14](#fr-03-14) | View access formats of a book | F-03 | UC-03 | Won't |
| [FR-03-15](#fr-03-15) | Download the PDF of an online book | F-03 | UC-03 | Won't |
| [FR-03-16](#fr-03-16) | Reply when the chatbot finds no books | F-03 | UC-08 | Could |
| [FR-03-17](#fr-03-17) | Handle an unavailable AI service | F-03 | UC-08 | Could |
| [FR-03-18](#fr-03-18) | Prompt sign-in before chatting | F-03 | UC-08 | Could |
| [FR-03-19](#fr-03-19) | Recommend popular books when there is no reader data | F-03 | UC-09 | Could |
| [FR-03-20](#fr-03-20) | Top up short recommendation lists | F-03 | UC-09 | Could |
| [FR-03-21](#fr-03-21) | Prompt sign-in for recommendations | F-03 | UC-09 | Could |
| [FR-03-22](#fr-03-22) | Reject invalid reading history or preference updates | F-03 | UC-07 | Should |
| [FR-03-23](#fr-03-23) | Show no results for an access-format filter | F-03 | UC-03 | Should |
| [FR-03-24](#fr-03-24) | Reject saving a book twice | F-03 | UC-12 | Should |
| [FR-03-25](#fr-03-25) | Show an empty saved books list | F-03 | UC-12 | Should |
| [FR-04-01](#fr-04-01) | Sign in with library card and email OTP | F-04 | UC-11 | Must |
| [FR-04-02](#fr-04-02) | Register or sign in with email OTP | F-04 | UC-11 | Won't |
| [FR-04-03](#fr-04-03) | Sign in with Google | F-04 | UC-11 | Won't |
| [FR-04-04](#fr-04-04) | Send and verify email OTP | F-04 | UC-11 | Must |
| [FR-04-05](#fr-04-05) | Link an online account to a library card | F-04 | UC-11 | Won't |
| [FR-04-06](#fr-04-06) | Reject linking when both profiles hold data | F-04 | UC-11 | Won't |
| [FR-04-07](#fr-04-07) | Sign in On-site Staff with internal library account | F-04 | UC-10, UC-13 | Must |
| [FR-04-08](#fr-04-08) | Enforce sign-in and staff access control | F-04 | UC-04, UC-07, UC-08, UC-09, UC-12, UC-14, UC-10, UC-13 | Must |
| [FR-04-09](#fr-04-09) | Sync catalogue, shelf placement and library layout | F-04 | UC-15 | Must |
| [FR-04-10](#fr-04-10) | Sync loan records | F-04 | UC-15 | Must |
| [FR-04-11](#fr-04-11) | Handle sync failures | F-04 | UC-15 | Should |
| [FR-04-12](#fr-04-12) | Keep an audit log | F-04 | – | Must |
| [FR-04-13](#fr-04-13) | Deploy automatically | F-04 | – | Must |
| [FR-04-14](#fr-04-14) | Run automated tests on every change | F-04 | – | Must |
| [FR-04-15](#fr-04-15) | Monitor errors and availability | F-04 | – | Won't |
| [FR-04-16](#fr-04-16) | Handle a failed OTP email | F-04 | UC-11 | Must |
| [FR-04-17](#fr-04-17) | Limit incorrect OTP attempts | F-04 | UC-11 | Must |
| [FR-04-18](#fr-04-18) | Reject invalid staff sign-in | F-04 | UC-10, UC-13 | Must |
| [FR-04-19](#fr-04-19) | Show the remaining OTP attempts | F-04 | UC-11 | Should |
| [FR-04-20](#fr-04-20) | Handle a network or loading error | F-04 | – | Must |
| [FR-04-21](#fr-04-21) | Sign out of the staff page | F-04 | UC-10, UC-13 | Should |

## F-01 Book Location & Library Map

Readers see the exact shelf location of each book and browse a digital map of floors and reading rooms. Use cases: UC-01, UC-02.

<a id="fr-01-01"></a>

### FR-01-01 View book shelf location

| Field | Value |
|---|---|
| Criterion | WHEN a reader opens a book detail page and requests the shelf location, the system SHALL retrieve the format and physical location data of the book, and SHALL display the floor, room and shelf code only if the book has a physical copy and its floor, room and shelf codes are complete and consistent. |
| Source trace | UC:UC-01; DFD L0: Book placement & library layout (EIF) |
| Depends on | FR-04-09 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-01-01-FE` · FE · Screen: shelf location panel on the book detail page
- `FR-01-01-BE` · BE · API: get floor, room and shelf code by book ID

<a id="fr-01-02"></a>

### FR-01-02 Browse the digital library map

| Field | Value |
|---|---|
| Criterion | WHEN the reader requests the digital library map, the system SHALL retrieve the synchronized floor and room data and display the available floors and reading rooms. WHEN the reader requests to view another floor, the system SHALL display the selected floor's map and its reading rooms. |
| Source trace | UC:UC-02; DFD L0: Book placement & library layout (EIF) |
| Depends on | FR-01-04; FR-04-09 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-01-02-FE` · FE · Screen: interactive floor plan with floor switcher and clickable rooms
- `FR-01-02-BE` · BE · API: list floors and rooms

<a id="fr-01-03"></a>

### FR-01-03 Show a book's room on the map

| Field | Value |
|---|---|
| Criterion | WHEN a reader requests the map of the room that holds a book, the system SHALL retrieve the floor plan of the book’s floor and display the library map with that room highlighted, and SHALL keep the shelf details visible. |
| Source trace | UC:UC-01; UC:UC-02 |
| Depends on | FR-01-01; FR-01-02 |
| Priority | Could (was Should, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-01-03-FE` · FE · Screen: map view with highlighted room and deep link from book detail
- `FR-01-03-BE` · BE · API: return room map coordinates with the shelf location

<a id="fr-01-04"></a>

### FR-01-04 Prepare the digital floor plan

| Field | Value |
|---|---|
| Criterion | The system SHALL provide a digital floor plan of every floor in which each reading room carries the same room code as the internal library system. |
| Source trace | W0 Table 4 note (floor plan is a fixed asset built once by the project team) |
| Depends on | – |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-01-04-FE` · FE · Asset: draw the digital floor plan of each floor and tag every room with its room code

<a id="fr-01-05"></a>

### FR-01-05 Check room codes against the internal system

| Field | Value |
|---|---|
| Criterion | WHEN a sync run finishes, the system SHALL report every room code on the floor plan that has no matching room code in the synced layout, and every synced room code that has no room on the floor plan. |
| Source trace | UC:UC-15; Derived: W0 Table 4 note (floor plan room codes must match the internal system) |
| Depends on | FR-01-04; FR-04-09 |
| Priority | Should |
| Hidden work | Yes |

Work items (L3):

- `FR-01-05-BE` · BE · Job: compare synced room codes with floor plan room codes and report mismatches

<a id="fr-01-06"></a>

### FR-01-06 Show that an online-only book has no shelf location

| Field | Value |
|---|---|
| Criterion | IF a catalogue record indicates that a book is an electronic resource with no physical copy, THEN the system SHALL display that the book is available electronically and that no physical shelf location applies. |
| Source trace | UC:UC-01; PCCV (activity diagram edge case) |
| Depends on | FR-01-01 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-01-06-FE` · FE · Message: available electronically, no physical shelf location

<a id="fr-01-07"></a>

### FR-01-07 Handle a missing or inconsistent shelf location

| Field | Value |
|---|---|
| Criterion | IF the floor, room or shelf code of a book is missing or inconsistent, THEN the system SHALL display that the shelf location is unavailable and direct the reader to library staff. |
| Source trace | UC:UC-01; UC:UC-12; PCCV (activity diagram edge case) |
| Depends on | FR-01-01 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-01-07-FE` · FE · Message: shelf location unavailable, ask library staff
- `FR-01-07-BE` · BE · Check that floor, room and shelf codes are complete and consistent

<a id="fr-01-09"></a>

### FR-01-09 Handle a room not found on the floor plan

| Field | Value |
|---|---|
| Criterion | IF the room code of a book is not found on the retrieved floor plan, THEN the system SHALL keep the shelf details visible and display that the room cannot be identified on the map. |
| Source trace | UC:UC-01; UC:UC-02; PCCV (activity diagram edge case) |
| Depends on | FR-01-03 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-01-09-FE` · FE · Message: room cannot be identified on the map, shelf details kept

<a id="fr-01-10"></a>

### FR-01-10 Handle an unavailable floor plan

| Field | Value |
|---|---|
| Criterion | IF the digital floor plan is unavailable or unreadable, THEN the system SHALL display a map-unavailable message and SHALL retain any shelf-location details already displayed. |
| Source trace | UC:UC-01; UC:UC-02; PCCV (activity diagram edge case) |
| Depends on | FR-01-02 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-01-10-FE` · FE · Message: map unavailable, shelf details kept

<a id="fr-01-11"></a>

### FR-01-11 Select a reading room on the map

| Field | Value |
|---|---|
| Criterion | WHEN the reader selects a reading room on the library map, the system SHALL highlight that room and display its room name, room code and floor. |
| Source trace | UC:UC-02; PCCV (activity diagram edge case) |
| Depends on | FR-01-02 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-01-11-FE` · FE · Screen: highlight the selected room with its name, code and floor
- `FR-01-11-BE` · BE · API: room details by room code


## F-02 Reviews & QR

Readers write, edit, delete and read reviews of books, including by scanning a QR code on a physical book, and On-site Staff print the QR labels and remove reviews that violate rules. Use cases: UC-04, UC-05, UC-06, UC-10, UC-13, UC-14.

<a id="fr-02-01"></a>

### FR-02-01 Write a book review

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader submits a review text for a book, the system SHALL check that the text is not empty, is at most 2,000 characters and is plain text, and SHALL save it against that book and that reader only if the check passes. |
| Source trace | UC:UC-04; DFD L0: Book review (ILF) |
| Depends on | FR-04-01; FR-04-08 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-01-FE` · FE · Screen: review form
- `FR-02-01-BE` · BE · API: validate and save review

<a id="fr-02-02"></a>

### FR-02-02 View book reviews

| Field | Value |
|---|---|
| Criterion | WHEN a reader opens the reviews of a book, the system SHALL display the reviews of that book one page at a time. IF more reviews exist after the displayed page, THEN the system SHALL allow the reader to request the next page. |
| Source trace | UC:UC-05; DFD L0: Book review (ILF) |
| Depends on | FR-02-01 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-02-FE` · FE · Screen: paged review list
- `FR-02-02-BE` · BE · API: list reviews with pagination

<a id="fr-02-03"></a>

### FR-02-03 Edit own review

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader submits an edited text for their own review, the system SHALL apply the same text check as FR-02-01, and SHALL replace the review text and keep the review linked to the same book only if the check passes. |
| Source trace | UC:UC-04 (extension: edit own review, team decision); DFD L0: Book review (ILF) |
| Depends on | FR-02-01 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-03-FE` · FE · Screen: edit action on own review
- `FR-02-03-BE` · BE · API: update own review

<a id="fr-02-04"></a>

### FR-02-04 Delete own review

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader confirms the deletion of their own review, the system SHALL remove that review from public display. |
| Source trace | UC:UC-04 (extension: delete own review, team decision); DFD L0: Book review (ILF) |
| Depends on | FR-02-01 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-04-FE` · FE · Screen: delete action with confirmation on own review
- `FR-02-04-BE` · BE · API: remove own review from public display

<a id="fr-02-05"></a>

### FR-02-05 Open book information and reviews via QR code

| Field | Value |
|---|---|
| Criterion | WHEN a reader scans the QR code on a physical book, the system SHALL open the information and review page of that book. |
| Source trace | UC:UC-06; DFD L0: Book QR codes (ILF) |
| Depends on | FR-02-07; FR-02-02 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-05-FE` · FE · Screen: mobile landing page for a scanned QR code
- `FR-02-05-BE` · BE · API: resolve QR code to book

<a id="fr-02-06"></a>

### FR-02-06 Count QR code scans

| Field | Value |
|---|---|
| Criterion | WHEN a QR code is scanned, the system SHALL increase the scan count of that QR code by one. |
| Source trace | UC:UC-06; DFD L0: Book QR codes (ILF), scan counts |
| Depends on | FR-02-05 |
| Priority | Could (was Should, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-02-06-BE` · BE · Increase the scan counter on each QR code resolve

<a id="fr-02-07"></a>

### FR-02-07 Generate QR codes for new physical books

| Field | Value |
|---|---|
| Criterion | WHEN a new physical book appears in the synced catalogue, the system SHALL generate one unique QR code linked to that book title; all physical copies of the title share this code. |
| Source trace | UC:UC-10; DFD L0: Book QR codes (ILF); W0 Table 3 (no QR code for online-only books) |
| Depends on | FR-04-09 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-07-BE` · BE · Job: generate and store a unique QR code for each new physical book

<a id="fr-02-08"></a>

### FR-02-08 Print QR code labels

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff select physical books and choose Print labels, the system SHALL produce a printable sheet of QR code labels for the selected books, 24 labels per A4 page, continuing on further A4 pages when more than 24 books are selected, and WHEN the staff confirm that the sheet was printed («Đã in xong»), the system SHALL record that a label has been printed for each book on the sheet. |
| Source trace | UC:UC-10 |
| Depends on | FR-02-07; FR-02-23; FR-04-07 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-08-FE` · FE · Screen: staff page to select books and preview the label sheet
- `FR-02-08-BE` · BE · API: build the printable label sheet (PDF)

<a id="fr-02-09"></a>

### FR-02-09 Report a review that breaks the rules

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in Reader submits a report for a selected review, the system SHALL save the report, associate it with that specific review and display a confirmation. |
| Source trace | UC:UC-14 |
| Depends on | FR-02-02; FR-04-01 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-09-FE` · FE · Screen: Report action on a review
- `FR-02-09-BE` · BE · API: save a report against a review

<a id="fr-02-10"></a>

### FR-02-10 Review and remove reported reviews

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff confirm the removal of a selected review from the reported-reviews list, the system SHALL remove that review from public display. |
| Source trace | UC:UC-13 |
| Depends on | FR-02-14 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-10-FE` · FE · Screen: Remove action with confirmation on a reported review
- `FR-02-10-BE` · BE · API: remove a reported review from public display

<a id="fr-02-11"></a>

### FR-02-11 Reject invalid review actions

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader submits a review text that fails the text check, or tries to edit or delete a review that is not their own, the system SHALL reject the action and show an error message. |
| Source trace | UC:UC-04; PCCV (activity diagram edge case) |
| Depends on | FR-02-01 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-11-FE` · FE · Error messages for rejected review actions
- `FR-02-11-BE` · BE · Reject failed text checks and edits or deletes of another reader's review

<a id="fr-02-12"></a>

### FR-02-12 Confirm review changes

| Field | Value |
|---|---|
| Criterion | WHEN a review is saved, replaced or removed, the system SHALL show a confirmation and the updated review list of that book. |
| Source trace | UC:UC-04; PCCV (activity diagram edge case) |
| Depends on | FR-02-01 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-12-FE` · FE · Confirmation and refreshed review list after save, edit or delete

<a id="fr-02-13"></a>

### FR-02-13 Hide removed reviews from the list

| Field | Value |
|---|---|
| Criterion | WHEN the system displays the reviews of a book, the system SHALL leave out every review that has been removed from public display. |
| Source trace | UC:UC-05; PCCV (activity diagram edge case) |
| Depends on | FR-02-02 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-13-BE` · BE · Filter out reviews removed from public display

<a id="fr-02-14"></a>

### FR-02-14 View the reported-reviews list

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff request the reported-reviews list, the system SHALL retrieve and display the reviews that have been reported. |
| Source trace | UC:UC-13; PCCV (activity diagram edge case) |
| Depends on | FR-02-09; FR-04-07 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-14-FE` · FE · Screen: staff list of reported reviews
- `FR-02-14-BE` · BE · API: list reported reviews

<a id="fr-02-15"></a>

### FR-02-15 End a review request with nothing to show

| Field | Value |
|---|---|
| Criterion | IF the requested book does not exist, THEN the system SHALL end the request without displaying a review list and SHALL display that there are no reviews to show. IF the book exists but has no published review, THEN the system SHALL display that the book has no reviews yet and SHALL invite the reader to write the first review. |
| Source trace | UC:UC-05; PCCV (activity diagram edge case) |
| Depends on | FR-02-02 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-15-FE` · FE · Empty state when the book is not found or has no reviews

<a id="fr-02-16"></a>

### FR-02-16 Handle a QR code linked to no book

| Field | Value |
|---|---|
| Criterion | IF a scanned QR code is not linked to any book in the catalogue, THEN the system SHALL display that the book cannot be found and SHALL not increase any scan count. |
| Source trace | UC:UC-06; PCCV (activity diagram edge case) |
| Depends on | FR-02-05 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-16-FE` · FE · Page: book cannot be found
- `FR-02-16-BE` · BE · Return not found for an unknown QR code without counting the scan

<a id="fr-02-17"></a>

### FR-02-17 Require at least one book for label printing

| Field | Value |
|---|---|
| Criterion | IF signed-in On-site Staff choose Print labels without selecting any physical book, THEN the system SHALL not produce a label sheet and SHALL ask them to select at least one physical book. |
| Source trace | UC:UC-10; PCCV (activity diagram edge case) |
| Depends on | FR-02-08 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-17-FE` · FE · Validation: select at least one physical book before printing

<a id="fr-02-18"></a>

### FR-02-18 Leave books without a QR code out of the label sheet

| Field | Value |
|---|---|
| Criterion | IF some selected physical books have no QR code yet, THEN the system SHALL leave them out of the label sheet and list them to the staff. IF none of the selected books has a QR code, THEN the system SHALL not produce a label sheet. |
| Source trace | UC:UC-10; PCCV (activity diagram edge case) |
| Depends on | FR-02-08 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-18-FE` · FE · List of books left out of the label sheet
- `FR-02-18-BE` · BE · Skip books without a QR code and return the list of skipped books

<a id="fr-02-19"></a>

### FR-02-19 Show an empty reported-reviews list

| Field | Value |
|---|---|
| Criterion | IF there are no reported reviews, THEN the system SHALL display that no reported reviews are waiting. |
| Source trace | UC:UC-13; PCCV (activity diagram edge case) |
| Depends on | FR-02-14 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-19-FE` · FE · Empty state: no reported reviews waiting

<a id="fr-02-20"></a>

### FR-02-20 Dismiss a report on a review that follows the rules

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff dismiss the report of a selected review that does not violate the rules, the system SHALL keep the review on public display and remove it from the reported-reviews list. |
| Source trace | UC:UC-13; PCCV (activity diagram edge case) |
| Depends on | FR-02-14 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-20-FE` · FE · Dismiss action on a reported review
- `FR-02-20-BE` · BE · API: close the report and keep the review public

<a id="fr-02-21"></a>

### FR-02-21 Reject a duplicate report

| Field | Value |
|---|---|
| Criterion | IF a Reader reports a review that they have already reported, THEN the system SHALL not save a second report and SHALL display that the review has already been reported. |
| Source trace | UC:UC-14; PCCV (activity diagram edge case) |
| Depends on | FR-02-09 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-21-FE` · FE · Message: review already reported
- `FR-02-21-BE` · BE · Reject a second report of the same review by the same reader

<a id="fr-02-22"></a>

### FR-02-22 Post a review under the reader's name or anonymously

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader submits or edits a review, the system SHALL let the reader choose to post it anonymously, and SHALL display the reader's full name as registered on the library card account, or "Bạn đọc ẩn danh" when the reader chose to post anonymously. |
| Source trace | UC:UC-04; UC:UC-06; Lesson 8 ui-conventions v0.6 (accepted by the team 19/11/2026) |
| Depends on | FR-02-01 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-02-22-FE` · FE · Checkbox "Đăng ẩn danh" on the review panel; show the reviewer name or "Bạn đọc ẩn danh" on each review
- `FR-02-22-BE` · BE · Store the anonymous choice per review; return the card full name or "Bạn đọc ẩn danh" as the display name

<a id="fr-02-23"></a>

### FR-02-23 List physical books awaiting a QR label

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff open QR label printing, the system SHALL list the physical books in the synced catalogue that have not yet had a QR label printed, 20 per page, ordered by floor, room and shelf code of each book's primary shelf location returned by the sync. |
| Source trace | UC:UC-10; Group decision 22/11/2026 (Chi) |
| Depends on | FR-02-07; FR-04-07 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-02-23-FE` · FE · Screen: list of physical books awaiting a QR label, 20 per page, ticks kept across pages, selected-books count
- `FR-02-23-BE` · BE · API: list physical books with no label printed yet, ordered by floor, room and shelf code of the primary shelf location from the sync, 20 per page

<a id="fr-02-24"></a>

### FR-02-24 Reject a report on the reader's own review

| Field | Value |
|---|---|
| Criterion | IF a signed-in Reader reports a review that they wrote, THEN the system SHALL not save the report and SHALL display that a reader cannot report their own review. |
| Source trace | UC:UC-14; Group decision 23/11/2026 (Chi) |
| Depends on | FR-02-09 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-02-24-FE` · FE · Message: a reader cannot report their own review
- `FR-02-24-BE` · BE · Rule: reject a report when the signed-in reader wrote the review

<a id="fr-02-25"></a>

### FR-02-25 Reprint QR labels for labelled books

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff select physical books that already have a printed label and choose Reprint labels («In lại nhãn»), the system SHALL produce a printable sheet with the existing QR code and the title of each selected book, without generating a new code and without a shelf location, and WHEN the staff confirm that the sheet was printed («Đã in xong»), the system SHALL write the audit entry and SHALL keep those books in the list of labelled books. |
| Source trace | UC:UC-10; Group decision 23/11/2026 (Chi) |
| Depends on | FR-02-08 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-02-25-FE` · FE · Screen: Chưa in nhãn / Đã in nhãn filter, «In lại nhãn» and reprint preview
- `FR-02-25-BE` · BE · API: list labelled books; produce a reprint sheet from the existing QR codes, no shelf location


## F-03 Discovery, Reading History & Recommendation

Readers filter books by access format (online, physical or both), keep a reading history and a saved-books list, and get AI chatbot search and recommendations based on their preferences. Use cases: UC-03, UC-07, UC-08, UC-09, UC-12.

<a id="fr-03-01"></a>

### FR-03-01 View reading history

| Field | Value |
|---|---|
| Criterion | WHEN an authenticated reader accesses their reading history, the system SHALL retrieve and display their reading history, including reading status, and display the updated history after a successful update. |
| Source trace | UC:UC-07; DFD L0: Reading history & preferences (ILF) |
| Depends on | FR-04-01; FR-03-03 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-01-FE` · FE · Screen: reading history list with status
- `FR-03-01-BE` · BE · API: list history entries of the signed-in reader

<a id="fr-03-02"></a>

### FR-03-02 Add a history entry when an online book is opened from this platform

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in library card reader selects an online book in the results of this platform to open it on the OPAC, the system SHALL add that book to the reading history of that reader. |
| Source trace | UC:UC-07; UC:UC-03 |
| Depends on | FR-03-12; FR-04-01 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-02-BE` · BE · Event hook: create a history entry when a signed-in library card reader selects an online book to open it on the OPAC

<a id="fr-03-03"></a>

### FR-03-03 Add history entries from borrowed physical books

| Field | Value |
|---|---|
| Criterion | WHEN a synced loan record of a library card account shows a borrowed book, the system SHALL add that book to the reading history of that reader. |
| Source trace | UC:UC-07; DFD L0: Reader loan records (EIF) |
| Depends on | FR-04-10 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-03-BE` · BE · Job: create history entries from synced loan records (library card accounts only)

<a id="fr-03-04"></a>

### FR-03-04 Mark reading status and progress

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader updates the reading status and progress of a book, the system SHALL check that the status is Reading or Finished and that the progress is between 0 and 100 percent, and SHALL save the updated information only if the check passes. |
| Source trace | UC:UC-07; DFD L0: Reading history & preferences (ILF) |
| Depends on | FR-03-01 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-04-FE` · FE · Screen: status selector and progress input
- `FR-03-04-BE` · BE · API: update status and progress of a history entry

<a id="fr-03-05"></a>

### FR-03-05 Set reading preferences

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader submits updated reading preferences, the system SHALL validate and save the preferences to that reader's profile and display the updated preferences. |
| Source trace | UC:UC-07 (preferences part); DFD L0: Reading history & preferences (ILF) |
| Depends on | FR-04-01 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-05-FE` · FE · Screen: reading preferences form
- `FR-03-05-BE` · BE · API: save reading preferences

<a id="fr-03-06"></a>

### FR-03-06 Save a physical book to a personal list

| Field | Value |
|---|---|
| Criterion | WHEN an authenticated reader selects a physical book to save, the system SHALL add that book to their saved books list. |
| Source trace | UC:UC-12; DFD L0: Saved books list (ILF) |
| Depends on | FR-01-01; FR-04-01 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-06-FE` · FE · Screen: Save button on the book detail page
- `FR-03-06-BE` · BE · API: add a book to the saved books list

<a id="fr-03-07"></a>

### FR-03-07 View saved books with shelf locations

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader opens the saved books list, the system SHALL display the saved books with the shelf location of each book. |
| Source trace | UC:UC-12; DFD L0: Saved books list (ILF), Book placement & library layout (EIF) |
| Depends on | FR-03-06; FR-01-01 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-07-FE` · FE · Screen: saved books list with shelf locations
- `FR-03-07-BE` · BE · API: list saved books joined with placement data

<a id="fr-03-08"></a>

### FR-03-08 Remove a saved book

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader selects Remove on a saved book, the system SHALL delete the book from that reader's saved books list and refresh and display the updated list. |
| Source trace | UC:UC-12 (extension: remove from list, team decision); DFD L0: Saved books list (ILF) |
| Depends on | FR-03-07 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-08-FE` · FE · Screen: Remove action on the saved books list
- `FR-03-08-BE` · BE · API: remove a book from the saved books list

<a id="fr-03-09"></a>

### FR-03-09 Search books by chatting with the AI chatbot

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader submits an inquiry message to the chatbot, the system SHALL forward the message and reader context to the AI service in the Library Core System, retrieve matching catalogue books, and display the conversational reply with book result cards. |
| Source trace | UC:UC-08; DFD L0: Chatbot conversations (ILF) |
| Depends on | FR-04-01; FR-04-09 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-09-FE` · FE · Screen: chat window with book result cards
- `FR-03-09-BE` · BE · API: handle chat message, query the catalogue, build the reply
- `FR-03-09-INT` · INT · Call the AI service inside the Library Core System with the reader message and context

<a id="fr-03-10"></a>

### FR-03-10 Save chatbot conversations per reader

| Field | Value |
|---|---|
| Criterion | WHEN the chatbot exchanges a message with a signed-in reader, the system SHALL persist both the reader message and the system reply in the conversation history of that reader. |
| Source trace | UC:UC-08; DFD L0: Chatbot conversations (ILF) |
| Depends on | FR-03-09 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-10-BE` · BE · Persist chat messages per reader

<a id="fr-03-11"></a>

### FR-03-11 Recommend books automatically

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader opens the recommendations section, the system SHALL aggregate the reader's reading history, declared preferences and chatbot conversations, compute recommendation scores, and display a list of personalized book recommendations. |
| Source trace | UC:UC-09 |
| Depends on | FR-03-01; FR-03-05; FR-03-10 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-11-FE` · FE · Screen: recommendation list
- `FR-03-11-BE` · BE · Recommendation logic using history, preferences and chat data

<a id="fr-03-12"></a>

### FR-03-12 Filter books by access format

| Field | Value |
|---|---|
| Criterion | WHEN a reader selects an access format (Online, Physical, or Both), the system SHALL filter and retrieve matching books and display the results with their corresponding access-format labels, 20 per page with page navigation. WHEN the reader selects another access format, the system SHALL return the results to page 1. |
| Source trace | UC:UC-03; W0 Table 3 (filter is added by this platform; OPAC advanced filter has no format option) |
| Depends on | FR-04-09 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-12-FE` · FE · Screen: access-format filter and results page (S-F03-01), linked from the OPAC catalogue and search results
- `FR-03-12-BE` · BE · API: query books by access format

<a id="fr-03-13"></a>

### FR-03-13 Log anonymous online-book reads

| Field | Value |
|---|---|
| Criterion | WHEN any reader selects an online book in the results of this platform to open it on the OPAC, the system SHALL record the book and the time of the selection without any reader identity. |
| Source trace | UC:UC-03; team decision: anonymous read log kept to train the AI features; W0 Table 4 (Online book read log, ILF) |
| Depends on | FR-03-12 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-13-BE` · BE · Event hook: store the book ID and time of each online book opened from the results, without reader identity

<a id="fr-03-14"></a>

### FR-03-14 View access formats of a book

| Field | Value |
|---|---|
| Criterion | WHEN a reader opens a book detail page, the system SHALL list the access formats of the book (Physical, Online PDF). |
| Source trace | UC:UC-03; DFD L0: Book catalogue (EIF) |
| Depends on | FR-04-09 |
| Priority | Won't (was Should, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-03-14-FE` · FE · Screen: access format list on the book detail page
- `FR-03-14-BE` · BE · API: include access formats in book responses

<a id="fr-03-15"></a>

### FR-03-15 Download the PDF of an online book

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in reader selects Download PDF on an online book, the system SHALL deliver the PDF file of that book. |
| Source trace | UC:UC-03; DFD L0: Book catalogue (PDF files, EIF) |
| Depends on | FR-04-01 |
| Priority | Won't (was Must, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-03-15-FE` · FE · Screen: Download PDF button with sign-in prompt
- `FR-03-15-BE` · BE · API: check reader session and stream the PDF file
- `FR-03-15-INT` · INT · Fetch the PDF file from the internal library system

<a id="fr-03-16"></a>

### FR-03-16 Reply when the chatbot finds no books

| Field | Value |
|---|---|
| Criterion | IF the AI service in the Library Core System returns no catalogue books matching the reader's inquiry, THEN the system SHALL display a conversational message explaining that no results were found and suggest alternative search terms or subjects. |
| Source trace | UC:UC-08; PCCV (activity diagram edge case) |
| Depends on | FR-03-09 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-16-BE` · BE · No-results reply with alternative search terms or subjects

<a id="fr-03-17"></a>

### FR-03-17 Handle an unavailable AI service

| Field | Value |
|---|---|
| Criterion | IF the AI service in the Library Core System is unresponsive, times out or returns an error, THEN the system SHALL display an error notice indicating that the AI search is temporarily unavailable and advise the reader to use the format filter. |
| Source trace | UC:UC-08; PCCV (activity diagram edge case) |
| Depends on | FR-03-09 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-17-FE` · FE · Notice: AI search temporarily unavailable, use the format filter
- `FR-03-17-BE` · BE · Timeout and error handling for AI Service calls

<a id="fr-03-18"></a>

### FR-03-18 Prompt sign-in before chatting

| Field | Value |
|---|---|
| Criterion | IF a reader attempts to send a chatbot message without a valid signed-in session, THEN the system SHALL deny the request and display a prompt to sign in with a library card. |
| Source trace | UC:UC-08; PCCV (activity diagram edge case) |
| Depends on | FR-03-09; FR-04-08 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-18-FE` · FE · Sign-in prompt on the chat screen, shown as the shared modal "Sign in to continue?" (M-F00-01)

<a id="fr-03-19"></a>

### FR-03-19 Recommend popular books when there is no reader data

| Field | Value |
|---|---|
| Criterion | IF a signed-in reader has no recorded reading history, preferences, or chatbot interactions, THEN the system SHALL display a fallback list of popular books based on QR scan counts and prompt the reader to configure reading preferences. |
| Source trace | UC:UC-09; PCCV (activity diagram edge case) |
| Depends on | FR-03-11; FR-02-06 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-19-FE` · FE · Prompt to set reading preferences
- `FR-03-19-BE` · BE · Fallback list of popular books by QR scan count

<a id="fr-03-20"></a>

### FR-03-20 Top up short recommendation lists

| Field | Value |
|---|---|
| Criterion | IF the recommendation calculation yields fewer than three matching titles, THEN the system SHALL supplement the list with trending books from the same subject categories. |
| Source trace | UC:UC-09; PCCV (activity diagram edge case) |
| Depends on | FR-03-11 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-20-BE` · BE · Add trending books from the same subject categories when fewer than three titles

<a id="fr-03-21"></a>

### FR-03-21 Prompt sign-in for recommendations

| Field | Value |
|---|---|
| Criterion | IF an unauthenticated visitor opens the recommendations section, THEN the system SHALL display a sign-in prompt explaining that personalized recommendations require a library card account. |
| Source trace | UC:UC-09; PCCV (activity diagram edge case) |
| Depends on | FR-03-11; FR-04-08 |
| Priority | Could |
| Hidden work | No |

Work items (L3):

- `FR-03-21-FE` · FE · Sign-in prompt on the recommendations screen, shown as the shared modal "Sign in to continue?" (M-F00-01)

<a id="fr-03-22"></a>

### FR-03-22 Reject invalid reading history or preference updates

| Field | Value |
|---|---|
| Criterion | IF a signed-in reader submits a reading status or progress that fails the check in FR-03-04, or reading preferences that fail the validation in FR-03-05, THEN the system SHALL reject the update, keep the saved data unchanged and display an error message. |
| Source trace | UC:UC-07; PCCV (activity diagram edge case) |
| Depends on | FR-03-04; FR-03-05 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-22-FE` · FE · Error message for rejected updates
- `FR-03-22-BE` · BE · Validate status, progress and preferences and reject invalid updates

<a id="fr-03-23"></a>

### FR-03-23 Show no results for an access-format filter

| Field | Value |
|---|---|
| Criterion | IF no books match the selected access format, THEN the system SHALL display that no books were found and allow the reader to choose another access format. |
| Source trace | UC:UC-03; PCCV (activity diagram edge case) |
| Depends on | FR-03-12 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-23-FE` · FE · Message: no books found, choose another format

<a id="fr-03-24"></a>

### FR-03-24 Reject saving a book twice

| Field | Value |
|---|---|
| Criterion | IF a signed-in reader saves a physical book that is already in their saved books list, THEN the system SHALL not add it again and SHALL display that the book is already saved. |
| Source trace | UC:UC-12; PCCV (activity diagram edge case) |
| Depends on | FR-03-06 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-24-FE` · FE · Message: book already saved
- `FR-03-24-BE` · BE · Reject a book already in the saved books list

<a id="fr-03-25"></a>

### FR-03-25 Show an empty saved books list

| Field | Value |
|---|---|
| Criterion | IF a signed-in reader opens the saved books list and the list is empty, THEN the system SHALL display that no books have been saved yet. |
| Source trace | UC:UC-12; PCCV (activity diagram edge case) |
| Depends on | FR-03-07 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-03-25-FE` · FE · Empty state: no books saved yet


## F-04 Platform, Access & Operations

Readers sign in (library card with email OTP), On-site Staff sign in with their internal library accounts to reach their minimal page, and the platform syncs data from the library's internal system, is deployed and keeps an audit log. Use cases: UC-11, UC-15.

<a id="fr-04-01"></a>

### FR-04-01 Sign in with library card and email OTP

| Field | Value |
|---|---|
| Criterion | WHEN a reader submits a library card number, the system SHALL look up the card in the Library Internal System reader accounts and, if the card is found, SHALL send an OTP to the email declared on that card. WHEN the reader submits an OTP that is correct, not expired and not used before, the system SHALL start a signed-in session for that reader and SHALL write an audit entry with the actor, the action and the time. IF the card number is not found, or the OTP is expired or already used, THEN the system SHALL reject the sign-in and display an error message. |
| Source trace | UC:UC-11; DFD L0: Reader accounts (EIF) |
| Depends on | FR-04-04 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-04-01-FE` · FE · Screen: card number and OTP entry, with error message
- `FR-04-01-BE` · BE · API: check card, request OTP, verify OTP, create session, reject with error when card not found or OTP wrong or expired
- `FR-04-01-INT` · INT · Look up the card number and declared email in the internal reader accounts

<a id="fr-04-02"></a>

### FR-04-02 Register or sign in with email OTP

| Field | Value |
|---|---|
| Criterion | WHEN a visitor submits an email address and the correct OTP, the system SHALL create an online account if none exists for that email and start a signed-in session. |
| Source trace | UC:UC-11; DFD L0: Online reader accounts (ILF) |
| Depends on | FR-04-04 |
| Priority | Won't (was Must, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-04-02-FE` · FE · Screen: email and OTP entry
- `FR-04-02-BE` · BE · API: create account if new, verify OTP, create session

<a id="fr-04-03"></a>

### FR-04-03 Sign in with Google

| Field | Value |
|---|---|
| Criterion | WHEN a visitor completes the Google sign-in, the system SHALL create an online account if none exists for that Google account and start a signed-in session. |
| Source trace | UC:UC-11; DFD L0: Online reader accounts (ILF) |
| Depends on | – |
| Priority | Won't (was Could, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-04-03-FE` · FE · Screen: Continue with Google button
- `FR-04-03-BE` · BE · API: verify Google token, create account if new, create session
- `FR-04-03-INT` · INT · Integrate Google sign-in (OAuth 2.0)

<a id="fr-04-04"></a>

### FR-04-04 Send and verify email OTP

| Field | Value |
|---|---|
| Criterion | WHEN the system sends an OTP for a library card that was found, the system SHALL email a one-time 6-digit code to the email declared on that card, and the code SHALL expire after 5 minutes and SHALL be usable only once. WHEN the reader requests a new OTP, the system SHALL invalidate the previous code and send a new one. |
| Source trace | UC:UC-11 |
| Depends on | – |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-04-04-BE` · BE · OTP generation, expiry, single use and new-OTP request
- `FR-04-04-INT` · INT · Integrate an email delivery service

<a id="fr-04-05"></a>

### FR-04-05 Link an online account to a library card

| Field | Value |
|---|---|
| Criterion | WHEN a signed-in online account reader submits a valid library card number and the correct OTP sent to the email declared on that card, the system SHALL attach the card number to the profile of that reader. |
| Source trace | UC:UC-11 (online part, cut in W4; W0 Table 3); DFD L0: Online reader accounts (ILF), Reader accounts (EIF) |
| Depends on | FR-04-02 |
| Priority | Won't (was Could, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-04-05-FE` · FE · Screen: link library card form with OTP entry
- `FR-04-05-BE` · BE · API: verify card OTP and attach card number to the profile

<a id="fr-04-06"></a>

### FR-04-06 Reject linking when both profiles hold data

| Field | Value |
|---|---|
| Criterion | IF the library card already belongs to a profile that holds data, THEN the system SHALL reject the link request and display a message that merging profiles is not supported. |
| Source trace | UC:UC-11 (online part, cut in W4); W0 Table 3 (merging two reader profiles is out of scope) |
| Depends on | FR-04-05 |
| Priority | Won't (was Could, see [Priority changes](#priority-changes-w4)) |
| Hidden work | No |

Work items (L3):

- `FR-04-06-BE` · BE · Check: reject the link when the card profile already holds data

<a id="fr-04-07"></a>

### FR-04-07 Sign in On-site Staff with internal library account

| Field | Value |
|---|---|
| Criterion | WHEN On-site Staff submit valid internal library account credentials, the system SHALL start a staff session and open the staff page. |
| Source trace | UC:UC-10; UC:UC-13; DFD L0: Staff accounts (EIF) |
| Depends on | – |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-04-07-FE` · FE · Screen: staff sign-in and staff page menu
- `FR-04-07-BE` · BE · API: staff sign-in and staff session
- `FR-04-07-INT` · INT · Verify staff credentials against the internal library accounts

<a id="fr-04-08"></a>

### FR-04-08 Enforce sign-in and staff access control

| Field | Value |
|---|---|
| Criterion | WHEN a request to a protected reader action or to the staff page has no valid session for the required role, the system SHALL deny the request. |
| Source trace | W0 Table 1 (Login required: UC-04, UC-07, UC-08, UC-09, UC-12, UC-14; Staff login: UC-10, UC-13) |
| Depends on | FR-04-01; FR-04-07 |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-04-08-BE` · BE · Session validation and role check (RBAC) middleware on protected endpoints

<a id="fr-04-09"></a>

### FR-04-09 Sync catalogue, shelf placement and library layout

| Field | Value |
|---|---|
| Criterion | WHEN the daily sync time is reached, the system SHALL import the catalogue, the shelf codes, and the floors and rooms from the internal library system without writing back to it. |
| Source trace | UC:UC-15; DFD L0: Book catalogue (EIF), Book placement & library layout (EIF) |
| Depends on | – |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-04-09-INT` · INT · Scheduled import of catalogue, shelf codes, floors and rooms from the internal system

<a id="fr-04-10"></a>

### FR-04-10 Sync loan records

| Field | Value |
|---|---|
| Criterion | WHEN the daily sync time is reached, the system SHALL import the loan records of library card accounts from the internal library system without writing back to it. |
| Source trace | UC:UC-15; DFD L0: Reader loan records (EIF) |
| Depends on | – |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-04-10-INT` · INT · Scheduled import of loan records from the internal system

<a id="fr-04-11"></a>

### FR-04-11 Handle sync failures

| Field | Value |
|---|---|
| Criterion | IF a sync run fails, THEN the system SHALL keep the last successful data, retry up to 3 times and write the error to the audit log. |
| Source trace | UC:UC-15; Derived: FR-04-09 and FR-04-10 |
| Depends on | FR-04-09; FR-04-10 |
| Priority | Should |
| Hidden work | Yes |

Work items (L3):

- `FR-04-11-BE` · BE · Retry policy and last-good-data fallback for sync jobs

<a id="fr-04-12"></a>

### FR-04-12 Keep an audit log

| Field | Value |
|---|---|
| Criterion | WHEN a sign-in, a label print, a review removal or a sync run happens, the system SHALL write an audit entry with the actor, the action and the time. |
| Source trace | Derived: F-04 scope (audit log) |
| Depends on | – |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-04-12-BE` · BE · Audit logging service and storage

<a id="fr-04-13"></a>

### FR-04-13 Deploy automatically

| Field | Value |
|---|---|
| Criterion | WHEN a change is merged to the main branch and the automated tests pass, the system SHALL build it and deploy it to the hosting environment. |
| Source trace | Derived: F-04 scope (deployment) |
| Depends on | FR-04-14 |
| Priority | Must |
| Hidden work | Yes |

Work items (L3):

- `FR-04-13-BE` · BE · CI/CD pipeline and environments (staging, production)

<a id="fr-04-14"></a>

### FR-04-14 Run automated tests on every change

| Field | Value |
|---|---|
| Criterion | WHEN a change is pushed to the repository, the system SHALL run the automated unit and integration tests and report the result. |
| Source trace | Derived: F-04 scope (deployment); hidden technical work |
| Depends on | – |
| Priority | Must (was Should, see [Priority changes](#priority-changes-w4)) |
| Hidden work | Yes |

Work items (L3):

- `FR-04-14-BE` · BE · Automated test suite for core flows and pipeline test stage

<a id="fr-04-15"></a>

### FR-04-15 Monitor errors and availability

| Field | Value |
|---|---|
| Criterion | WHEN the system raises an unhandled error or a health check fails, the system SHALL record the error with its context and notify the project team. |
| Source trace | Derived: F-04 scope (operations); hidden technical work |
| Depends on | – |
| Priority | Won't (was Should, see [Priority changes](#priority-changes-w4)) |
| Hidden work | Yes |

Work items (L3):

- `FR-04-15-BE` · BE · Error tracking, health check and alert to the project team

<a id="fr-04-16"></a>

### FR-04-16 Handle a failed OTP email

| Field | Value |
|---|---|
| Criterion | IF the OTP email cannot be sent to the email declared on the card, THEN the system SHALL display that the code could not be sent and SHALL allow the reader to request a new OTP. |
| Source trace | UC:UC-11; PCCV (activity diagram edge case) |
| Depends on | FR-04-04 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-04-16-FE` · FE · Message: code could not be sent, request a new OTP
- `FR-04-16-BE` · BE · Detect OTP email send failure

<a id="fr-04-17"></a>

### FR-04-17 Limit incorrect OTP attempts

| Field | Value |
|---|---|
| Criterion | IF a reader submits an incorrect OTP, THEN the system SHALL display that the code is incorrect and allow the reader to enter it again. IF 5 incorrect attempts are made for the same OTP, THEN the system SHALL invalidate that OTP and reject the sign-in. |
| Source trace | UC:UC-11; PCCV (activity diagram edge case) |
| Depends on | FR-04-04 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-04-17-FE` · FE · Message: incorrect code, enter it again
- `FR-04-17-BE` · BE · Count incorrect OTP attempts and invalidate the OTP after 5

<a id="fr-04-18"></a>

### FR-04-18 Reject invalid staff sign-in

| Field | Value |
|---|---|
| Criterion | IF On-site Staff submit credentials that the internal library accounts do not accept, or an account without the On-site Staff role, THEN the system SHALL reject the sign-in, display an error message, and allow the staff to try again. |
| Source trace | UC:UC-10; UC:UC-13; PCCV (activity diagram edge case) |
| Depends on | FR-04-07 |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-04-18-FE` · FE · Message on the staff sign-in: sign-in rejected (wrong account or no staff role), try again
- `FR-04-18-BE` · BE · Reject credentials the internal library accounts do not accept, or an account without the staff role

<a id="fr-04-19"></a>

### FR-04-19 Show the remaining OTP attempts

| Field | Value |
|---|---|
| Criterion | IF a reader submits an incorrect OTP and fewer than 5 incorrect attempts have been made for that OTP, THEN the system SHALL display the number of attempts left. |
| Source trace | UC:UC-11; Lesson 8 ui-conventions v0.6 (accepted by the team 19/11/2026) |
| Depends on | FR-04-17 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-04-19-FE` · FE · Message: incorrect code with the number of attempts left
- `FR-04-19-BE` · BE · Return the number of attempts left with the incorrect-OTP response

<a id="fr-04-20"></a>

### FR-04-20 Handle a network or loading error

| Field | Value |
|---|---|
| Criterion | IF a screen cannot load or save its data because of a network or server error, THEN the system SHALL keep the data already shown, display an error message that the page could not load, and SHALL allow the user to try again. |
| Source trace | All screens; Lesson 8 ui-conventions v0.6, MSG-04 (accepted by the team 19/11/2026) |
| Depends on | – |
| Priority | Must |
| Hidden work | No |

Work items (L3):

- `FR-04-20-FE` · FE · Banner error (MSG-04) with Try again on every screen, keeping the data already shown
- `FR-04-20-BE` · BE · Standard error response for load and save failures on every API

<a id="fr-04-21"></a>

### FR-04-21 Sign out of the staff page

| Field | Value |
|---|---|
| Criterion | WHEN signed-in On-site Staff choose Sign out, the system SHALL end the staff session and SHALL open the staff sign-in screen. The system SHALL keep the staff session valid until the staff member signs out (no time-out). |
| Source trace | UC:UC-10; UC:UC-13; Group decision 22/11/2026 (Chi) |
| Depends on | FR-04-07 |
| Priority | Should |
| Hidden work | No |

Work items (L3):

- `FR-04-21-FE` · FE · Button "Đăng xuất" in the header of the staff page, QR label printing and reported reviews; open the staff sign-in after sign-out
- `FR-04-21-BE` · BE · API: end the staff session; staff session stays valid with no time-out


## Priority rules (W4)

Every priority change names the rule it followed. Cut scope by lowering priority, never by lowering effort.

| Rule | Meaning | Test question | Usual Kano category |
|---|---|---|---|
| R1 · Must | The release has no viable use without it | If it is absent on delivery day, is the release unusable? | Must-be — invisible when present, fatal when absent |
| R2 · Should | Important, but a workaround exists | Painful to leave out, yet the solution still works? | One-dimensional — more of it, more satisfaction |
| R3 · Could | Desirable, low impact if dropped | Would anyone notice within the first month? | Attractive — a delighter, never a Must |
| R4 · Won't | Agreed as out of scope for this release | Did the client accept deferring it, and is it in W0 Table 3? | Indifferent — asked for, but nobody actually cares |

## Priority changes (W4)

| FR | Name | Initial | Rule | Kano | Effective | Justification |
|---|---|---|---|---|---|---|
| [FR-01-03](#fr-01-03) | Show a book's room on the map | Should | R3 Could | Attractive | Could | Workaround exists: readers still see floor, room and shelf code (FR-01-01) and can browse the map (FR-01-02); the deep link from a book to its highlighted room is a convenience. Nobody would miss it in the first month. |
| [FR-02-06](#fr-02-06) | Count QR code scans | Should | R3 Could | Attractive | Could | No reader-facing impact: scan counts only feed analysis and AI training, and the AI features are already Could. Dropping it does not block QR access (FR-02-05) or label printing (FR-02-08). |
| [FR-03-14](#fr-03-14) | View access formats of a book | Should | R4 Won't | Indifferent | Won't | Not rebuilt: for physical books the current OPAC already shows copies and shelf location, and for online books it already shows a download button. Readers still filter by format (FR-03-12). |
| [FR-03-15](#fr-03-15) | Download the PDF of an online book | Must | R4 Won't | Indifferent | Won't | Not rebuilt: the current OPAC already has the PDF download function for online books. No PDF delivery, session check or PDF fetch from the internal system is built on this platform. |
| [FR-04-02](#fr-04-02) | Register or sign in with email OTP | Must | R4 Won't | Indifferent | Won't | No online reader accounts in release 1: only library card holders sign in (FR-04-01), and online books need no account. |
| [FR-04-03](#fr-04-03) | Sign in with Google | Could | R4 Won't | Indifferent | Won't | Follows the removal of online accounts: Google sign-in only created online accounts. |
| [FR-04-05](#fr-04-05) | Link an online account to a library card | Could | R4 Won't | Indifferent | Won't | Nothing to link once online accounts are removed. |
| [FR-04-06](#fr-04-06) | Reject linking when both profiles hold data | Could | R4 Won't | Indifferent | Won't | Only checked the link in FR-04-05, which is removed. |
| [FR-04-14](#fr-04-14) | Run automated tests on every change | Should | R1 Must | Must-be | Must | Raised because FR-04-13 (Must) deploys only when the automated tests pass: without these tests the Must deployment cannot work. Effort unchanged; decided by Chi 23/11/2026 (D50). |
| [FR-04-15](#fr-04-15) | Monitor errors and availability | Should | R4 Won't | Indifferent | Won't | Deferred to fit team capacity: error tracking, health check and alerts are done by hand in release 1. Revisit if the client asks for uptime reporting. |

## Open questions (W5 §4)

| # | Question | Blocking? | Feature | Default applied |
|---|---|---|---|---|
| 1 | Resolved 23/11/2026 (D42): the platform records the event when a reader selects an online book in its own results («Mở trên OPAC»); what the reader then reads or downloads on the existing OPAC is not seen. | No | F-03 | FR-03-02 and FR-03-13 record the selection, not the download (D42) |
| 2 | Resolved 23/11/2026 (D47): the internal library system holds the access format (online, physical or both) of every book. | No | F-03 | FR-03-12 filters on the synced access format (D47) |
| 3 | Resolved 23/11/2026 (D47): library staff tell the team when a room is added, renamed or removed. | No | F-01 | Library staff report room changes; FR-01-05 checks the codes after each sync (D47) |
| 4 | Resolved 23/11/2026 (D47): library staff watch errors and availability after release; no uptime report is needed in release 1. | No | F-04 | Library staff check the system by hand in release 1 (D47) |
| 5 | [NEEDS CLARIFICATION: does the anonymous read log (FR-03-13) need a privacy notice or a retention period?] | No | F-03 | Assuming only the book ID and the time are stored, with no reader identity |
| 6 | Resolved 23/11/2026 (D43): the 360 h team capacity covers Must + Should; the Could pool is optional. | No | All | Must + Should = 345.6 h, within 360 h (D43) |
