# Screen Spec: S-F01-01 Shelf location (with Save to my list)

| Field | Value |
|---|---|
| Screen ID | `S-F01-01` |
| Screen name | Shelf location (with Save to my list) |
| Actor | Reader |
| Priority | Must |
| Feature | `F-01` |
| Activity diagrams | `AD-UC-01`, `AD-UC-12` (Save action) |
| Mockup image | `img/S-F01-01-numbered.png`; state panels: `img/S-F01-01-states.png` |
| Status | Draft — pending group review and wireframe/export verification |
| Frame width | 360px (export at 3x = 1080px) |
| Wireframe source | [NEEDS CLARIFICATION: confirm committed source path under `screens/src/`] |
| Wireframe author | Nhi |
| Screen spec author | Nhi |
| UI conventions | v0.8 |

## 1. Purpose

**Shown when:** A Reader selects **Shelf location** on the existing OPAC Book Detail page to see the floor, room and shelf code for a book. The screen may also be reopened from `S-F01-02` using Back. This screen does not require Reader sign-in for viewing shelf information.

**The user leaves this screen when:** They select Back to return to the existing OPAC Book Detail page, or select **Xem trên bản đồ** to open `S-F01-02`. Selecting **Lưu vào danh sách** keeps the Reader on this screen after a successful save. If the Reader is not signed in, the shared modal `M-F00-01` is shown; choosing Sign in continues through `S-F00-01` and returns to the requested action.

## 2. Mockup

Ảnh wireframe đánh số của màn hình S-F01-01 và ảnh tổng hợp các trạng thái hiện có.

**Numbered wireframe**

