# Wireframe notes: S-F02-01 Book reviews

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back to existing OPAC Book Detail; title “Đánh giá sách” | — |
| 2 | Book context | Book row | Book catalogue › title, author plus neutral grey “Cover” placeholder: “Principles of Economics” · N. Gregory Mankiw | FR-02-02 |
| 3 | Review editor | Text area with counter | Book review › review text; plain text, 1–2,000 characters; counter n/2.000 | FR-02-01, FR-02-03, FR-02-11 |
| 4 | Anonymous posting | Checkbox | Reader accounts › full registered name; unchecked by default, checked displays “Bạn đọc ẩn danh” | FR-02-22 |
| 5 | Review guideline | Text link | Library review guideline; destination URL not supplied | AD-UC-13 Q1 |
| 6 | Submit review | Primary button | “Đăng đánh giá” / “Lưu thay đổi” when editing (editing keeps existing review text, “Đăng ẩn danh” state, “Lưu thay đổi” label, and cancel/exit action) | FR-02-01, FR-02-03, FR-02-22 |
| 7 | Own review | Review item | Book review › review text, reviewer, posted date, is own review (no review ID shown on UI, no “edited” label); Text buttons “Sửa”, “Xoá đánh giá” | FR-02-03, FR-02-04 |
| 8 | Other readers’ reviews | Review item | Book review › review text, reviewer, posted date (no review ID shown on UI); Text button “Báo cáo đánh giá” on S-F02-01 only | FR-02-02, FR-02-13, FR-02-09, FR-02-21 |
| 9 | Next page | Load more button | “Xem thêm đánh giá”; 10 per page, newest first; only when more pages exist | FR-02-02 |
| 10 | Empty list message | Empty state | “Không có đánh giá nào để hiển thị. Hãy là người đầu tiên viết đánh giá.” (when book exists with no reviews); if book is not found, keep Book context/form or show not-found guidance with next step | FR-02-15 |
| 11 | Page-level feedback | Banner | MSG-04 network error (“Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.”); duplicate report “Bạn đã báo cáo đánh giá này.”; invalid ownership action “Bạn không thể sửa hoặc xoá đánh giá của người khác.” | FR-04-20, FR-02-21, FR-02-11 |
| 12 | Field validation feedback | Inline error | Empty review text: “Bạn chưa viết nội dung đánh giá. Hãy nhập ít nhất 1 ký tự.”; over 2,000 characters: “Nội dung đánh giá vượt quá 2.000 ký tự. Hãy rút gọn nội dung.” | FR-02-01, FR-02-11 |
| 13 | Success confirmation | Toast | “Đã đăng đánh giá.” / “Đã cập nhật đánh giá.” / “Đã xoá đánh giá.” / “Đã gửi báo cáo.” | FR-02-12, FR-02-09 |
| 14 | Loading placeholder | Skeleton | Same shape as book context, form and review list | MSG-05 |
| 15 | Retry action | Secondary button | “Thử lại” inside MSG-04 Banner | FR-04-20 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F02-01.png (numbered: img/S-F02-01-numbered.png) | Book context, review editor, own review, other readers’ reviews (no review IDs), 10-item page and next-page action; elements 1–9 numbered | FR-02-01, FR-02-02, FR-02-03, FR-02-04, FR-02-09 |
| Empty | img/S-F02-01-empty.png (numbered: img/S-F02-01-empty-numbered.png) | Book context and review editor visible; Empty state with next step in place of review list; element 10 numbered | FR-02-15 |
| Loading | img/S-F02-01-loading.png (numbered: img/S-F02-01-loading-numbered.png) | Skeleton blocks replace content; no loading text; element 14 numbered | MSG-05 |
| Error | img/S-F02-01-error.png (numbered: img/S-F02-01-error-numbered.png) | Existing book context and review list preserved; over-limit review text with Inline error; element 12 numbered | FR-02-01, FR-02-11 |
| Error-2 | img/S-F02-01-error-2.png (numbered: img/S-F02-01-error-2-numbered.png) | Existing book context and review list preserved; MSG-04 network error Banner with “Thử lại” button; elements 11 and 15 numbered | FR-04-20 |
| Error-3 | img/S-F02-01-error-3.png (numbered: img/S-F02-01-error-3-numbered.png) | Existing book context and review list preserved; duplicate report or invalid ownership Banner; element 11 numbered | FR-02-21, FR-02-11 |
| Success | img/S-F02-01-success.png (numbered: img/S-F02-01-success-numbered.png) | Refreshed review list keeping reader’s own review alongside new/other reviews, plus confirmation Toast; element 13 numbered | FR-02-12, FR-02-09 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Back | tap | Existing OPAC Book Detail (exit) |
| Review editor / Submit review | enter plain text and submit | stays |
| Review editor / Submit while signed out | request sign-in | M-F00-01 (reused; owned by Ha), then S-F00-01 → S-F00-02 → S-F02-01 |
| Review guideline | open library review rules | stays (destination URL unresolved) |
| Own review / Sửa | edit own review text and save | stays; if signed out, M-F00-01 then return to S-F02-01 |
| Own review / Xoá đánh giá | request deletion | M-F02-01-01; if signed out, M-F00-01 then return to S-F02-01 |
| Other review / Báo cáo đánh giá | request report | M-F02-01-02 |
| Report while signed out | request sign-in | M-F00-01 (reused; owned by Ha), then S-F00-01 → S-F00-02 → S-F02-01 |
| Xem thêm đánh giá | request next page | stays |
| Thử lại | retry after load failure | stays |

## Open questions
| # | Question | Default drawn |
|---|---|---|
| 1 | Closed 19/11/2026: No — Report only on other readers' reviews (AD-UC-14 Q2; ui-conventions v0.8). | Report button appears on other readers’ reviews only; own reviews show “Sửa” and “Xoá đánh giá”. |
| 2 | [NEEDS CLARIFICATION: What is the exact destination URL for the library review guideline?] | Render the Text link label only; destination remains unresolved. |
| 3 | [NEEDS CLARIFICATION: Does “Xem thêm đánh giá” append or replace the current 10-item page?] | Render as the page-next control; no invented pagination mechanics. |
| 4 | [NEEDS CLARIFICATION: UI conventions list Book row usage on other screens, not S-F02-01. Is it approved as the book-context block here?] | Reuse the existing Book row style without a cover image or access-format label; flag for Linh/group. |