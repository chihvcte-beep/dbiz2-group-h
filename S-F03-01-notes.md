# Wireframe notes: S-F03-01 Book Catalogue & Access Format Filter

Actor: Reader · Feature: F-03 Discovery, Reading History & Recommendation · Use case: UC-03 · Activity diagram: AD-UC-03 v1.2

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back navigation | Existing OPAC navigation | Returns to the existing OPAC catalogue / search results from which the reader opened the filter. | — |
| 2 | Screen title | Screen header | “Lọc theo hình thức” [wireframe label; confirm the final approved Vietnamese title] | — |
| 3 | Access-format selector | Segmented control | Exactly three choices: “Trực tuyến” (Online), “Bản giấy” (Physical), and “Cả hai” (Both). “Both” means books that have both a physical copy and an online version. | FR-03-12 |
| 4 | Matching book results | Book result row / list | Retrieve matching books from the whole synced catalogue, not only the current search results. Each result displays its access-format label: “Online”, “Physical”, or the applicable label for the Both filter. | FR-03-12 |
| 5 | No-results message | Empty state | Tell the reader that no books were found and invite them to choose another access format. Exact approved message wording is not specified in AD-UC-03. | FR-03-23 |
| 6 | Online-book link | Result-row action / link | Opens the selected online book on the current OPAC. This project does not build an online-book viewer or download function. | FR-03-13 |
| 7 | Anonymous online-read log | Background system action; not a visible UI element | When an online book is opened, record the book and time without any reader identity. | FR-03-13 |
| 8 | Signed-in reader history update | Background system action; not a visible UI element | Check whether the reader is signed in with a library card. If yes, add the book to their reading history; if not, do not create a history entry. | FR-03-02 |

## States drawn

| State | Image | What the user sees | Source / FR |
|---|---|---|---|
| Default | img/S-F03-01-default.png, img/S-F03-01-numbered.png | Access-format filter area with the three choices. The initial selected option is not specified in AD-UC-03; confirm whether the control should start with no selection or a default selection before final handoff. | UC-03 · FR-03-12 |
| Empty | img/S-F03-01-empty.png | No matching books are found. The message invites the reader to choose another format; the filter remains available on this same screen. | AD-UC-03 d1 [No], s3 · FR-03-23 |
| Loading | img/S-F03-01-loading.png | Loading presentation while the system retrieves books for the selected access format. This is a conventional UI state; AD-UC-03 does not define exact loading copy or a separate loading interaction. | System step s1 · FR-03-12 |
| Error | img/S-F03-01-error.png | [NOT SPECIFIED IN AD-UC-03] The activity diagram defines the no-matching-books alternative, not a network/system-error message. Do not treat an error banner or MSG-04 as a UC-03 requirement unless confirmed in the approved shared message catalogue / screen spec. | Needs confirmation |
| Results / Success | img/S-F03-01-success.png, if retained in the export | Matching books are displayed with their access-format labels. The result list stays on S-F03-01 while the reader chooses another format or finishes filtering. “Success” is the matching-results outcome, not a separate confirmation Toast. | AD-UC-03 d1 [Yes], s2 · FR-03-12 |

## Actions and where they go

| Element / event | User action / system event | Result / destination |
|---|---|---|
| Entry | Reader opens the access-format filter from the existing OPAC catalogue / search results | S-F03-01 |
| Access-format selector | Reader chooses Online, Physical or Both | System retrieves matching books from the whole synced catalogue; results update on S-F03-01 |
| No-results state | No matching books are found | Display the no-results message on S-F03-01; reader can choose another format |
| Choose another format | Reader selects a different format after seeing no results or a result list | Return to the format-selection step on S-F03-01; retrieve and display the new matching results |
| Online book result | Reader opens an online book | Hand off to that book on the current OPAC (existing destination; no new viewer/download screen is built here) |
| Online book opened | System records the book and time without reader identity | Background action s4 · FR-03-13 |
| Library-card sign-in check | System checks whether the reader is signed in with a library card | If Yes, add the book to reading history (s5 · FR-03-02); if No, do not add a history entry |
| Finish | Reader stops filtering | Activity ends; the current result list remains on S-F03-01 |

## Open questions

| # | Question | Current treatment |
|---|---|---|
| 1 | What is the initial state of the three-option selector when S-F03-01 first opens? | Not defined in AD-UC-03. The current Default wireframe must be checked with the team; do not infer a default selection from the use case. |
| 2 | What is the exact Vietnamese wording for the no-results message? | AD-UC-03 only says to display that no books were found and allow another format choice. Use approved shared copy if available; otherwise mark the wireframe text as provisional. |
| 3 | Is there an approved system/network error message for this screen? | No UC-03 system-error branch is specified in AD-UC-03. The Error state in the visual export is a design placeholder, not a confirmed FR. |
| 4 | Confirm the final Vietnamese screen title and exact result-row layout. | The activity diagram specifies the behaviour and access-format labels, but does not define detailed visual copy or row anatomy. |

## Scope and implementation notes

- Login is not required to use the access-format filter.
- The catalogue and each book's access format must already be synced (FR-04-09 precondition in AD-UC-03).
- The three choices are exactly Online, Physical and Both (FR-03-12).
- “Both” means a book has both a physical copy and an online version; the filter applies to the whole synced catalogue.
- The empty-result outcome does not end the activity. The reader can choose another format on the same screen (FR-03-23).
- Opening an online book hands the reader over to the current OPAC. This platform does not build an online viewer or download function (W0 Table 3; FR-03-14 and FR-03-15 are out of scope).
- Every online-book opening creates an anonymous read-log record containing the book and time only (FR-03-13).
- Only a reader signed in with a library card receives a reading-history entry (FR-03-02). This is background processing, not another screen.
- No modal is specified for UC-03.
- The Advanced Filter Panel is an area within Search Results, not a separate screen.
