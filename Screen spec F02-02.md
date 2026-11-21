# Screen Spec: S-F02-02 Book information and reviews (QR landing page)

| Field | Value |
|---|---|
| Screen ID | `S-F02-02` |
| Screen name | Book information and reviews (QR landing page) |
| Actor | Reader |
| Priority | Must (edit and delete own review are Could parts inside this Must screen) |
| Feature | `F-02 Reviews & QR` |
| Activity diagrams | `AD-UC-06`, `AD-UC-04` (called) |
| Mockup image | `img/S-F02-02.png` |
| Frame width | 360px (exported 3x = 1080px) |
| Wireframe source | `src/S-F02-02.html` [NEEDS CLARIFICATION: wireframe source file is not yet placed in `screens/src/`] |
| Author | Hoa |
| Status | Draft |

## 1. Purpose

**Shown when:** The reader scans the QR code label on a physical book with a phone camera to open the QR landing link (`AD-UC-06` r1), or returns directly to this screen after completing OTP verification on `S-F00-02` following a signed-out review action (`AD-UC-04` c1)[cite: 3, 9, 14].

**The user leaves this screen when:** The reader taps the “Xem sách trên OPAC” link (`#3`) to open the book’s existing OPAC Book Detail page (exit) (`L8-08`), or triggers a signed-out write, edit, or delete review action and chooses “Đăng nhập” in `M-F00-01` to go to `S-F00-01`[cite: 3, 8, 14].

## 2. Mockup

![S-F02-02](img/S-F02-02.png)

Numbered reference image: `img/S-F02-02-numbered.png` (element numbers `#1`–`#9` match Section 3; feedback elements `#10`–`#14` appear in non-default states)[cite: 15, 16].

Visual styling, spacing, typography, and colour tokens follow `EXTERNAL DESIGN/ui-conventions.md#6-design-tokens`[cite: 2, 13].

### State → Image

| State | Image |
|---|---|
| Default | `img/S-F02-02.png` |
| Empty | `img/S-F02-02-empty.png` |
| Loading | `img/S-F02-02-loading.png` |
| Error (invalid QR / book not found) | `img/S-F02-02-error.png` |
| Error-2 (network / load failure) | `img/S-F02-02-error-2.png` |
| Error-3 (review validation / ownership rejection) | `img/S-F02-02-error-3.png` |
| Success | `img/S-F02-02-success.png` |

## 3. Element inventory

This screen embeds the **same review panel as `S-F02-01`** (`#4`–`#9`, `#11`, `#13`), reusing identical component names and rules (`L8-07`), with the Report action omitted[cite: 1, 8, 15].

