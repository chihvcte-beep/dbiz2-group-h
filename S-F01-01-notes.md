# Wireframe notes: S-F01-01 Shelf location (with Save to my list)

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | “Vị trí kệ sách” | — |
| 2 | Book title | [NEEDS CLARIFICATION: no standalone book-title component is listed in UI Conventions section 3] | Book catalogue › title; sample: “Principles of Economics” | FR-01-01 |
| 3 | Shelf location line | Shelf location line | Book placement & library layout › floor, room code, shelf code; one line per physical copy: “Tầng 2 · Phòng R-204 · Kệ S-12” | FR-01-01 |
| 4 | Unavailable shelf location | Banner | MSG-06: “Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé.” | FR-01-07 |
| 5 | Online-only information | Banner | “Sách này chỉ có bản trực tuyến, không có vị trí trên kệ.” | FR-01-06 |
| 6 | Save to my list | Primary button | “Lưu vào danh sách”; physical books only | FR-03-06 |
| 7 | View on map | Secondary button | “Xem trên bản đồ”; show only when a physical copy has a room location | FR-01-03 |
| 8 | Save confirmation | Toast | “Đã lưu sách vào danh sách của bạn.” [NEEDS CLARIFICATION: exact success wording is not listed in shared messages] | FR-03-06 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F01-01-default.png, img/S-F01-01-numbered.png | Book title, one shelf-location line per physical copy, Save and View on map actions | FR-01-01, FR-03-06, FR-01-03 |
| Empty | Not applicable: this is a single-book location view, not a list | — | — |
| Loading | img/S-F01-01-loading.png | Skeleton blocks matching the title, location and action areas; no loading text | FR-01-01 |
| Error | img/S-F01-01-error.png | MSG-06 banner; the book title remains visible | FR-01-07 |
| Success — saved | img/S-F01-01-success.png | “Book saved” confirmation shown as a Toast; temporary Vietnamese wording is used pending confirmation | FR-03-06 |
| Success — already saved | Same layout as Success — saved; wording variant: “Sách này đã có trong danh sách của bạn.” | The book is already in the reader’s saved list | FR-03-24 |
| Information — online only | img/S-F01-01-online-only.png | Online-only information; no shelf location, Save or View on map actions | FR-01-06 |

## Actions and where they go

| Element | User action | Goes to |
|---|---|---|
| Back | Tap | Existing OPAC Book Detail (exit) |
| View on map | Tap | S-F01-02 |
| Save to my list | Tap while signed in | stays |
| Save to my list | Tap while not signed in | M-F00-01 |

## Open questions

| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: no standalone book-title component is named in UI Conventions section 3.] | Show the title as a heading, without inventing a new control. |
| 2 | [NEEDS CLARIFICATION: exact success Toast wording for saving is not listed in shared messages.] | Temporary wording is shown; confirm with Linh. |

Notes:
- Save is available for physical books only. Do not show a Save action for an online-only book.
- Do not add a link from this screen to the saved-books list.
- Do not show shelf availability or a list of borrowable copies; these are outside the release scope.
- If shelf details are missing or do not match the library layout, show the shared MSG-06 wording.
- The map action is available only when the physical copy has a usable room location.
