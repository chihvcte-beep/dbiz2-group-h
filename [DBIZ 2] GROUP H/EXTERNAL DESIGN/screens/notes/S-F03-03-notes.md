# Wireframe notes: S-F03-03 Saved Books List

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title and back navigation | Screen header | Sách đã lưu; back to the previous OPAC page. | FR-03-07 |
| 2 | Saved book entry | Book row | Book cover placeholder, title and author for each saved physical book. Data comes from the Reader's saved-books list. | FR-03-07 |
| 3 | Access-format label | Format label | Bản giấy. UC-12 saves physical books only. | FR-03-06, FR-03-07 |
| 4 | Shelf location | Location text | Synced floor, room code and shelf code for the saved book. | FR-03-07 |
| 5 | Unavailable shelf location | Inline error banner | “Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé.” Shown when the location is missing or inconsistent. | FR-01-07 |
| 6 | Remove saved book | Secondary button | Bỏ khỏi danh sách. Removes the selected book and refreshes the list. | FR-03-08 |
| 7 | Empty-list message | Empty state | “Chưa có sách nào được lưu.” | FR-03-25 |
| 8 | Load error | Banner | MSG-04 — “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” | FR-04-20* |
| 9 | Try again | Secondary button | Thử lại. Retries loading the saved-books list. | FR-04-20* |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/S-F03-03.png, img/S-F03-03-numbered.png | Saved physical books with format labels, synced shelf locations and Remove actions. One row demonstrates an unavailable shelf location. | FR-03-06, FR-03-07, FR-01-07, FR-03-08 |
| Empty | img/S-F03-03-empty.png, img/S-F03-03-empty-numbered.png | “Chưa có sách nào được lưu.” | FR-03-25 |
| Loading | img/S-F03-03-loading.png, img/S-F03-03-loading-numbered.png | Skeleton while saved books and shelf locations are being retrieved. | FR-03-07 |
| Error | img/S-F03-03-error.png, img/S-F03-03-error-numbered.png | MSG-04 with a Try again action after the list fails to load. | FR-04-20* |
| Success | img/S-F03-03-success.png, img/S-F03-03-success-numbered.png | The selected book has been removed and the saved-books list is refreshed. | FR-03-08 |
| Location unavailable | img/S-F03-03.png, img/S-F03-03-numbered.png | The affected book row shows that its shelf location is unavailable and directs the Reader to the information desk. Other saved books remain visible. | FR-01-07 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Saved books link on the existing OPAC personal area | Open the saved-books list after a valid Reader sign-in. | S-F03-03; if the Reader is not signed in, use the shared sign-in flow S-F00-01. |
| Back navigation | Return to the previous OPAC page. | Previous page |
| Remove saved book | Delete the selected book from the Reader's saved-books list. No confirmation modal is specified in AD-UC-12. | S-F03-03 with the refreshed list; if no books remain, show Empty. |
| Try again | Retry retrieving the saved-books list after a load failure. | Stays on S-F03-03 |
| Save a physical book | Save is selected from the existing OPAC book detail / catalogue display; check for duplicates before adding. | Existing OPAC book display; the saved entry is then available in S-F03-03. |

## Open questions

Review status: checked against the UC-12 Screen List and Usage Flow. Final consistency review is pending.

| # | Question | Default drawn |
| --- | --- | --- |
| 1 | [NEEDS CLARIFICATION: Is MSG-04 / FR-04-20 the approved network-error treatment for this Reader screen?] | Show the network-error banner and Try again action as drawn. |
| 2 | [NEEDS CLARIFICATION: Confirm the exact Vietnamese wording for the empty-list message.] | “Chưa có sách nào được lưu.” |
| 3 | [NEEDS CLARIFICATION: Confirm the sample book titles, authors and shelf codes against the synced catalogue.] | Sample catalogue data and shelf codes are illustrative placeholders. |
| 4 | [NEEDS CLARIFICATION: Confirm whether the information-desk direction should name a specific location/contact.] | Direct the Reader to the information desk on the ground floor. |

* FR-04-20 is shown in the current wireframe for MSG-04 and Retry. The UC-12 Screen List / Usage Flow explicitly confirms the empty-list, unavailable-location and removal outcomes, but does not independently specify a generic network-error state for S-F03-03. Confirm this mapping before treating it as a final requirement.