| # | Element | Type | Content / data source | Required | Validation |
|---|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back icon button (accessible name “Quay lại”); title “Thông tin và đánh giá sách”[cite: 13, 15, 16] | Yes | none |
| 2 | Book information | Book row | Neutral grey “Cover” placeholder block; `Book catalogue › title` (e.g., “Principles of Economics”), `Book catalogue › author` (e.g., “N. Gregory Mankiw”), `Book catalogue › subjects` (e.g., “Chủ đề: Kinh tế học”), and section “Tóm tắt” with `Book catalogue › summary` (`FR-02-05`)[cite: 15, 16] | Yes | none |
| 3 | OPAC book link | Text link | “Xem sách trên OPAC” (`FR-02-05`, `L8-08`)[cite: 8, 15, 16] | Yes | none |
| 4 | Review editor (same review panel as `S-F02-01`) | Text area with counter | Section heading “Viết đánh giá”, label “Nội dung đánh giá”, placeholder “Chia sẻ cảm nhận của bạn về cuốn sách...”, bound to `Book review › review text`; counter `<n>/2.000` (e.g., `0/2.000`). In edit mode, pre-fills the reader’s existing `Book review › review text` and displays a cancel edit control (`FR-02-01`, `FR-02-03`, `FR-02-04`, `FR-02-11`)[cite: 15, 16] | Yes | Required on submit: plain text only, 1–2,000 characters (`FR-02-01`, `FR-02-03`, `FR-02-11`). Reject empty text or >2,000 characters[cite: 9, 15] |
| 5 | Anonymous posting (same review panel as `S-F02-01`) | Checkbox | Label “Đăng ẩn danh”; bound to `Reader accounts › full registered name` (unchecked by default: displays full name as registered; checked: displays “Bạn đọc ẩn danh”) (`FR-02-22`)[cite: 13, 15, 16] | No | none |
| 6 | Review guideline (same review panel as `S-F02-01`) | Text link | “Xem quy định viết đánh giá của thư viện” (`AD-UC-13` Q1)[cite: 15, 16] | No | none |
| 7 | Submit review (same review panel as `S-F02-01`) | Primary button | “Đăng đánh giá” (create mode) / “Lưu thay đổi” (edit mode) (`FR-02-01`, `FR-02-03`)[cite: 13, 15, 16] | Yes | none |
| 8 | Own review (same review panel as `S-F02-01`) | Review item | Section heading “Đánh giá từ bạn đọc”; `Book review › reviewer` (full name or “Bạn đọc ẩn danh”), badge “Đánh giá của bạn”, `Book review › posted date` (`dd/MM/yyyy`), `Book review › review text` (no internal review ID displayed on UI); Text buttons “Sửa” and “Xoá đánh giá” (`.danger` variant); no Report action (`FR-02-03`, `FR-02-04`, `FR-02-13`, `FR-02-22`)[cite: 13, 15, 16] | No | none |
| 9 | Other readers’ reviews / Page-level feedback | Review item / Banner | **Review item:** `Book review › reviewer` (full name or “Bạn đọc ẩn danh”), `Book review › posted date` (`dd/MM/yyyy`), `Book review › review text` (no internal review ID displayed on UI; no Report action on QR page) (`FR-02-02`, `FR-02-13`, `FR-02-22`).<br>**Banner (error states):** Invalid QR error (“Không tìm thấy sách.” with next-step guidance, `FR-02-16`), `MSG-04` network error (“Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.”, `FR-04-20`), or non-owner edit/delete rejection (`FR-02-11`)[cite: 13, 15, 16] | No | none |
| 10 | Empty list message | Empty state | “Không có đánh giá nào để hiển thị. Hãy là người đầu tiên viết đánh giá cho cuốn sách này.” while `#2` Book information remains visible (`FR-02-15`)[cite: 15] | No | none |
| 11 | Success confirmation | Toast | “Đã đăng đánh giá.” / “Đã cập nhật đánh giá.” / “Đã xoá đánh giá.” (`FR-02-12`)[cite: 13, 15] | No | none |
| 12 | Loading placeholder | Skeleton | Placeholder blocks matching `#2` Book information, `#4–#7` review editor, and `#8–#9` review list (`MSG-05`)[cite: 13, 15] | No | none |
| 13 | Field validation feedback | Inline error | Shared review-panel validation error displayed directly under `#4` Review editor with “!” icon and 2px `colour/error-red` field border when review text is empty or exceeds 2,000 characters (`FR-02-01`, `FR-02-11`)[cite: 13, 15] | No | none |
| 14 | Retry action | Secondary button | “Thử lại” inside the `MSG-04` error Banner (`FR-04-20`)[cite: 13, 15] | No | none |

## 4. States

