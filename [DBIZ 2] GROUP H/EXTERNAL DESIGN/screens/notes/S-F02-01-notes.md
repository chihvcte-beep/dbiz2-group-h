# Wireframe notes: S-F02-01 Book reviews

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back to existing OPAC Book Detail; title “Đánh giá sách” | — |
| 2 | Book context | Book row | Book catalogue › title, author plus neutral grey “Cover” placeholder: “Principles of Economics” · N. Gregory Mankiw | FR-02-02 |
| 3 | Review editor | Text area with counter | Book review › review text; plain text, 1–2,000 characters; counter n/2.000 | FR-02-01, FR-02-03, FR-02-11 |
| 4 | Anonymous posting | Checkbox | Reader accounts › full registered name; unchecked by default, checked displays “Bạn đọc ẩn danh” | FR-02-22 |
| 5 | Review guideline | Text link | Library review guideline; destination URL not supplied | AD-UC-13 Q1 |
| 6 | Submit review | Primary button | “Đăng đánh giá” / “Lưu thay đổi” when editing | FR-02-01, FR-02-03 |
| 7 | Own review | Review item | Book review › review text, reviewer, posted date, is own review; actions “Sửa”, “Xoá đánh giá” | FR-02-03, FR-02-04 |
| 8 | Other readers’ reviews | Review item | Book review › review text, reviewer, posted date; “Báo cáo đánh giá” on S-F02-01 | FR-02-02, FR-02-13, FR-02-09, FR-02-21 |
| 9 | Next page | Load more button | “Xem thêm đánh giá”; 10 per page, newest first; only when more pages exist | FR-02-02 |
| 10 | Empty list message | Empty state | “Không có đánh giá nào để hiển thị.”; replaces review list | FR-02-15 |
| 11 | Page-level feedback | Banner | MSG-04 network error; “Bạn đã báo cáo đánh giá này.” for duplicate report | FR-04-20, FR-02-21 |
| 12 | Field validation feedback | Inline error | Review text empty / over 2,000 characters; invalid ownership action feedback | FR-02-01, FR-02-11 |
| 13 | Success confirmation | Toast | “Đã đăng đánh giá.” / “Đã cập nhật đánh giá.” / “Đã xoá đánh giá.” | FR-02-12, FR-02-09 |
| 14 | Loading placeholder | Skeleton | Same shape as book context, form and review list | MSG-05 |
| 15 | Retry action | Secondary button | “Thử lại” inside MSG-04 Banner | FR-04-20 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F02-01.png | Book context, review editor, own review, other reviews, 10-item page and next-page action | FR-02-01, FR-02-02, FR-02-03, FR-02-04, FR-02-09 |
| Empty | img/S-F02-01-empty.png | Book exists but has no published reviews; one-line empty message, no review list | FR-02-15 |
| Loading | img/S-F02-01-loading.png | Skeleton blocks replace content; no loading text | MSG-05 |
| Error | img/S-F02-01-error.png | Over-limit review text with Inline error; error-numbered image included | FR-02-01, FR-02-11 |
| Error-2 | img/S-F02-01-error-2.png | MSG-04 network error with retry action; numbered variant included | FR-04-20 |
| Error-3 | img/S-F02-01-error-3.png | Duplicate report message “Bạn đã báo cáo đánh giá này.”; numbered variant included | FR-02-21 |
| Success | img/S-F02-01-success.png | Confirmation toast and refreshed review list | FR-02-12, FR-02-09 |

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
| 1 | [NEEDS CLARIFICATION: AD-UC-14 Q2 allows reporting one’s own review, but UI conventions v0.7 section 3 says own reviews show Edit/Delete and other readers’ reviews show Report. Which rule controls the release UI?] | Follow v0.7 component rule in this wireframe: Report appears on other readers’ reviews only; flag for Linh/Owner C. |
| 2 | [NEEDS CLARIFICATION: What is the exact destination URL for the library review guideline?] | Render the Text link label only; destination remains unresolved. |
| 3 | [NEEDS CLARIFICATION: Does “Xem thêm đánh giá” append or replace the current 10-item page?] | Render as the page-next control; no invented pagination mechanics. |
| 4 | [NEEDS CLARIFICATION: UI conventions list Book row usage on other screens, not S-F02-01. Is it approved as the book-context block here?] | Reuse the existing Book row style without adding a cover image or access-format content. |
