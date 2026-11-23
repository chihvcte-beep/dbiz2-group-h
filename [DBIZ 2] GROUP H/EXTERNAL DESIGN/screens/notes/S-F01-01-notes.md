# Wireframe notes: S-F01-01 Shelf location 

Actor: Reader · Frame: 360px (exported at 3x / 1080px) · UI conventions: v0.8 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | “Vị trí kệ sách”. Back returns to the existing OPAC Book Detail page. | — |
| 2 | Book title | Section title | Book catalogue › title; sample: “Principles of Economics”. | FR-01-01 |
| 3 | Author | Text | Book catalogue › author; sample: “N. Gregory Mankiw”. | FR-01-01 |
| 4 | Shelf location line — copy 1 | Shelf location line | Book placement & library layout › floor, room code and shelf code; sample: “Tầng 2 · Phòng R-204 · Kệ S-12”. Show one line per physical copy; this first line is the primary shelf location returned by the sync (D27). | FR-01-01 |
| 5 | Shelf location line — copy 2 | Shelf location line | Same source; sample: “Tầng 1 · Phòng R-102 · Kệ S-08”. The screen shows the synced data of each copy. | FR-01-01 |
| 6 | Save to my list | Primary button | “Lưu vào danh sách”; available for physical books only. | FR-03-06 |
| 7 | View on map | Secondary button | “Xem trên bản đồ”; show only when a physical copy has a usable room location. | FR-01-03 |
| 8 | Unavailable shelf location | Banner | MSG-06: “Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé.” Keep the book title visible. | FR-01-07 |
| 9 | Online-only information | Banner | “Sách này chỉ có bản trực tuyến, không có vị trí trên kệ.” Do not show shelf locations, Save or View on map. | FR-01-06 |
| 10 | Save confirmation | Toast | “Đã lưu sách vào danh sách của bạn.” | FR-03-06 |
| 11 | Already-saved confirmation | Toast | “Sách này đã có trong danh sách của bạn.” | FR-03-24 |
| 12 | Network/load error | Banner and secondary button | MSG-04: “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” Show “Thử lại” to retry loading. | FR-04-20* |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | `img/S-F01-01/S-F01-01.png` | Book title and author; one shelf-location line for each physical copy, the primary shelf location first (D27); Save and View on map actions. | FR-01-01, FR-03-06, FR-01-03 |
| Empty | Not applicable | This is a single-book location view, not a list; no separate Empty state is defined. | — |
| Loading | `img/S-F01-01/S-F01-01-loading.png` | Skeleton placeholders replace the title, author, location lines and action areas while data loads. | FR-01-01 |
| Error — shelf location unavailable | `img/S-F01-01/S-F01-01-error.png` | Book title remains visible; show the exact MSG-06 banner instead of shelf details. | FR-01-07 |
| Error — network/load failure | `img/S-F01-01/S-F01-01-error-2.png` | Show MSG-04 and the “Thử lại” action when the page cannot load. | FR-04-20* |
| Success — saved | `img/S-F01-01/S-F01-01-success.png` | Keep the Default layout and show the save-confirmation Toast. | FR-03-06 |
| Success — already saved | `img/S-F01-01/S-F01-01-success-2.png` | Keep the Default layout and show the already-saved Toast. | FR-03-24 |
| Information — online only | `img/S-F01-01/S-F01-01-online-only.png` | Show online-only information; omit shelf locations, Save and View on map. | FR-01-06 |

## Actions and where they go

| Element / event | User action | Result / destination |
|---|---|---|
| Back | Tap | Existing OPAC Book Detail page (exit). |
| View on map | Tap | S-F01-02; show the relevant floor and room when the room code is available on the floor plan. |
| Save to my list — signed in | Tap | Save the physical book; remain on S-F01-01 and show the success Toast. If already saved, show the already-saved Toast. |
| Save to my list — not signed in | Tap | Open shared modal M-F00-01. If the Reader signs in, continue the shared sign-in flow and return to the original action. |
| Try again | Tap | Retry loading the screen after MSG-04. |

## Open questions

None. Decisions: see [decision-index.md](../../decision-index.md#s-f01-01).