| State | What the user sees | Trigger |
|---|---|---|
| Default | `#1` Screen header, `#2` Book information (cover placeholder, title, author, subjects, summary), `#3` “Xem sách trên OPAC” link, `#4–#7` empty Review editor (`0/2.000`, “Đăng ẩn danh” unchecked, “Đăng đánh giá”), and `#8–#9` published reviews (newest first, excluding `Removed` reviews; own reviews show “Sửa” and “Xoá đánh giá”; other readers’ reviews have no Report action) (`FR-02-05`, `FR-02-01`, `FR-02-02`, `FR-02-03`, `FR-02-04`, `FR-02-13`, `FR-02-22`)[cite: 15, 16]. | Reader scans a valid physical book QR code that links to a book in the synced catalogue with at least 1 published review (`AD-UC-06` r1)[cite: 3, 15]. |
| Empty (no data) | `#1` Screen header, `#2` Book information, `#3` OPAC book link, `#4–#7` Review editor, and `#10` Empty state message replacing the review list (`FR-02-15`)[cite: 15]. | Scanned QR code links to a valid book in the catalogue that has 0 published reviews (all reviews are `Removed` or none exist) (`FR-02-15`)[cite: 15]. |
| Loading | `#1` Screen header and `#12` Skeleton blocks replacing book information and review content; no loading text (`MSG-05`)[cite: 13, 15]. | Initial page load upon QR scan, or saving/updating/deleting a review. |
| Error | **Error (invalid QR / book not found):** `#9` error Banner displays “Không tìm thấy sách.” with next-step guidance (`FR-02-16`)[cite: 1, 15].<br>**Error-2 (network / load failure):** Existing page content preserved; `#9` error Banner displays `MSG-04` (“Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.”) with `#14` Secondary button “Thử lại” (`FR-04-20`)[cite: 13, 15].<br>**Error-3 (review validation / ownership rejection):** Existing page content preserved; `#4` Review editor gets 2px `colour/error-red` border with `#13` Inline error below the field (`FR-02-01`, `FR-02-11`), or `#9` error Banner displays non-owner action rejection (`FR-02-11`)[cite: 13, 15]. | QR code is not linked to any book in the synced catalogue (`FR-02-16`); network/server fails while loading or saving (`FR-04-20`); reader submits empty or >2,000-character review text (`AD-UC-04` d3 [No], d5 [No]); or reader attempts to edit/delete another reader’s review (`AD-UC-04` d4 [No], d7 [No])[cite: 1, 9, 15]. |
| Success / confirmation | `#11` Toast appears for 4 seconds (“Đã đăng đánh giá.”, “Đã cập nhật đánh giá.”, or “Đã xoá đánh giá.”) and the review list refreshes to reflect the saved, updated, or removed review (`FR-02-12`)[cite: 13, 15]. | Reader successfully submits a new review (`AD-UC-04` s3), saves an edited review (`AD-UC-04` s5), or confirms deletion in `M-F02-01-01` (`AD-UC-04` s6)[cite: 9, 15]. |

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | `#1` Back (`Quay lại`) | tap | Keeps reader on screen in current wireframe [NEEDS CLARIFICATION: destination when opened directly from phone camera QR scan is unresolved; see Section 9 Q1][cite: 1, 15]. | stays |
| 2 | `#3` OPAC book link (`Xem sách trên OPAC`) | tap | Leaves the QR landing page and opens the book’s existing OPAC Book Detail page (`FR-02-05`, `L8-08`)[cite: 1, 8, 15]. | Existing OPAC Book Detail (exit) |
| 3 | `#4` Review editor / `#5` Anonymous posting / `#7` Submit review (`Đăng đánh giá` / `Lưu thay đổi`) [signed in] | type plain text, optionally toggle “Đăng ẩn danh”, and tap submit | Validates text (1–2,000 chars, plain text). If invalid, shows `#13` Inline error. If valid, saves new review (`FR-02-01`, `FR-02-22`) or updates own review (`FR-02-03`), shows `#11` Toast (“Đã đăng đánh giá.” or “Đã cập nhật đánh giá.”), and refreshes `#8–#9` review list (`FR-02-12`)[cite: 9, 13, 15]. | stays |
| 4 | `#4` Review editor / `#7` Submit review [signed out] | attempt to write/submit a review without a valid session | Denies unauthenticated write (`FR-04-08`) and opens sign-in prompt `M-F00-01` (`MSG-01`). If reader chooses “Đăng nhập”, navigates to `S-F00-01` → `S-F00-02` and returns to `S-F02-02` upon OTP acceptance (`L8-01`)[cite: 8, 9, 13, 15]. | `M-F00-01` (see `screen-spec-S-F00-01.md` §3.1) |
| 5 | `#6` Review guideline (`Xem quy định viết đánh giá của thư viện`) | tap | Opens library review rules [NEEDS CLARIFICATION: destination URL is not yet specified][cite: 15]. | stays |
| 6 | `#8` Own review › `Sửa` [signed in] | tap | Switches `#4` Review editor into edit mode pre-filled with the selected review’s text, changes `#7` Primary button to “Lưu thay đổi”, and displays a cancel edit control (`FR-02-03`, `AD-UC-06` c2)[cite: 3, 15]. | stays |
| 7 | `#8` Own review › `Sửa` [signed out] | tap | Denies unauthenticated edit (`FR-04-08`) and opens `M-F00-01` (`MSG-01`)[cite: 3, 13, 15]. | `M-F00-01` (see `screen-spec-S-F00-01.md` §3.1) |
| 8 | `#8` Own review › `Xoá đánh giá` [signed in] | tap | Opens shared confirmation modal `M-F02-01-01` over dimmed `S-F02-02` (`AD-UC-06` c3, `AD-UC-04` r4/d6)[cite: 3, 9, 15]. | `M-F02-01-01` (see `screen-spec-S-F02-01.md` §3.1)[cite: 1, 2] |
| 9 | `#8` Own review › `Xoá đánh giá` [signed out] | tap | Denies unauthenticated delete (`FR-04-08`) and opens `M-F00-01` (`MSG-01`)[cite: 3, 13, 15]. | `M-F00-01` (see `screen-spec-S-F00-01.md` §3.1)[cite: 1, 2] |
| 10 | `#14` Retry action (`Thử lại`) | tap | Retries the failed load or save request and clears the `MSG-04` Banner on success (`FR-04-20`)[cite: 13, 15]. | stays |

