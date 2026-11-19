# Wireframe notes: S-F03-02 Reading History and Preferences

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back to OPAC Personal Area (or S-F03-07 if invoked from recommendations prompt); title “Lịch sử đọc & sở thích” | — |
| 2 | History section title | Section header | “Lịch sử đọc” with count badge (e.g., “3 cuốn”) | FR-03-01 |
| 3 | Reading history entry | Book row | Book catalogue › title, author plus neutral grey “Cover” placeholder; loan/online history timestamp; access format tag (“Bản giấy” / “Trực tuyến”) | FR-03-01, FR-03-02, FR-03-03 |
| 4 | Reading status badge | Status badge | Reading history & preferences › reading status; exactly two valid states: “Đang đọc” (Reading) or “Đã đọc xong” (Finished) | FR-03-04 |
| 5 | Progress indicator | Progress bar & label | Reading history & preferences › reading progress; numeric percentage (0–100%) and visual progress bar | FR-03-04 |
| 6 | Update progress trigger | Secondary button | “Cập nhật” button on each history row; expands inline edit form for status & progress | FR-03-04 |
| 7 | Status selector | Segmented control | Two options: “Đang đọc” (Reading) and “Đã đọc xong” (Finished) | FR-03-04 |
| 8 | Progress input | Number input with unit | Integer field (0–100) with “%” suffix; defaults to current reading progress | FR-03-04 |
| 9 | Save progress button | Primary button | “Lưu tiến độ”; validates 0 <= progress <= 100% | FR-03-04 |
| 10 | Cancel edit button | Ghost button | “Hủy”; closes inline edit form without changing saved values | — |
| 11 | Preferences section title | Section header | “Sở thích đọc sách” with subtext “Chọn các chủ đề bạn quan tâm để nhận gợi ý sách phù hợp” | FR-03-05 |
| 12 | Subject chips selector | Multi-select chips | Filter chips of synced catalogue subjects: “Kinh tế”, “Marketing”, “Công nghệ thông tin”, “Kỹ năng mềm”, “Văn học”, “Khoa học”; selected chips highlighted | FR-03-05 |
| 13 | Save preferences button | Primary button | “Lưu sở thích”; validates selected subjects against catalogue | FR-03-05 |
| 14 | Empty history message | Empty state | “Chưa có lịch sử đọc nào. Sách bạn mượn hoặc đọc trực tuyến sẽ tự động xuất hiện tại đây.” with illustration/icon | FR-03-01* |
| 15 | Invalid progress error | Inline error banner | “Tiến độ đọc phải từ 0% đến 100%. Dữ liệu đã lưu trước đó được giữ nguyên.” (Shown on values like 120%) | FR-03-22 |
| 16 | Success confirmation | Toast | “Đã cập nhật tiến độ đọc.” / “Đã lưu sở thích đọc.” | FR-03-01, FR-03-05 |
| 17 | Loading placeholder | Skeleton | Skeleton rows for reading history cards and subject chips | MSG-05 |
| 18 | Page-level error | Banner with retry | MSG-04 — “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” with “Thử lại” button | FR-04-20 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F03-02.png, img/S-F03-02-numbered.png | Reading history list showing books with format labels, status badges, progress bars, and update triggers. Below is the subject preferences section with selected chips. | FR-03-01, FR-03-04, FR-03-05 |
| Empty | img/S-F03-02-empty.png | Empty state for reading history with friendly icon and guidance; preferences section remains visible and editable. | FR-03-01* |
| Loading | img/S-F03-02-loading.png | Skeleton cards and chips while history and preferences are being retrieved. | MSG-05 |
| Error | img/S-F03-02-error.png | User entered invalid progress (e.g. 120%); inline error banner appears, and previous value (20%) is retained. | FR-03-22 |
| Success | img/S-F03-02-success.png | Updated progress (e.g. 65%) reflected in row with green success toast notification. | FR-03-01, FR-03-04 |

## Actions and where they go

| Element | User action | Goes to |
|---|---|---|
| Back navigation | Tap `<` button | Existing OPAC personal area (or S-F03-07 if arrived from recommendations prompt) |
| Reading history row / Cập nhật | Tap to expand edit controls | Opens inline status & progress editor on S-F03-02 |
| Lưu tiến độ (valid 0–100%) | Submit updated status & progress | S-F03-02 (Success state with toast, updated list) |
| Lưu tiến độ (invalid >100% / <0%) | Submit invalid progress | S-F03-02 (Error state: rejects update, retains saved data, displays inline alert — FR-03-22) |
| Hủy inline edit | Tap cancel | Closes editor, stays on S-F03-02 with unchanged values |
| Subject chips | Tap chip to toggle selection | Toggles active state of subject on S-F03-02 |
| Lưu sở thích | Submit selected subjects | S-F03-02 (Success toast; feeds future recommendations in S-F03-07) |
| Thử lại (on MSG-04 error) | Tap retry | Retries loading reading history and preferences |

## Open questions

| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: What is the initial status of automatically added history entries?] | Team consensus (2026-11-04): Defaults to "Reading" (Đang đọc) with 0% progress until edited by the reader. |
| 2 | [NEEDS CLARIFICATION: If a reader borrows the same physical book twice, are there duplicate history rows?] | Team consensus (2026-11-04): Yes, each borrow transaction generates a discrete history entry (FR-03-03). |
| 3 | [NEEDS CLARIFICATION: Can a book be marked "Finished" if progress is under 100%?] | Team consensus (2026-11-04): Yes, status and progress are decoupled inputs; saved as entered by the reader. |
| 4 | [NEEDS CLARIFICATION: Confirm exact Vietnamese copy for empty reading history state.] | “Chưa có lịch sử đọc nào. Sách bạn mượn hoặc đọc trực tuyến sẽ tự động xuất hiện tại đây.” |

## Scope and implementation notes

- Requires an active reader session (FR-04-08). Unauthenticated access triggers `M-F00-01` before landing here.
- Reading history entries are populated automatically via daily loan sync (FR-03-03) or opening online books (FR-03-02). There is deliberately no manual "Add book to history" button on this screen (W0 Table 3).
- Status options are strictly constrained to `Reading` (Đang đọc) and `Finished` (Đã đọc xong) (FR-03-04).
- Subject choices are dynamically validated against active subjects in the synced catalogue (AD-UC-07 Q3).
- On validation failure, the previous state is preserved without data loss (FR-03-22).
