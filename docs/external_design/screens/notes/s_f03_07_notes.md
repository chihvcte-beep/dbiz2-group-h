# Wireframe notes: S-F03-07 Book Recommendations

Actor: Reader · Frame: 360px (export 3x = 1080px) · UI conventions: v0.8 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back navigation | Screen header | Returns to existing OPAC main menu | — |
| 2 | Screen title | Screen header | “Sách gợi ý cho bạn” | — |
| 3 | Preferences shortcut | Secondary button | “Sở thích” at the right of the header, in every signed-in state (Default, Cold-start, Topped-up, Loading, Error); opens S-F03-02 any time (D10b) | — |
| 4 | Section subtitle | Paragraph text | “Gợi ý được cá nhân hoá dựa trên lịch sử đọc và chủ đề bạn quan tâm.” (displayed in Default and Topped-up states) | FR-03-11 |
| 5 | Recommended book row | Book row | Book catalogue › title, author, neutral grey “Cover” placeholder; format label (“Bản giấy” / “Trực tuyến”) with icon. Tapping entire row opens Book Detail on OPAC | FR-01-01, FR-03-11 |
| 6 | Cold-start notice banner | Banner | “Bạn chưa có lịch sử đọc hoặc sở thích. Dưới đây là các sách được bạn đọc quan tâm nhiều nhất qua mã QR.” | FR-03-19 |
| 7 | Set preferences CTA | Text link | “Thiết lập sở thích đọc ngay”; styled as text link inside cold-start banner leading to S-F03-02 | FR-03-19 |
| 8 | Popular books section title | Headings / Section title | “Sách phổ biến” | FR-03-19 |
| 9 | Popular book row | Book row | Most popular catalogue books ranked by loan/QR scan count; tapping row opens OPAC Book Detail | FR-03-19 |
| 10 | Supplemented trending books | Book row | Trending catalogue books in the same subject category from the last 30 days, integrated into list when personalized matches < 3; each carries the Trend tag #13 | FR-03-20 |
| 11 | Loading placeholder | Skeleton | Skeleton rows for 5 book rows preserving layout during recommendation computation | MSG-05 |
| 12 | Page-level load error | Banner | MSG-04 — “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” with “Thử lại” button | FR-04-20 |
| 13 | Trending mark | Trend tag | «Xu hướng» with trending icon, below the format label, only on books added from trending titles; no recommendation-reason text on any row (D10a, D11) | FR-03-20 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | [s_f03_07.png](../img/s_f03_07/s_f03_07.png), [s_f03_07_numbered.png](../img/s_f03_07/s_f03_07_numbered.png) | Header with «Sở thích» button; personalised recommendation list (displays up to 10 books; wireframe illustrates representative sample) with format labels. Entire book row is tappable. Numbered image shows #1–#5 (re-exported 22/11/2026). | FR-03-11 |
| Cold-start | [s_f03_07_cold_start.png](../img/s_f03_07/s_f03_07_cold_start.png) | Reader has no history/preferences: header with «Sở thích» button, callout banner with “Thiết lập sở thích đọc ngay” text link, followed by popular books list. | FR-03-19 |
| Topped-up | [s_f03_07_topped_up.png](../img/s_f03_07/s_f03_07_topped_up.png) | Fewer than 3 personalised matches: shows personalized books supplemented by trending books in the same subject from the last 30 days; each trending book carries the Trend tag «Xu hướng». | FR-03-20 |
| Loading | [s_f03_07_loading.png](../img/s_f03_07/s_f03_07_loading.png) | Header with «Sở thích» button; skeleton book rows during recommendation calculation. | MSG-05 |
| Error | [s_f03_07_error.png](../img/s_f03_07/s_f03_07_error.png) | Header with «Sở thích» button; MSG-04 network load error banner with “Thử lại” action button. | FR-04-20 |
| Empty | *Not applicable* | Khi chưa có dữ liệu đọc cá nhân, hệ thống tự động hiển thị danh sách sách phổ biến nhất (FR-03-19), do đó màn hình không bao giờ bị trống. | FR-03-19 |
| Success | *Not applicable* | Màn hình hiển thị danh sách kết quả trực tiếp, không có thông báo Toast xác nhận riêng. | FR-03-11 |

## Actions and where they go

| Element / event | User action / system event | Result / destination |
|---|---|---|
| Open without session | Reader opens S-F03-07 without active session | M-F00-01 (Sign-in prompt modal with MSG-03: “Gợi ý riêng cho bạn cần tài khoản thẻ thư viện. Hãy đăng nhập để xem.”); after sign-in returns to S-F03-07 (FR-03-21) |
| Back navigation | Tap `<` button | Existing OPAC main menu (exit) |
| Sở thích (header Secondary button) | Tap, in any signed-in state | S-F03-02 (Reading history and preferences screen, UC-07), any time |
| Thiết lập sở thích đọc ngay | Tap text link in cold-start banner | S-F03-02 (UC-07) to set preferences; returning rebuilds recommendations |
| Book row (any recommended/popular/trending title) | Tap entire book row | OPAC Book Detail › leads to shelf location S-F01-01 (UC-01) |
| Thử lại (on MSG-04 error) | Tap “Thử lại” button | stays; retries loading recommendations on S-F03-07 |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f03-07).