## 6. Screen-level rules

| Rule ID | Rule | Source |
|---|---|---|
| SR-001 | **Same review panel as `S-F02-01`, without Report:** `S-F02-02` embeds the identical review editor, anonymity toggle, own-review actions (“Sửa”, “Xoá đánh giá”), and deletion modal `M-F02-01-01` defined in `screen-spec-S-F02-01.md` using the same component names (`L8-07`), but omits “Báo cáo đánh giá” (`UC-14` is not called from `AD-UC-06`). | `L8-07`, `AD-UC-06`, `ui-conventions.md` §3[cite: 1, 3, 8, 13] |
| SR-002 | **Public reading, authenticated mutations:** Scanning a QR code to view book details and published reviews requires no sign-in (`FR-02-05`, `FR-02-02`). Creating, editing, or deleting a review requires a valid reader session; unauthenticated attempts open `M-F00-01` (`MSG-01`) and return to `S-F02-02` after OTP sign-in. | `FR-04-08`, `AD-UC-04` d0/d1, `L8-01`[cite: 3, 8, 9] |
| SR-003 | **Exit path to existing OPAC:** Because `S-F02-02` is entered externally via a phone camera QR scan, it provides the “Xem sách trên OPAC” Text link (`#3`) to the book’s existing OPAC Book Detail page (`L8-08`). | `FR-02-05`, `L8-08`, `screen-transition.md` §1[cite: 1, 8, 14] |
| SR-004 | **Invalid QR code handling:** When the scanned QR code does not map to any book in the synced catalogue, the system displays “Không tìm thấy sách.” (`FR-02-16`). | `FR-02-16`, `screen-list.md`[cite: 1, 3, 15] |
| SR-005 | **Background QR scan counting:** Opening `S-F02-02` for a valid physical book triggers a background QR scan count increment (`FR-02-06`) with no separate UI element on this screen. | `FR-02-06`, `screen-list.md` |
| SR-006 | **Visibility, identity, and validation rules:** Published reviews exclude `Removed` reviews (`FR-02-13`), display either the registered card full name or “Bạn đọc ẩn danh” (`FR-02-22`), hide internal review IDs, allow multiple reviews per reader (`AD-UC-04` Q1), and enforce 1–2,000 plain-text characters (`FR-02-01`, `FR-02-03`, `FR-02-11`). | `FR-02-01`, `FR-02-03`, `FR-02-11`, `FR-02-13`, `FR-02-22`, `AD-UC-04` Q1[cite: 9, 13, 15] |
| SR-007 | **Could scope boundary:** Edit own review (`FR-02-03`) and Delete own review (`FR-02-04`) are Could parts inside this Must screen; if cut from release scope, their controls and `M-F02-01-01` are omitted without removing `S-F02-02`. | `screen-list.md` notes, `AD-UC-04` Q4[cite: 3, 9] |

