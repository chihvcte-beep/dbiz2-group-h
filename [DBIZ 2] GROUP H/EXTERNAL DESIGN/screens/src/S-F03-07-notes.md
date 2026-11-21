# Wireframe notes: S-F03-07 Book Recommendations

Actor: Reader · Frame: 360px (export 3x = 1080px) · UI conventions: v0.7 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back navigation | Screen header | Returns to existing OPAC main menu | — |
| 2 | Screen title | Screen header | “Sách gợi ý cho bạn” | — |
| 3 | Preferences shortcut | Text link | “Sở thích” header action; allows quick access to S-F03-02 | — |
| 4 | Section subtitle | Paragraph text | “Gợi ý được cá nhân hoá dựa trên lịch sử đọc và chủ đề bạn quan tâm.” (displayed in Default and Topped-up states) | FR-03-11 |
| 5 | Recommended book row | Book row | Book catalogue › title, author, neutral grey “Cover” placeholder; format label (“Bản giấy” / “Trực tuyến”) with icon. Tapping entire row opens Book Detail on OPAC | FR-01-01, FR-03-11 |
| 6 | Cold-start notice banner | Banner | “Bạn chưa có lịch sử đọc hoặc sở thích. Dưới đây là các sách được bạn đọc quan tâm nhiều nhất qua mã QR.” | FR-03-19 |
| 7 | Set preferences CTA | Text link | “Thiết lập sở thích đọc ngay”; styled as text link inside cold-start banner leading to S-F03-02 | FR-03-19 |
| 8 | Popular books section title | Headings / Section title | “Sách phổ biến” | FR-03-19 |
| 9 | Popular book row | Book row | Most popular catalogue books ranked by loan/QR scan count; tapping row opens OPAC Book Detail | FR-03-19 |
| 10 | Supplemented trending books | Book row | Trending catalogue books in the same subject category from the last 30 days, integrated into list when personalized matches < 3 | FR-03-20 |
| 11 | Loading placeholder | Skeleton | Skeleton rows for 5 book rows preserving layout during recommendation computation | MSG-05 |
| 12 | Page-level load error | Banner | MSG-04 — “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” with “Thử lại” button | FR-04-20 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F03-07.png, img/S-F03-07-numbered.png | Personalised recommendation list (displays up to 10 books; wireframe illustrates representative sample) with format labels. Entire book row is tappable. | FR-03-11 |
| Cold-start | img/S-F03-07-cold-start.png | Reader has no history/preferences: callout banner with “Thiết lập sở thích đọc ngay” text link, followed by popular books list. | FR-03-19 |
| Topped-up | img/S-F03-07-topped-up.png | Fewer than 3 personalised matches: shows personalized books supplemented by trending books in the same subject from the last 30 days. | FR-03-20 |
| Loading | img/S-F03-07-loading.png | Skeleton book rows during recommendation calculation. | MSG-05 |
| Error | img/S-F03-07-error.png | MSG-04 network load error banner with “Thử lại” action button. | FR-04-20 |
| Empty | *Not applicable* | Khi chưa có dữ liệu đọc cá nhân, hệ thống tự động hiển thị danh sách sách phổ biến nhất (FR-03-19), do đó màn hình không bao giờ bị trống. | FR-03-19 |
| Success | *Not applicable* | Màn hình hiển thị danh sách kết quả trực tiếp, không có thông báo Toast xác nhận riêng. | FR-03-11 |

## Actions and where they go

| Element / event | User action / system event | Result / destination |
|---|---|---|
| Open without session | Reader opens S-F03-07 without active session | M-F00-01 (Sign-in prompt modal with MSG-03: “Gợi ý riêng cho bạn cần tài khoản thẻ thư viện. Hãy đăng nhập để xem.”); after sign-in returns to S-F03-07 (FR-03-21) |
| Back navigation | Tap `<` button | Existing OPAC main menu (exit) |
| Sở thích (header link) | Tap header link | S-F03-02 (Reading history and preferences screen, UC-07) |
| Thiết lập sở thích đọc ngay | Tap text link in cold-start banner | S-F03-02 (UC-07) to set preferences; returning rebuilds recommendations |
| Book row (any recommended/popular/trending title) | Tap entire book row | OPAC Book Detail › leads to shelf location S-F01-01 (UC-01) |
| Thử lại (on MSG-04 error) | Tap “Thử lại” button | stays; retries loading recommendations on S-F03-07 |

## Open questions

| # | Question | Current treatment |
|---|---|---|
| 1 | What metric defines popular books in cold-start if QR scan counting is disabled? | Decided — AD-UC-09 Q1 (04/11/2026): Use highest loan counts in synced loan records. |
| 2 | What defines “trending” for topping up short lists (FR-03-20)? | Decided — AD-UC-09 Q2 (04/11/2026): Most borrowed titles in the same subject category within the last 30 days. |
| 3 | What is the maximum number of recommendations displayed on S-F03-07? | Decided — AD-UC-09 Q3 (04/11/2026): 10 books (wireframe illustrates representative sample). |
| 4 | Recommendation rationale tag: Should individual rows display explanatory tags (e.g. “Khớp sở thích: Kinh tế”)? | Provisional: No tag drawn, as instructed in review feedback. Awaiting team decision whether to add rationale badges. |
| 5 | Header preferences shortcut: Should the header shortcut to S-F03-02 be present in all states or only in cold-start? | Provisional: Retained in header. Team to confirm alignment between screen-transition.md and screen-list.md. |
