# Wireframe notes: S-F02-02 Book information and reviews (QR landing page)

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Screen title | Screen header | Title “Thông tin và đánh giá sách” only; no Back button in any state (page opened only by scanning the QR label; D5) | — |
| 2 | Book information | Book row | Book catalogue › neutral grey “Cover” placeholder, title, author, subjects, summary; no Format label (D21); sample “Principles of Economics” | FR-02-05 |
| 3 | OPAC book link | Text link | “Xem sách trên OPAC” → existing OPAC Book Detail | FR-02-05 |
| 4 | Review editor (same review panel as S-F02-01) | Text area with counter | Book review › review text; plain text, 1–2,000 characters; counter n/2.000 (same review panel as S-F02-01) | FR-02-01, FR-02-03, FR-02-04, FR-02-11 |
| 5 | Anonymous posting (same review panel as S-F02-01) | Checkbox | “Đăng ẩn danh”; full registered name or “Bạn đọc ẩn danh” (same review panel as S-F02-01) | FR-02-22 |
| 6 | Review hint (same review panel as S-F02-01) | Text area with counter | Hint line under the review field, small muted text: “Đánh giá không được chứa từ ngữ xúc phạm, quảng cáo hoặc thông tin cá nhân.” (MSG-14, D20); not a link (same review panel as S-F02-01) | D20 |
| 7 | Submit review (same review panel as S-F02-01) | Primary button | “Đăng đánh giá” / “Lưu thay đổi” (same review panel as S-F02-01) | FR-02-01, FR-02-03 |
| 8 | Own review (same review panel as S-F02-01) | Review item | Same Review item component as S-F02-01 (no review ID code on UI); text buttons “Sửa”, “Xoá đánh giá”; no Report on QR page | FR-02-03, FR-02-04, FR-02-13 |
| 9 | Other readers’ reviews / Page-level feedback | Review item / Banner | Same Review item component as S-F02-01 (no review ID code on UI, no Report on QR page); Banner for QR error “Không tìm thấy sách.”, MSG-04 network error, or invalid review content | FR-02-02, FR-02-13, FR-02-16, FR-04-20, FR-02-11 |
| 10 | Load more reviews (same review panel as S-F02-01) | Load more button | “Xem thêm đánh giá”, full width at the end of the review list; shown while more published reviews remain; next 10 reviews (D6) | FR-02-02 |
| 11 | Empty list message | Empty state | “Không có đánh giá nào để hiển thị. Hãy là người đầu tiên viết đánh giá cho cuốn sách này.” while book information remains visible | FR-02-15 |
| 12 | Success confirmation | Toast | “Đã đăng đánh giá.” / “Đã cập nhật đánh giá.” / “Đã xoá đánh giá.” | FR-02-12 |
| 13 | Loading placeholder | Skeleton | Replaces book information and review content | MSG-05 |
| 14 | Field validation feedback | Inline error | Shared review-panel text validation (empty or over 2,000 characters) | FR-02-01, FR-02-11 |
| 15 | Retry action | Secondary button | “Thử lại” inside MSG-04 Banner | FR-04-20 |
| 16 | Way out of the invalid-QR error | Text link | “Về OPAC” in the error Banner, shown only when the QR code is linked to no book; opens the existing OPAC main menu | D37 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | [s_f02_02.png](../img/s_f02_02/s_f02_02.png) | Title-only header (no Back), book title, author, subjects, summary, OPAC link, shared review panel (no review IDs, no Report), first 10 reviews and Load more “Xem thêm đánh giá” (#10); numbered variant in [s_f02_02_numbered.png](../img/s_f02_02/s_f02_02_numbered.png) (#1–#10, re-exported 22/11/2026) | FR-02-05, FR-02-01, FR-02-02 |
| Empty | [s_f02_02_empty.png](../img/s_f02_02/s_f02_02_empty.png) | Book found, no published reviews; empty state message (#11) with prompt to write first review while book information stays visible; no Load more | FR-02-15 |
| Loading | [s_f02_02_loading.png](../img/s_f02_02/s_f02_02_loading.png) | Title-only header; Skeleton blocks (#13) replace book information and reviews | MSG-05 |
| Error | [s_f02_02_error.png](../img/s_f02_02/s_f02_02_error.png) | Invalid QR: “Không tìm thấy sách.” with next-step guidance and the “Về OPAC” link in Banner (D37) | FR-02-16 |
| Error-2 | [s_f02_02_error_2.png](../img/s_f02_02/s_f02_02_error_2.png) | MSG-04 network error with retry action (#15); page content preserved, including Load more (#10) | FR-04-20 |
| Error-3 | [s_f02_02_error_3.png](../img/s_f02_02/s_f02_02_error_3.png) | Shared review-panel validation error (FR-02-11) with Banner and Inline error (#14); page content preserved, including Load more (#10) | FR-02-11, FR-02-01 |
| Success | [s_f02_02_success.png](../img/s_f02_02/s_f02_02_success.png) | Review action confirmation Toast (#12) and full refreshed review list with Load more (#10) | FR-02-12 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Xem sách trên OPAC | tap | Existing OPAC Book Detail (exit) |
| Shared review panel / Submit review | write and submit | stays |
| Shared review panel / Submit while signed out | request sign-in | M-F00-01 (reused; owned by Ha), then S-F00-01 → S-F00-02 → S-F02-02 |
| Own review / Sửa | edit and save own review | stays; if signed out, M-F00-01 then return to S-F02-02 |
| Own review / Xoá đánh giá | request deletion | M-F02-01-01; if signed out, M-F00-01 then return to S-F02-02 |
| Xem thêm đánh giá | tap | stays; next 10 published reviews appended; button hidden when none remain (same as S-F02-01) |
| Thử lại | retry after load failure | stays |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f02-02).