## 7. Linked requirements

| FR ID | What this screen does for it |
|---|---|
| `FR-02-01` | Provides the shared review editor (`#4`, 1–2,000 plain-text characters) and “Đăng đánh giá” button (`#7`) to submit a new review from the QR landing page. |
| `FR-02-02` | Displays published reviews (`#8`, `#9`) for the scanned book, newest first. |
| `FR-02-03` | Provides “Sửa” on the reader’s own review (`#8`), pre-fills `#4`, and saves changes via “Lưu thay đổi” (`#7`). |
| `FR-02-04` | Provides “Xoá đánh giá” on the reader’s own review (`#8`) and confirms removal from public display via modal `M-F02-01-01`. |
| `FR-02-05` | Displays physical book information (`#2`: title, author, subjects, summary) and the “Xem sách trên OPAC” link (`#3`) upon scanning a valid book QR code. |
| `FR-02-11` | Rejects empty/over-limit review text via `#13` Inline error and rejects non-owner edit/delete attempts via `#9` Banner. |
| `FR-02-12` | Displays confirmation Toast (`#11`) and refreshes the review list (`#8–#9`) after creating, editing, or deleting a review. |
| `FR-02-13` | Excludes reviews in state `Removed` from the displayed review list (`#8–#9`). |
| `FR-02-15` | Replaces the review list with Empty state message `#10` while keeping `#2` Book information visible when the book has no published reviews. |
| `FR-02-16` | Displays the “Không tìm thấy sách.” error state (`#9` Banner) when the scanned QR code is linked to no book. |
| `FR-02-22` | Provides the “Đăng ẩn danh” checkbox (`#5`) and displays either the registered card full name or “Bạn đọc ẩn danh” on each review item (`#8–#9`). |
| `FR-04-08` | Checks reader session on write, edit, and delete review actions, opening `M-F00-01` (`MSG-01`) when signed out. |
| `FR-04-20` | Preserves currently displayed data and shows `MSG-04` Banner (`#9`) with “Thử lại” (`#14`) when loading or saving fails due to a network/server error. |

## 8. Responsive and accessibility notes

