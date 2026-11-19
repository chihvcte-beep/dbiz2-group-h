# Wireframe notes: S-F03-07 Book Recommendations

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back to existing OPAC main menu; title “Gợi ý sách cho bạn” | — |
| 2 | Preferences shortcut | Header action button | “Tùy chỉnh sở thích”; secondary action leading directly to S-F03-02 | — |
| 3 | Section description | Subtitle | “Gợi ý được cá nhân hoá dựa trên lịch sử đọc và chủ đề bạn quan tâm” | FR-03-11 |
| 4 | Recommended book row | Book row | Book catalogue › title, author plus neutral grey “Cover” placeholder; access format tag (“Bản giấy” / “Trực tuyến”) | FR-03-11 |
| 5 | Recommendation reason tag | Metadata tag | “Phù hợp sở thích: Kinh tế” / “Dựa trên sách đã đọc”; explains basis of AI recommendation | FR-03-11 |
| 6 | View shelf location link | Row action link | Tapping book row opens OPAC Book Detail › leads to S-F01-01 (UC-01) | FR-01-01, FR-03-11 |
| 7 | Cold-start notice banner | Callout banner | “Bạn chưa thiết lập lịch sử hoặc sở thích đọc. Thư viện gợi ý các cuốn sách được bạn đọc quét mã QR nhiều nhất.” | FR-03-19 |
| 8 | Set preferences CTA | Primary button | “Thiết lập sở thích đọc ngay”; prominent button inside cold-start banner leading to S-F03-02 | FR-03-19 |
| 9 | Popular books list | Book row list | Book QR codes › scan count / loans; fallback recommendation ranked by popularity | FR-03-19 |
| 10 | Popularity scan badge | Metadata badge | “Quét QR: 142 lượt” / “Mượn nhiều”; indicates popularity signal | FR-03-19 |
| 11 | Trending supplement divider | Section divider | “Bổ sung sách xu hướng mượn nhiều trong 30 ngày qua (cùng chủ đề Kinh tế)”; shown when personalized titles < 3 | FR-03-20 |
| 12 | Trending book row | Book row | Trending catalogue books matching reader's subject interest | FR-03-20 |
| 13 | Trending badge | Tag / Badge | “Xu hướng mượn nhiều”; highlights supplemented titles | FR-03-20 |
| 14 | Loading placeholder | Skeleton | Skeleton cards for 5 book rows preserving layout during AI score computation | MSG-05 |
| 15 | Page-level load error | Banner with retry | MSG-04 — “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” with “Thử lại” button | FR-04-20 |
| 16 | Sign-in modal prompt | Modal trigger (M-F00-01) | Prompt shown when unauthenticated visitor enters: “Đăng nhập bằng thẻ thư viện để xem danh sách sách được gợi ý riêng cho bạn” | FR-03-21 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F03-07.png, img/S-F03-07-numbered.png | Personalised recommendation list (up to 10 books) with subject matching tags and access format labels. | FR-03-11 |
| Cold-start | img/S-F03-07-cold-start.png | Reader has no history/preferences: callout banner with “Thiết lập sở thích đọc ngay” button, followed by popular books by QR scan count. | FR-03-19 |
| Topped-up | img/S-F03-07-topped-up.png | Fewer than 3 personalised matches: shows matched books supplemented by trending books in the same subject from the last 30 days. | FR-03-20 |
| Loading | img/S-F03-07-loading.png | Skeleton book cards during recommendation calculation. | MSG-05 |
| Error | img/S-F03-07-error.png | MSG-04 network load error banner with Try again action. | FR-04-20 |

## Actions and where they go

| Element | User action | Goes to |
|---|---|---|
| Back navigation | Tap `<` | Existing OPAC main menu (exit) |
| Tùy chỉnh sở thích (header button) | Tap button | Navigates to Reading history & preferences screen S-F03-02 (UC-07) |
| Thiết lập sở thích đọc ngay (banner CTA) | Tap CTA | Navigates to S-F03-02 (UC-07) to initialize preferences; returning rebuilds list |
| Book row | Tap book | Opens book on existing OPAC Book Detail › leads to shelf location S-F01-01 (UC-01) |
| Thử lại | Tap retry on MSG-04 | Retries loading recommendations on S-F03-07 |

## Open questions

| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: What metric defines popular books in cold-start if QR scan counting is disabled?] | Team consensus (2026-11-04): Use highest loan counts in synced loan records (AD-UC-09 Q1). |
| 2 | [NEEDS CLARIFICATION: What defines "trending" for topping up short lists (FR-03-20)?] | Team consensus (2026-11-04): Most borrowed titles in the same subject category within the last 30 days (AD-UC-09 Q2). |
| 3 | [NEEDS CLARIFICATION: What is the maximum number of recommendations displayed on S-F03-07?] | Team consensus (2026-11-04): 10 books (AD-UC-09 Q3). |
| 4 | [NEEDS CLARIFICATION: Should supplemented trending books have a distinct visual badge?] | Default drawn: Yes, labelled with “Xu hướng” tag and separated by a clean subsection divider for transparency. |

## Scope and implementation notes

- Personalised recommendations strictly require a signed-in reader account (FR-03-21). Unauthenticated access triggers `M-F00-01` before landing on this screen.
- Recommendations synthesize three data sources: reading history entries, registered reading preferences, and chatbot inquiry topics (FR-03-11).
- If personalized matches are < 3, the list automatically tops up with trending books in the same subject categories without manual filter toggling (FR-03-20).
- Cold-start readers are actively guided to S-F03-02 via prominent callout to break out of zero-state (FR-03-19).
