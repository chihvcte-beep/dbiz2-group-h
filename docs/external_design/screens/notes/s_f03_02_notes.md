# Wireframe notes: S-F03-02 Reading History and Preferences

Actor: Reader · Frame: 360px (export 3x = 1080px) · UI conventions: v0.8 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back navigation | Screen header | Returns to OPAC Personal Area (or S-F03-07 if invoked from recommendations prompt) | — |
| 2 | Screen title | Screen header | “Lịch sử đọc và sở thích” | — |
| 3 | History section title | Headings / Section title | “Lịch sử đọc” with count badge (e.g. “3 cuốn”) and subtext | FR-03-01 |
| 4 | Reading history entry | Book card | Book catalogue › title, author, neutral grey “Cover” placeholder; loan/read timestamp (e.g. 12/10/2026), format label (“Bản giấy” / “Trực tuyến”) with icon, and reading status badge | FR-03-01, FR-03-02, FR-03-03 |
| 5 | Reading status badge | Status badge | Reading history & preferences › reading status; exactly two valid states: “Đang đọc” (info style) or “Đã đọc xong” (success style) | FR-03-04 |
| 6 | Progress indicator | Progress bar & label | Reading history & preferences › reading progress; numeric percentage (0–100%) and visual progress bar | FR-03-04 |
| 7 | Update progress trigger | Secondary button | “Cập nhật tiến độ” button on each history card; expands inline edit panel for status & progress | FR-03-04 |
| 8 | Status selector | Select | Native select dropdown with two choices: “Đang đọc” (Reading) and “Đã đọc xong” (Finished) | FR-03-04 |
| 9 | Progress input | Text input | Integer field (0–100) with “%” suffix; defaults to current reading progress | FR-03-04 |
| 10 | Save progress button | Primary button | “Lưu thay đổi”; single primary button on screen; validates 0 <= progress <= 100% | FR-03-04 |
| 11 | Cancel edit button | Secondary button | “Huỷ”; collapses inline edit panel without changing saved values | — |
| 12 | Preferences section title | Headings / Section title | “Sở thích đọc sách” with subtext “Chọn các chủ đề từ danh mục để hệ thống gợi ý sách phù hợp.” | FR-03-05 |
| 13 | Subject selector | Multi-select chips | One chip per synced catalogue subject: “Kinh tế”, “Marketing”, “Công nghệ thông tin”, “Kỹ năng mềm”, “Văn học”, “Khoa học”; selected chips show fill + check icon (S-F03-02 Q5) | FR-03-05 |
| 14 | Save preferences button | Secondary button | “Lưu sở thích”; validates selected subjects against catalogue | FR-03-05 |
| 15 | Empty history message | Empty state | MSG-13: “Chưa có lịch sử đọc nào. Sách bạn mượn hoặc đọc trực tuyến sẽ tự động xuất hiện tại đây.” with book icon (D24) | FR-03-01* |
| 16 | Invalid progress error | Inline error | 2px red border, “!” icon and inline error message directly below input: “Tiến độ đọc phải từ 0% đến 100%. Dữ liệu đã lưu trước đó được giữ nguyên.” | FR-03-22 |
| 17 | Page-level load error | Banner | MSG-04 — “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” with “Thử lại” button | FR-04-20 |
| 18 | Success confirmation | Toast | MSG text: “Đã cập nhật tiến độ đọc.” / “Đã lưu sở thích đọc.” | FR-03-01, FR-03-05 |
| 19 | Loading placeholder | Skeleton | Skeleton cards and lines for reading history entries and subject chips | MSG-05 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | [s_f03_02.png](../img/s_f03_02/s_f03_02.png), [s_f03_02_numbered.png](../img/s_f03_02/s_f03_02_numbered.png) | Reading history list showing 3 books with format labels, status badges, progress bars, and update triggers. Below is the subject preferences section with subject chips. | FR-03-01, FR-03-04, FR-03-05 |
| Empty | [s_f03_02_empty.png](../img/s_f03_02/s_f03_02_empty.png) | Empty state for reading history with friendly icon and guidance; preferences section remains visible and editable. | FR-03-01* |
| Loading | [s_f03_02_loading.png](../img/s_f03_02/s_f03_02_loading.png) | Skeleton cards and lines while history and preferences are being retrieved. | MSG-05 |
| Error (Inline) | [s_f03_02_error.png](../img/s_f03_02/s_f03_02_error.png), [s_f03_02_error_numbered.png](../img/s_f03_02/s_f03_02_error_numbered.png) | User entered invalid progress (e.g. 120%); 2px red border on input, inline error with “!” appears directly under input, previous value (20%) is retained. Also handles invalid subject preferences (AD-UC-07 d4 [No]). | FR-03-22 |
| Error (Page load) | [s_f03_02_error_2.png](../img/s_f03_02/s_f03_02_error_2.png) | Page-level system/network error banner with MSG-04 and “Thử lại” secondary button. | FR-04-20 |
| Success | [s_f03_02_success.png](../img/s_f03_02/s_f03_02_success.png) | Updated progress (e.g. 65%) reflected in list with floating toast notification “Đã cập nhật tiến độ đọc.”. | FR-03-01, FR-03-04 |

## Actions and where they go

| Element / event | User action / system event | Result / destination |
|---|---|---|
| Open without session | Reader navigates to S-F03-02 without active session | M-F00-01 (Sign-in prompt modal with MSG-01: “Bạn cần đăng nhập bằng thẻ thư viện để xem và quản lý lịch sử đọc.”) |
| Back navigation | Tap `<` button | Existing OPAC personal area (or S-F03-07 if arrived from recommendations prompt) |
| Reading history card / Cập nhật tiến độ | Tap button | stays; expands inline status & progress edit panel on S-F03-02 |
| Lưu thay đổi (valid 0–100%) | Submit updated status & progress | stays; updates history entry, displays floating toast “Đã cập nhật tiến độ đọc.” on S-F03-02 |
| Lưu thay đổi (invalid >100% / <0%) | Submit invalid progress | stays; rejects update, retains saved data, displays inline error with “!” on S-F03-02 (FR-03-22) |
| Huỷ inline edit | Tap “Huỷ” button | stays; collapses edit panel on S-F03-02 with unchanged values |
| Subject chips | Tap a chip | stays; toggles the selected state of that subject on S-F03-02 |
| Lưu sở thích | Submit selected subjects | stays; validates and saves preferences, displays floating toast on S-F03-02 (feeds future recommendations in S-F03-07) |
| Thử lại (on MSG-04 error) | Tap “Thử lại” button | stays; retries loading reading history and preferences on S-F03-02 |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f03-02).