- **Smallest supported width:** 360px (Reader mobile viewport opened from phone camera, exported at 3x = 1080px)[cite: 13, 15].
- **What collapses or stacks on a narrow screen:** All sections (`#2` Book information, `#3` OPAC link, `#4–#7` Review editor, `#8–#9` Review items) stack vertically in a single 100%-width column with 16px screen padding (`space/unit`). Confirmation modal `M-F02-01-01` stacks buttons vertically at 360px with Destructive button on top and Secondary button (“Huỷ”) below (`ui-conventions.md` §3)[cite: 13].
- **Information never carried by colour alone:** Validation errors on `#4` combine a 2px `colour/error-red` field border with `#13` Inline error containing a “!” icon and explanatory text; `#9` error Banners pair left border colour with an icon and text; `#3` “Xem sách trên OPAC” and `#6` guideline Text links use underline + `colour/link`; Destructive actions (`#8` “Xoá đánh giá”, `M-F02-01-01` `#2`) pair `colour/error-red` with explicit labels and a trash icon (`ui-conventions.md` §5)[cite: 13].
- **Text contrast and minimum size:** All text and control borders meet WCAG 2.2 AA (`≥ 4.5:1` for body/labels/links, `≥ 3:1` for borders and 20px `SVN-Gilroy` title) using tokens in `ui-conventions.md` §6. `#4` Text area uses 16px `Inter` text to prevent mobile browser zoom on focus. Interactive targets (`#1` Back button 44×44px, `#5` Checkbox row 44px height, `#7` Primary button 48px height) meet the 44×44px Reader minimum (`ui-conventions.md` §5). Focusable controls display a 2px `colour/focus` (`#1074C3`) focus ring with 2px offset[cite: 13].

## 9. Open questions

| # | Question | Blocking? | Status |
|---|---|---|---|
| 1 | `[NEEDS CLARIFICATION: What should the Screen header Back action (#1) do when S-F02-02 is opened directly by scanning a QR code with a phone camera — navigate to the existing OPAC Book Detail page, use browser history back, or omit the Back button?]` | No | Open — Back button kept visible per `ui-conventions.md` §3; no navigation destination asserted until team confirms[cite: 1, 13, 15]. |
| 2 | `[NEEDS CLARIFICATION: Should S-F02-02 include a “Xem thêm đánh giá” Load more button (UC-05 pagination rule, Q2 in screen-spec-chung.md), or display reviews without pagination?]` | Yes | Open — no Load more control is drawn on `S-F02-02` (`ui-conventions.md` §3 lists Load more only for `S-F02-01`); requires team confirmation per Q2[cite: 1, 2, 13, 15]. |
| 3 | May `S-F02-02` show the “Báo cáo đánh giá” action on other readers’ reviews? | No | Closed 08/11/2026 (`L8-07`): **No** — Report (`UC-14`) is available only on `S-F02-01`, because `AD-UC-06` has no Report call[cite: 1, 8, 15]. |
| 4 | `[NEEDS CLARIFICATION: What is the exact destination URL for the library review guideline link (#6 “Xem quy định viết đánh giá của thư viện”)?]` | No | Open — rendered as a Text link label only; destination URL unresolved (`AD-UC-13` Q1)[cite: 15]. |
| 5 | `[NEEDS CLARIFICATION: ui-conventions.md §3 lists Book row for S-F03-01, S-F03-03, S-F03-07, and S-F02-03, omitting S-F02-02. Confirm that Book row (with cover placeholder, title, author, subjects, and summary, without access-format label) is approved for #2 Book information.]` | No | Open — reused existing Book row structure without cover image or access-format label[cite: 13, 15]. |

---

## Completion checklist

- [x] The mockup is a separate cropped image file, named with the Screen ID (`img/S-F02-02.png`).
- [x] Every visible element in the mockup appears in the element inventory (`#1`–`#9` in Default; `#10`–`#14` in Empty/Loading/Error/Success states).
- [x] Every input element has a validation rule or an explicit "none" (`#4` Text area with counter has 1–2,000 plain-text rule; `#5` Checkbox has `none`).
- [x] All five states are filled in, or marked "not applicable" with a reason (`Default`, `Empty`, `Loading`, `Error` / `Error-2` / `Error-3`, `Success`).
- [x] Every navigation target is a Screen ID that exists in the Screen List (`M-F00-01`, `M-F02-01-01`), `stays`, or `Existing OPAC Book Detail (exit)`.
- [x] Every element that displays data names the field it displays (`Book catalogue › title/author/subjects/summary`, `Book review › review text/reviewer/posted date`, `Reader accounts › full registered name`).
- [x] Every linked FR exists in the Function List, and every action of this screen in an activity diagram is covered by an interaction row (`AD-UC-06`, `AD-UC-04`).