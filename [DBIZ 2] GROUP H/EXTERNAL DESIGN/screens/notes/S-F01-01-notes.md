# Wireframe notes: S-F01-01 Shelf location

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back button and screen title | Screen header | “Vị trí kệ sách”; Back returns to the existing OPAC Book Detail page. | — |
| 2 | Book title and author | Section title | Book catalogue › title and author. Sample: “Principles of Economics” — “N. Gregory Mankiw”. | FR-01-01 |
| 3 | Shelf location line | Shelf location line | Book placement & library layout › floor, room code and shelf code. Show one line for each physical copy, e.g. “Tầng 2 · Phòng R-204 · Kệ S-12”. Include the map-pin icon. | FR-01-01 |
| 4 | Unavailable shelf location | Banner | MSG-06: “Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé.” | FR-01-07 |
| 5 | Online-only information | Banner | “Sách này chỉ có bản trực tuyến, không có vị trí trên kệ.” | FR-01-06 |
| 6 | Save to my list | Primary button | “Lưu vào danh sách”. Show only for physical books. One Primary button is visible at a time. | FR-03-06 |
| 7 | View on map | Secondary button | “Xem trên bản đồ”. Show only when a physical copy has a usable room location. | FR-01-03 |
| 8 | Save confirmation | Toast | “Đã lưu sách vào danh sách của bạn.” Shown after a successful save. | FR-03-06 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F01-01-numbered.png | Book title and author; one shelf-location line per physical copy; Save and View on map actions. The numbered image identifies the elements. | FR-01-01, FR-03-06, FR-01-03 |
| Empty | Not applicable: this is a single-book location view, not a list. | No empty-list state is shown. | — |
| Loading | img/S-F01-01-states.png | Skeleton placeholders matching the title, location and action areas; no loading text. | FR-01-01 |
| Error — shelf location unavailable | img/S-F01-01-states.png | MSG-06 is shown while the book title remains visible. View on map is hidden when no usable room location exists. | FR-01-07 |
| Error — network/load failure | img/S-F01-01-states.png | MSG-04: “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” with “Thử lại”. Keep data already shown. | FR-04-20 |
| Success — saved | img/S-F01-01-states.png | A Toast confirms: “Đã lưu sách vào danh sách của bạn.” | FR-03-06 |
| Success — already saved | img/S-F01-01-states.png | Informational Toast: “Sách này đã có trong danh sách của bạn.” | FR-03-24 |
| Information — online only | img/S-F01-01-states.png | “Sách này chỉ có bản trực tuyến, không có vị trí trên kệ.” No shelf location, Save or View on map actions. | FR-01-06 |

## Actions and where they go

| Element | User action | Goes to |
|---|---|---|
| Back | Tap | Existing OPAC Book Detail (exit) |
| View on map | Tap | S-F01-02 |
| Save to my list | Tap while signed in | Stays on S-F01-01; show the save confirmation Toast. |
| Save to my list | Tap while not signed in | M-F00-01 |
| Save to my list | Tap when the book is already saved | Stays on S-F01-01; show the already-saved informational Toast. |

## Open questions

| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: confirm whether the success Toast wording “Đã lưu sách vào danh sách của bạn.” is approved for FR-03-06.] | Use the wording shown in the wireframe until the shared message catalogue confirms the final copy. |
| 2 | [NEEDS CLARIFICATION: confirm whether the already-saved message should be displayed as a Toast or another informational treatment.] | Use a short informational Toast for FR-03-24, consistent with the success feedback pattern. |
| 3 | [NEEDS CLARIFICATION: confirm whether multiple physical copies should be grouped by copy/holding or displayed as separate shelf-location lines.] | Display one shelf-location line per physical copy, as specified in AD-UC-01 question 1. |