![S-F01-01 — numbered wireframe](https://raw.githubusercontent.com/chihvcte-beep/dbiz2-group-h/main/%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/img/S-F01-01-numbered.png)

[Open original numbered image on GitHub](https://github.com/chihvcte-beep/dbiz2-group-h/blob/main/%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/img/S-F01-01-numbered.png)

**Current state panels**

![S-F01-01 — state panels](https://raw.githubusercontent.com/chihvcte-beep/dbiz2-group-h/main/%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/img/S-F01-01-states.png)

[Open original state image on GitHub](https://github.com/chihvcte-beep/dbiz2-group-h/blob/main/%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/img/S-F01-01-states.png)

> **Draft review note:** The images above are the existing repository exports, embedded directly in this section for visual review. The state-specific images have not yet been exported as separate files; each row below points to the relevant panel in the combined `-states.png` image. Do not treat the exports as approved until the required size and UI-conventions checks are complete.

| State | Image / panel | What to inspect |
|---|---|---|
| Default | `S-F01-01-numbered.png` | Wireframe đánh số. |
| Loading | Panel in `S-F01-01-states.png` | Panel Loading trong ảnh trạng thái tổng hợp. |
| Error — shelf location unavailable | Panel in `S-F01-01-states.png` | Panel vị trí kệ không khả dụng. |
| Error — network/load failure | Panel in `S-F01-01-states.png` | Panel lỗi mạng/tải trang. |
| Success — saved / already saved | Panel in `S-F01-01-states.png` | Các panel phản hồi đã lưu / đã có trong danh sách. |
| Information — online only | Panel in `S-F01-01-states.png` | Panel sách chỉ có bản trực tuyến. |

Use UI Conventions v0.8 for components, labels, messages and design tokens. Reader frame: 360px, target export at 3x (1080px).
## 3. Element inventory

Numbering follows `S-F01-01` wireframe notes. State-only retry behaviour is listed separately and is not a permanent Default control.

| # | Element | Type | Content / data source | Required | Validation / visibility |
|---|---|---|---|---|---|
| 1 | Back button and screen title | Screen header | `Vị trí kệ sách` | Yes | Back returns to the existing OPAC Book Detail page. |
| 2 | Book title and author | Section title | Book catalogue: title and author. Illustrative sample: `Principles of Economics` — `N. Gregory Mankiw`. | Yes | Display the selected book's catalogue data. |
| 3 | Shelf location line | Shelf location line | Book placement and library layout: floor, room code and shelf code. Example: `Tầng 2 · Phòng R-204 · Kệ S-12`. | Conditional | Show one line for each physical copy; include the map-pin icon. Do not imply stock/borrowing availability. |
| 4 | Unavailable shelf location | Banner | `MSG-06`: `Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé.` | Conditional | Show when shelf location is missing or inconsistent. Keep the book title visible. |
| 5 | Online-only information | Banner | `Sách này chỉ có bản trực tuyến, không có vị trí trên kệ.` | Conditional | Show for an online-only book. Do not show shelf location, Save or View on map actions. |
| 6 | Save to my list | Primary button | `Lưu vào danh sách` | Conditional | Show only for physical books. One Primary button is visible at a time. Requires a valid Reader session; otherwise open `M-F00-01`. |
| 7 | View on map | Secondary button | `Xem trên bản đồ` | Conditional | Show only when a physical copy has a usable room location. Opens `S-F01-02`. This is a Could-scope action (`FR-01-03`). |
| 8 | Save confirmation | Toast | `Đã lưu sách vào danh sách của bạn.` | Conditional | Show after a successful save; provisional copy pending team confirmation. |
| State only | Already-saved feedback | Informational Toast | `Sách này đã có trong danh sách của bạn.` | Conditional | Show when the book is already saved; do not add a duplicate entry. |
| State only | Network retry | Secondary button | `Thử lại` with shared `MSG-04` | Conditional | Show after a network/load failure; retain data already shown. |

## 4. States

| State | What the user sees | Trigger / outcome |
|---|---|---|
| Default | `Vị trí kệ sách`, book title and author, one shelf-location line per physical copy, and applicable Save / View on map actions. | Reader opens Shelf location from the existing OPAC Book Detail page. |
| Empty | Not applicable: this is a single-book location view, not a list. | — |
| Loading | Skeleton placeholders matching the title, location and action areas; no loading text. | System retrieves the book and shelf-location data. |
| Error — shelf location unavailable | `MSG-06` appears in place of shelf-location details while the book title remains visible. Hide View on map when there is no usable room location. | Shelf location is missing or inconsistent (`FR-01-07`). |
| Error — network/load failure | Shared `MSG-04`: `Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.` with `Thử lại`. Keep data already shown. | A network/load request fails (`FR-04-20`). |
| Success — saved | Keep the Default layout and show `Đã lưu sách vào danh sách của bạn.` as a Toast. | The physical book is added to the Reader's saved list (`FR-03-06`). |
| Message — already saved | Keep the Default layout and show `Sách này đã có trong danh sách của bạn.` as an informational Toast. No duplicate is added. | The book already exists in the Reader's saved list (`FR-03-24`). |
| Information — online only | Show `Sách này chỉ có bản trực tuyến, không có vị trí trên kệ.` Do not show shelf location, Save or View on map. | The selected book has no physical copy (`FR-01-06`). |

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | Entry | Select `Shelf location` on the existing OPAC Book Detail page. | Retrieve and display the selected book's shelf-location information. | `S-F01-01` |
| 2 | Back | Select Back. | Return to the OPAC Book Detail page from which the Reader opened this screen. | Existing OPAC Book Detail (exit) |
| 3 | View on map | Select `Xem trên bản đồ`. | Open the library map at the book's floor and highlight its room when the room code exists on the map. | `S-F01-02` |
| 4 | Save to my list — signed in | Select `Lưu vào danh sách`. | Check for an existing saved entry. If new, add the physical book and show the save Toast. | Stays on `S-F01-01` |
| 5 | Save to my list — not signed in | Select `Lưu vào danh sách`. | Ask the Reader to sign in through the shared sign-in modal. | `M-F00-01`; Sign in continues to `S-F00-01` |
| 6 | Save to my list — already saved | Select `Lưu vào danh sách` when the book is already saved. | Do not add a duplicate; show the already-saved informational Toast. | Stays on `S-F01-01` |
| 7 | Retry | Select `Thử lại` after `MSG-04`. | Retry the failed request and retain data already shown. | Stays on `S-F01-01` |

`M-F00-01` is a shared modal and is specified in the shared screen documentation; do not duplicate its content here.

## 6. Screen-level rules

| Rule ID | Rule | Source |
|---|---|---|
| SR-001 | Display the selected book's title and author and its shelf location, with one location line per physical copy. | `FR-01-01`; `AD-UC-01`; Nhi wireframe notes |
| SR-002 | If the book is online-only, show the online-only information and do not show shelf location, Save or View on map. | `FR-01-06`; `AD-UC-01` |
| SR-003 | If shelf location is missing or inconsistent, show the exact `MSG-06` wording and keep the book title visible. | `FR-01-07`; UI Conventions v0.8 |
| SR-004 | Save is available only for physical books. | `FR-03-06`; `AD-UC-12`; Nhi wireframe notes |
| SR-005 | A Reader without a valid session must use `M-F00-01` before the signed-in Save action can continue. | `FR-04-08`; `AD-UC-12`; Screen List |
| SR-006 | Check for an existing saved entry before adding a book; do not create a duplicate. | `FR-03-24`; `AD-UC-12` |
| SR-007 | `Xem trên bản đồ` is a Could-scope action and is shown only when a physical copy has a usable room location. | `FR-01-03`; Screen List; Nhi wireframe notes |
| SR-008 | Do not add a link from this screen to the saved-books list. | L8-06; Nhi wireframe notes |
| SR-009 | A network/load failure uses shared `MSG-04` and `Thử lại`. | `FR-04-20`; UI Conventions v0.8 |
| SR-010 | Do not display copy availability, borrowing status or a list of copies available to borrow. | W0 scope; Nhi wireframe notes |

## 7. Linked requirements

| FR ID | What this screen does for it |
|---|---|
| `FR-01-01` | Displays the floor, room and shelf code for each physical copy of the selected book. |
| `FR-01-06` | Displays the online-only information when the book has no physical copy. |
| `FR-01-07` | Displays `MSG-06` when shelf location is missing or inconsistent. |
| `FR-01-03` | Provides the conditional `Xem trên bản đồ` entry to `S-F01-02` (Could scope). |
| `FR-03-06` | Provides the Save action for physical books. |
| `FR-03-24` | Displays already-saved feedback and prevents duplicate entries. |
| `FR-04-20` | Handles network/load errors with `MSG-04` and `Thử lại`. |
| `FR-04-08` | Requires a valid Reader session for the Save action; sign-in is handled through `M-F00-01`. |

## 8. Responsive and accessibility notes

- Reader frame: 360px; export at 3x (1080px). Smallest supported width: 360px.
- Use UI Conventions v0.8 design tokens and typography; do not introduce arbitrary colours.
- Shelf-location lines include a map-pin icon and readable floor, room and shelf codes.
- Keep the full shelf code on one line where possible; do not rely on colour alone to communicate location or state.
- Interactive targets must be at least 44×44px, with a visible 2px focus ring.
- Text contrast: at least 4.5:1; meaningful control boundaries: at least 3:1.
- Toast feedback must remain readable and must not obscure the book title or essential location information.
- Book title and author are catalogue data. Sample title, author and shelf codes are illustrative until checked against synced catalogue data.

## 9. Open questions

| # | Question | Blocking? | Status |
|---|---|---|---|
| 1 | Confirm that `Đã lưu sách vào danh sách của bạn.` is the approved success Toast wording for `FR-03-06`. | No | Open |
| 2 | Confirm whether already-saved feedback for `FR-03-24` should remain an informational Toast. | No | Open |
| 3 | Confirm whether multiple physical copies should be grouped by holding/copy or displayed as separate shelf-location lines. | No | Open; current treatment is one line per physical copy |
| 4 | Confirm that the final numbered and state exports are separate 1080px-wide images and comply with v0.8. | Yes (mockup approval) | Open |
| 5 | Confirm the committed wireframe source path under `screens/src/`. | No | Open |

---

## Completion checklist

- [x] All eight numbered elements in Nhi's v0.8 notes are accounted for.
- [x] Empty is marked not applicable with a reason.
- [x] Loading, location-unavailable, network-error, saved, already-saved and online-only states are described.
- [x] Navigation targets use existing Screen IDs or existing OPAC destinations.
- [x] The shared sign-in modal is referenced, not redefined.
- [ ] Success Toast wording and already-saved feedback treatment confirmed.
- [ ] Final mockup exports verified at 1080px and reviewed against UI Conventions v0.8.
- [ ] Group review and approval completed.
