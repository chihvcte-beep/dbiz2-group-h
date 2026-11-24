# Wireframe notes: S-F03-03 Saved books list

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Screen title and back navigation | Screen header | “Sách đã lưu”. Back returns to the existing OPAC personal area. | — |
| 2 | Saved book entry | Book row | Book cover placeholder, title and author for each saved physical book. Data comes from the reader’s saved-books list. | FR-03-07 |
| 3 | Access-format label | Format label | “Bản giấy”. UC-12 saves physical books only. Show an icon with the label; do not rely on colour alone. | FR-03-06, FR-03-07 |
| 4 | Shelf location | Shelf location line | Show the synced location in the format “Tầng n · Phòng code · Kệ code”, with a location-pin icon. Keep the full shelf code on one line where possible. | FR-03-07 |
| 5 | Unavailable shelf location | Banner | Use MSG-06 exactly: “Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé.” Show it only for the affected book; other saved books remain visible. | FR-01-07 |
| 6 | Remove saved book | Secondary button | “Bỏ khỏi danh sách”. Remove the selected book and refresh the list. No confirmation modal is specified. | FR-03-08 |
| 7 | Empty-list message | Empty state | “Bạn chưa lưu sách nào. Bấm Lưu vào danh sách ở trang vị trí kệ sách.” | FR-03-25 |
| 8 | Load error | Banner | MSG-04: “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” Keep data already shown. | FR-04-20 |
| 9 | Retry action | Secondary button | “Thử lại”. Retry retrieving the saved-books list. | FR-04-20 |
| 10 | Removal success feedback | Toast | Short success feedback after removal: “Đã bỏ sách khỏi danh sách.” The list is refreshed underneath. | FR-03-08 |

## States drawn

| State | Image | What the user sees | Source / FR |
|---|---|---|---|
| Default | [s-f03-03.png](../img/s-f03-03/s-f03-03.png) | Saved physical books with format labels, synced shelf locations and “Bỏ khỏi danh sách” actions. One row demonstrates an unavailable shelf location. | FR-03-06, FR-03-07, FR-01-07, FR-03-08 |
| Empty | [s-f03-03-empty.png](../img/s-f03-03/s-f03-03-empty.png) | “Bạn chưa lưu sách nào. Bấm Lưu vào danh sách ở trang vị trí kệ sách.” | FR-03-25; UI Conventions §4 |
| Loading | [s-f03-03-loading.png](../img/s-f03-03/s-f03-03-loading.png) | Skeleton placeholders while saved books and shelf locations are retrieved. | FR-03-07; MSG-05 |
| Error | [s-f03-03-error.png](../img/s-f03-03/s-f03-03-error.png) | Shared MSG-04 banner and “Thử lại” action. Retain any data already shown. | FR-04-20 |
| Success | [s-f03-03-success.png](../img/s-f03-03/s-f03-03-success.png) | The selected book has been removed, the list is refreshed, and a short success Toast appears. | FR-03-08 |
| Location unavailable | [s-f03-03-error-2.png](../img/s-f03-03/s-f03-03-error-2.png) | The affected row shows the exact MSG-06 wording; other saved books remain visible. | FR-01-07; MSG-06 |

## Actions and where they go

| Element / event | User action | Result / destination |
|---|---|---|
| Saved books link on the existing OPAC personal area | Reader opens the saved-books list. | If signed in, open S-F03-03. If not signed in, open M-F00-01; choosing “Đăng nhập” continues through S-F00-01. |
| Back navigation | Reader taps Back. | Existing OPAC personal area (exit destination). |
| Remove saved book | Reader taps “Bỏ khỏi danh sách”. | Delete the selected saved entry and refresh S-F03-03. If no books remain, show Empty. No confirmation modal. |
| Retry | Reader taps “Thử lại” after a load error. | Retry retrieving the saved-books list; stay on S-F03-03. |
| Save a physical book | Reader saves a physical book from the existing OPAC book display / S-F01-01 flow. | This action is outside S-F03-03; the saved entry becomes available in this list. |

## Open questions

None. Decisions: see [decision-index.md](../../../project/decision-index.md#s-f03-03).
